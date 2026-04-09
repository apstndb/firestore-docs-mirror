Query a Firestore collection with a cursor start at document filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
DocumentReference docRef = citiesRef.Document("SF");
DocumentSnapshot snapshot = await docRef.GetSnapshotAsync();
Query query = citiesRef.OrderBy("Population").StartAt(snapshot);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
cities := client.Collection("cities")
dsnap, err := cities.Doc("SF").Get(ctx)
if err != nil {
 fmt.Println(err)
}
query := cities.OrderBy("population", firestore.Asc).StartAt(dsnap.Data()["population"]).Documents(ctx)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Fetch the snapshot with an API call, waiting for a maximum of 30 seconds for a result.
ApiFuture<DocumentSnapshot> future = db.collection("cities").document("SF").get();
DocumentSnapshot snapshot = future.get(30, TimeUnit.SECONDS);

// Construct the query
Query query = db.collection("cities").orderBy("population").startAt(snapshot);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const docRef = db.collection('cities').doc('SF');
const snapshot = await docRef.get();
const startAtSnapshot = db.collection('cities')
  .orderBy('population')
  .startAt(snapshot);

await startAtSnapshot.limit(10).get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$docRef = $citiesRef->document('SF');
$snapshot = $docRef->snapshot();

$query = $citiesRef
    ->orderBy('population')
    ->startAt($snapshot);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
doc_ref = db.collection("cities").document("SF")

snapshot = doc_ref.get()
start_at_snapshot = (
    db.collection("cities").order_by("population").start_at(snapshot)
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
doc_ref = firestore.doc "#{collection_path}/SF"
snapshot = doc_ref.get
query = cities_ref.order("population").start_at(snapshot)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
