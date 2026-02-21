Query a Firestore collection with a boolean eq filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("Capital", true);
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    Console.WriteLine("Document {0} returned by query Capital=true", documentSnapshot.Id);
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := client.Collection("cities").Where("capital", "==", true)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Create a reference to the cities collection
CollectionReference cities = db.collection("cities");
// Create a query against the collection.
Query query = cities.whereEqualTo("capital", true);
// retrieve  query results asynchronously using query.get()
ApiFuture<QuerySnapshot> querySnapshot = query.get();

for (DocumentSnapshot document : querySnapshot.get().getDocuments()) {
  System.out.println(document.getId());
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Create a reference to the cities collection
const citiesRef = db.collection('cities');

// Create a query against the collection
const allCapitalsRes = citiesRef.where('capital', '==', true);
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('capital', '=', true);
$snapshot = $query->documents();
foreach ($snapshot as $document) {
    printf('Document %s returned by query capital=true' . PHP_EOL, $document->id());
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("capital", "==", True))
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "capital", "=", true

query.get do |city|
  puts "Document #{city.document_id} returned by query capital=true."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
