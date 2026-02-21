Query a Firestore collection with a string eq filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereEqualTo("State", "CA");
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    Console.WriteLine("Document {0} returned by query State=CA", documentSnapshot.Id);
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := client.Collection("cities").Where("state", "==", "CA")
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Create a reference to the cities collection
CollectionReference cities = db.collection("cities");
// Create a query against the collection.
Query query = cities.whereEqualTo("state", "CA");
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
const queryRef = citiesRef.where('state', '==', 'CA');
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('state', '=', 'CA');
$snapshot = $query->documents();
foreach ($snapshot as $document) {
    printf('Document %s returned by query state=CA' . PHP_EOL, $document->id());
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create a reference to the cities collection
cities_ref = db.collection("cities")

# Create a query against the collection
query_ref = cities_ref.where(filter=FieldFilter("state", "==", "CA"))
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "state", "=", "CA"

query.get do |city|
  puts "Document #{city.document_id} returned by query state=CA."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
