# Sharded timestamps

If a collection contains documents with sequential indexed values, Firestore limits the write rate to 500 writes per second. This page describes how to shard a document field to overcome this limit. First, let's define what we mean by "sequential indexed fields" and clarify when this limit applies.

#### Sequential indexed fields

"Sequential indexed fields" means any collection of documents that contains a monotonically increasing or decreasing indexed field. In many cases, this means a `  timestamp  ` field, but any monotonically increasing or decreasing field value can trigger the write limit of 500 writes per second.

For example, the limit applies to a collection of `  user  ` documents with indexed field `  userid  ` if the app assigns `  userid  ` values like so:

  - `  1281, 1282, 1283, 1284, 1285, ...  `

On the other hand, not all `  timestamp  ` fields trigger this limit. If a `  timestamp  ` field tracks randomly distributed values, the write limit does not apply. The actual value of the field does not matter either, only that the field is monotonically increasing or decreasing. For example, both of the following sets of monotonically increasing field values trigger the write limit:

  - `  100000, 100001, 100002, 100003, ...  `
  - `  0, 1, 2, 3, ...  `

## Sharding a timestamp field

Assume your app uses a monotonically increasing `  timestamp  ` field. If your app doesn't use the `  timestamp  ` field in any queries, you can remove the 500 writes per second limit by not indexing the timestamp field. If you do require a `  timestamp  ` field for your queries, you can work around the limit by using *sharded timestamps* :

1.  Add a `  shard  ` field alongside the `  timestamp  ` field. Use `  1..n  ` distinct values for the `  shard  ` field. This raises the write limit for the collection to `  500*n  ` , but you must aggregate `  n  ` queries.
2.  Update your write logic to *randomly* assign a `  shard  ` value to each document.
3.  Update your queries to aggregate the sharded result sets.
4.  Disable single-field indexes for both the `  shard  ` field and the `  timestamp  ` field. Delete existing composite indexes that contain the `  timestamp  ` field.
5.  Create new composite indexes to support your updated queries. The order of the fields in an index matters, and the `  shard  ` field must come before the `  timestamp  ` field. Any indexes that include the `  timestamp  ` field must also include the `  shard  ` field.

You should implement sharded timestamps only in use cases with sustained write rates above 500 writes per second. Otherwise, this is a pre-mature optimization. Sharding a `  timestamp  ` field removes the 500 writes per second restriction but with the trade-off of needing client-side query aggregations.

The following examples show how to shard a `  timestamp  ` field and how to query a sharded result set.

### Example data model and queries

As an example, imagine an app for near real-time analysis of financial instruments like currencies, common stocks, and ETFs. This app writes documents to an `  instruments  ` collection like so:

##### Node.js

``` javascript
async function insertData() {
  const instruments = [
    {
      symbol: 'AAA',
      price: {
        currency: 'USD',
        micros: 34790000
      },
      exchange: 'EXCHG1',
      instrumentType: 'commonstock',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.010Z'))
    },
    {
      symbol: 'BBB',
      price: {
        currency: 'JPY',
        micros: 64272000000
      },
      exchange: 'EXCHG2',
      instrumentType: 'commonstock',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.101Z'))
    },
    {
      symbol: 'Index1 ETF',
      price: {
        currency: 'USD',
        micros: 473000000
      },
      exchange: 'EXCHG1',
      instrumentType: 'etf',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.001Z'))
    }
  ];

  const batch = fs.batch();
  for (const inst of instruments) {
    const ref = fs.collection('instruments').doc();
    batch.set(ref, inst);
  }

  await batch.commit();
}
nonShardedTimestamps.js
```

This app runs the following queries and orders by the `  timestamp  ` field:

##### Node.js

``` javascript
function createQuery(fieldName, fieldOperator, fieldValue, limit = 5) {
  return fs.collection('instruments')
      .where(fieldName, fieldOperator, fieldValue)
      .orderBy('timestamp', 'desc')
      .limit(limit)
      .get();
}

function queryCommonStock() {
  return createQuery('instrumentType', '==', 'commonstock');
}

function queryExchange1Instruments() {
  return createQuery('exchange', '==', 'EXCHG1');
}

function queryUSDInstruments() {
  return createQuery('price.currency', '==', 'USD');
}
nonShardedTimestamps.js
```

