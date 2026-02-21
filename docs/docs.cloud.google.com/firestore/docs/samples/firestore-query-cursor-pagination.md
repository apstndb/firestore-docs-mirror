Use start cursors and limits to paginate Firestore collections

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query firstQuery = citiesRef.OrderBy("Population").Limit(3);

// Get the last document from the results
QuerySnapshot querySnapshot = await firstQuery.GetSnapshotAsync();
long lastPopulation = 0;
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    lastPopulation = documentSnapshot.GetValue<long>("Population");
}

// Construct a new query starting at this document.
// Note: this will not have the desired effect if multiple cities have the exact same population value
Query secondQuery = citiesRef.OrderBy("Population").StartAfter(lastPopulation);
QuerySnapshot secondQuerySnapshot = await secondQuery.GetSnapshotAsync();
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
cities := client.Collection("cities")

// Get the first 25 cities, ordered by population.
firstPage := cities.OrderBy("population", firestore.Asc).Limit(25).Documents(ctx)
docs, err := firstPage.GetAll()
if err != nil {
 return err
}

// Get the last document.
lastDoc := docs[len(docs)-1]

// Construct a new query to get the next 25 cities.
secondPage := cities.OrderBy("population", firestore.Asc).
 StartAfter(lastDoc.Data()["population"]).
 Limit(25)

// ...
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Construct query for first 25 cities, ordered by population.
CollectionReference cities = db.collection("cities");
Query firstPage = cities.orderBy("population").limit(25);

// Wait for the results of the API call, waiting for a maximum of 30 seconds for a result.
ApiFuture<QuerySnapshot> future = firstPage.get();
List<QueryDocumentSnapshot> docs = future.get(30, TimeUnit.SECONDS).getDocuments();

// Construct query for the next 25 cities.
QueryDocumentSnapshot lastDoc = docs.get(docs.size() - 1);
Query secondPage = cities.orderBy("population").startAfter(lastDoc).limit(25);

future = secondPage.get();
docs = future.get(30, TimeUnit.SECONDS).getDocuments();
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const first = db.collection('cities')
  .orderBy('population')
  .limit(3);

const snapshot = await first.get();

// Get the last document
const last = snapshot.docs[snapshot.docs.length - 1];

// Construct a new query starting at this document.
// Note: this will not have the desired effect if multiple
// cities have the exact same population value.
const next = db.collection('cities')
  .orderBy('population')
  .startAfter(last.data().population)
  .limit(3);

// Use the query for pagination
// ...
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$firstQuery = $citiesRef->orderBy('population')->limit(3);

# Get the last document from the results
$documents = $firstQuery->documents();
$lastPopulation = 0;
foreach ($documents as $document) {
    $lastPopulation = $document['population'];
}

# Construct a new query starting at this document
# Note: this will not have the desired effect if multiple cities have the exact same population value
$nextQuery = $citiesRef->orderBy('population')->startAfter([$lastPopulation]);
$snapshot = $nextQuery->documents();
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
first_query = cities_ref.order_by("population").limit(3)

# Get the last document from the results
docs = first_query.stream()
last_doc = list(docs)[-1]

# Construct a new query starting at this document
# Note: this will not have the desired effect if
# multiple cities have the exact same population value
last_pop = last_doc.to_dict()["population"]

next_query = (
    cities_ref.order_by("population").start_after({"population": last_pop}).limit(3)
)
# Use the query for pagination
# ...
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref  = firestore.col collection_path
first_query = cities_ref.order("population").limit(3)

# Get the last document from the results.
last_population = 0
first_query.get do |city|
  last_population = city.data[:population]
end

# Construct a new query starting at this document.
# Note: this will not have the desired effect if multiple cities have the exact same population value.
second_query = cities_ref.order("population").start_after(last_population)
second_query.get do |city|
  puts "Document #{city.document_id} returned by paginated query cursor."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