``` javascript
insertData()
    .then(() => {
      const commonStock = queryCommonStock()
          .then(
              (docs) => {
                console.log('--- queryCommonStock: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      const exchange1Instruments = queryExchange1Instruments()
          .then(
              (docs) => {
                console.log('--- queryExchange1Instruments: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      const usdInstruments = queryUSDInstruments()
          .then(
              (docs) => {
                console.log('--- queryUSDInstruments: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      return Promise.all([commonStock, exchange1Instruments, usdInstruments]);
    });nonShardedTimestamps.js
```

After some research, you determine that the app will receive between 1,000 and 1,500 instrument updates per second. This surpasses the 500 writes per second allowed for collections containing documents with indexed timestamp fields. To increase the write throughput, you need 3 shard values, `  MAX_INSTRUMENT_UPDATES/500 = 3  ` . This example uses the shard values `  x  ` , `  y  ` , and `  z  ` . You can also use numbers or other characters for your shard values.

### Adding a shard field

Add a `  shard  ` field to your documents. Set the `  shard  ` field to values `  x  ` , `  y  ` , or `  z  ` which raises the write limit on the collection to 1,500 writes per second.

##### Node.js

``` javascript
// Define our 'K' shard values
const shards = ['x', 'y', 'z'];
// Define a function to help 'chunk' our shards for use in queries.
// When using the 'in' query filter there is a max number of values that can be
// included in the value. If our number of shards is higher than that limit
// break down the shards into the fewest possible number of chunks.
function shardChunks() {
  const chunks = [];
  let start = 0;
  while (start < shards.length) {
    const elements = Math.min(MAX_IN_VALUES, shards.length - start);
    const end = start + elements;
    chunks.push(shards.slice(start, end));
    start = end;
  }
  return chunks;
}

// Add a convenience function to select a random shard
function randomShard() {
  return shards[Math.floor(Math.random() * Math.floor(shards.length))];
}
shardedTimestamps.js
```

``` javascript
async function insertData() {
  const instruments = [
    {
      shard: randomShard(),  // add the new shard field to the document
      symbol: 'AAA',
      price: {
        currency: 'USD',
        micros: 34790000
      },
      exchange: 'EXCHG1',
      instrumentType: 'commonstock',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.010Z'))
    },
    {
      shard: randomShard(),  // add the new shard field to the document
      symbol: 'BBB',
      price: {
        currency: 'JPY',
        micros: 64272000000
      },
      exchange: 'EXCHG2',
      instrumentType: 'commonstock',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.101Z'))
    },
    {
      shard: randomShard(),  // add the new shard field to the document
      symbol: 'Index1 ETF',
      price: {
        currency: 'USD',
        micros: 473000000
      },
      exchange: 'EXCHG1',
      instrumentType: 'etf',
      timestamp: Timestamp.fromMillis(
          Date.parse('2019-01-01T13:45:23.001Z'))
    }
  ];

  const batch = fs.batch();
  for (const inst of instruments) {
    const ref = fs.collection('instruments').doc();
    batch.set(ref, inst);
  }

  await batch.commit();
}
shardedTimestamps.js
```

### Querying the sharded timestamp

Adding a `  shard  ` field requires that you update your queries to aggregate sharded results:

##### Node.js

``` javascript
function createQuery(fieldName, fieldOperator, fieldValue, limit = 5) {
  // For each shard value, map it to a new query which adds an additional
  // where clause specifying the shard value.
  return Promise.all(shardChunks().map(shardChunk => {
        return fs.collection('instruments')
            .where('shard', 'in', shardChunk)  // new shard condition
            .where(fieldName, fieldOperator, fieldValue)
            .orderBy('timestamp', 'desc')
            .limit(limit)
            .get();
      }))
      // Now that we have a promise of multiple possible query results, we need
      // to merge the results from all of the queries into a single result set.
      .then((snapshots) => {
        // Create a new container for 'all' results
        const docs = [];
        snapshots.forEach((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            // append each document to the new all container
            docs.push(doc);
          });
        });
        if (snapshots.length === 1) {
          // if only a single query was returned skip manual sorting as it is
          // taken care of by the backend.
          return docs;
        } else {
          // When multiple query results are returned we need to sort the
          // results after they have been concatenated.
          // 
          // since we're wanting the `limit` newest values, sort the array
          // descending and take the first `limit` values. By returning negated
          // values we can easily get a descending value.
          docs.sort((a, b) => {
            const aT = a.data().timestamp;
            const bT = b.data().timestamp;
            const secondsDiff = aT.seconds - bT.seconds;
            if (secondsDiff === 0) {
              return -(aT.nanoseconds - bT.nanoseconds);
            } else {
              return -secondsDiff;
            }
          });
          return docs.slice(0, limit);
        }
      });
}

function queryCommonStock() {
  return createQuery('instrumentType', '==', 'commonstock');
}

function queryExchange1Instruments() {
  return createQuery('exchange', '==', 'EXCHG1');
}

function queryUSDInstruments() {
  return createQuery('price.currency', '==', 'USD');
}
shardedTimestamps.js
```

``` javascript
insertData()
    .then(() => {
      const commonStock = queryCommonStock()
          .then(
              (docs) => {
                console.log('--- queryCommonStock: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      const exchange1Instruments = queryExchange1Instruments()
          .then(
              (docs) => {
                console.log('--- queryExchange1Instruments: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      const usdInstruments = queryUSDInstruments()
          .then(
              (docs) => {
                console.log('--- queryUSDInstruments: ');
                docs.forEach((doc) => {
                  console.log(`doc = ${util.inspect(doc.data(), {depth: 4})}`);
                });
              }
          );
      return Promise.all([commonStock, exchange1Instruments, usdInstruments]);
    });shardedTimestamps.js
```

### Update index definitions

To remove the 500 writes per second constraint, delete the existing single-field and composite indexes that use the `  timestamp  ` field.

#### Delete composite index definitions

### Firebase Console

1.  Open the ***Firestore Composite Indexes*** page in the Firebase console.

2.  For each index that contains the `  timestamp  ` field, click the more\_vert button and click ***Delete*** .

### GCP Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Indexes** , and then click the **Composite** tab.

4.  Use the **Filter** field to search for index definitions that contain the `  timestamp  ` field.

5.  For each of these indexes, click the more\_vert button and click ***Delete*** .

### Firebase CLI

1.  If you haven't set up the Firebase CLI, [follow these direction to install the CLI and run the `  firebase init  ` command](https://firebase.google.com/docs/cli#install_the_firebase_cli) . During the `  init  ` command, make sure to select `  Firestore: Deploy rules and create indexes for Firestore  ` .

2.  During setup, the Firebase CLI downloads your existing index definitions to a file named, by default, `  firestore.indexes.json  ` .

3.  Remove any index definitions that contain the `  timestamp  ` field, for example:
    
    ``` text
    {
    "indexes": [
      // Delete composite index definition that contain the timestamp field
      {
        "collectionGroup": "instruments",
        "queryScope": "COLLECTION",
        "fields": [
          {
            "fieldPath": "exchange",
            "order": "ASCENDING"
          },
          {
            "fieldPath": "timestamp",
            "order": "DESCENDING"
          }
        ]
      },
      {
        "collectionGroup": "instruments",
        "queryScope": "COLLECTION",
        "fields": [
          {
            "fieldPath": "instrumentType",
            "order": "ASCENDING"
          },
          {
            "fieldPath": "timestamp",
            "order": "DESCENDING"
          }
        ]
      },
      {
        "collectionGroup": "instruments",
        "queryScope": "COLLECTION",
        "fields": [
          {
            "fieldPath": "price.currency",
            "order": "ASCENDING"
          },
          {
            "fieldPath": "timestamp",
            "order": "DESCENDING"
          }
        ]
      },
     ]
    }
    ```

4.  Deploy your updated index definitions:
    
    ``` text
    firebase deploy --only firestore:indexes
    ```

#### Update Single-field index definitions

### Firebase Console

1.  Open the ***Firestore Single Field Indexes*** page in the Firebase console.

2.  Click ***Add Exemption*** .

3.  For ***Collection ID*** , enter `  instruments  ` . For ***Field path*** , enter `  timestamp  ` .

4.  Under ***Query scope*** , select both ***Collection*** and ***Collection group*** .

5.  Click ***Next***

6.  Toggle all the index settings to ***Disabled*** . Click ***Save*** .

7.  Repeat the same steps for the `  shard  ` field.

### GCP Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Indexes** , and then click the **Single Field** tab.

4.  Click the ***Single Field*** tab.

5.  Click ***Add Exemption*** .

6.  For ***Collection ID*** , enter `  instruments  ` . For ***Field path*** , enter `  timestamp  ` .

7.  Under ***Query scope*** , select both ***Collection*** and ***Collection group*** .

8.  Click ***Next***

9.  Toggle all the index settings to ***Disabled*** . Click ***Save*** .

10. Repeat the same steps for the `  shard  ` field.

### Firebase CLI

1.  Add the following to the `  fieldOverrides  ` section of your index definitions file:
    
    ``` text
    {
     "fieldOverrides": [
       // Disable single-field indexing for the timestamp field
       {
         "collectionGroup": "instruments",
         "fieldPath": "timestamp",
         "indexes": []
       },
     ]
    }
    ```

2.  Deploy your updated index definitions:
    
    ``` text
    firebase deploy --only firestore:indexes
    ```

### Create new composite indexes

After removing all the previous indexes containing the `  timestamp  ` , define the new indexes that your app requires. Any index containing the `  timestamp  ` field must also contain the `  shard  ` field. For example, to support the queries above, add the following indexes:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>instruments</td>
<td>arrow_downward shard, arrow_upward price.currency, arrow_downward timestamp</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>instruments</td>
<td>arrow_downward shard, arrow_upward exchange, arrow_downward timestamp</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>instruments</td>
<td>arrow_downward shard, arrow_upward instrumentType, arrow_downward timestamp</td>
<td>Collection</td>
</tr>
</tbody>
</table>

### Error Messages

You can build these indexes by running the updated queries.

Each query returns an error message with a link to create the required index in the Firebase Console.

### Firebase CLI

1.  Add the following indexes to your index definition file:
    
    ``` text
     {
       "indexes": [
       // New indexes for sharded timestamps
         {
           "collectionGroup": "instruments",
           "queryScope": "COLLECTION",
           "fields": [
             {
               "fieldPath": "shard",
               "order": "DESCENDING"
             },
             {
               "fieldPath": "exchange",
               "order": "ASCENDING"
             },
             {
               "fieldPath": "timestamp",
               "order": "DESCENDING"
             }
           ]
         },
         {
           "collectionGroup": "instruments",
           "queryScope": "COLLECTION",
           "fields": [
             {
               "fieldPath": "shard",
               "order": "DESCENDING"
             },
             {
               "fieldPath": "instrumentType",
               "order": "ASCENDING"
             },
             {
               "fieldPath": "timestamp",
               "order": "DESCENDING"
             }
           ]
         },
         {
           "collectionGroup": "instruments",
           "queryScope": "COLLECTION",
           "fields": [
             {
               "fieldPath": "shard",
               "order": "DESCENDING"
             },
             {
               "fieldPath": "price.currency",
               "order": "ASCENDING"
             },
             {
               "fieldPath": "timestamp",
               "order": "DESCENDING"
             }
           ]
         },
       ]
     }
    ```

2.  Deploy your updated index definitions:
    
    ``` text
    firebase deploy --only firestore:indexes
    ```

## Understanding the write limit for sequential indexed fields

The limit on the write rate for sequential indexed fields comes from how Firestore stores index values and scales index writes. For each index write, Firestore defines a key-value entry which concatenates the document name and the value of each indexed field. Firestore organizes these index entries into groups of data called *tablets* . Each Firestore server holds one or more tablets. When the write load to a particular tablet becomes too high, Firestore scales horizontally by splitting the tablet into smaller tablets and spreading the new tablets across different Firestore servers.

Firestore places lexicographically close index entries on the same tablet. If the index values in a tablet are too close together, such as for timestamp fields, Firestore cannot efficiently split the tablet into smaller tablets. This creates a hot spot where a single tablet receives too much traffic, and read and write operations to the hot spot become slower.

By sharding a timestamp field, you make it possible for Firestore to efficiently split workloads across multiple tablets. Although the values of the timestamp field might remain close together, the concatenated shard and index value give Firestore enough space between index entries to split the entries among multiple tablets.

## What's next

  - Read the [best practices for designing for scale](../best-practices#designing_for_scale)
  - For cases with high write rates to a single document, see [Distrubted counters](../solutions/counters)
  - See the [standard limits for Firestore](../quotas#limits)
