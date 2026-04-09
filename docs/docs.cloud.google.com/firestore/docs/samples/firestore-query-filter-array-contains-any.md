Query a Firestore collection with an array\_contains\_any filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereArrayContainsAny("Regions", new[] { "west_coast", "east_coast" });
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
cities := client.Collection("cities")
query := cities.Where("regions", "array-contains-any", []string{"west_coast", "east_coast"}).Documents(ctx)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
CollectionReference citiesRef = db.collection("cities");

Query query =
    citiesRef.whereArrayContainsAny("regions", Arrays.asList("west_coast", "east_coast"));
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const coastalCities = await citiesRef.where('regions', 'array-contains-any',
    ['west_coast', 'east_coast']).get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$containsQuery = $citiesRef->where('regions', 'array-contains-any', ['west_coast', 'east_coast']);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(
    filter=FieldFilter(
        "regions", "array_contains_any", ["west_coast", "east_coast"]
    )
)
return query
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path
costal_cities = cities_ref.where "regions", "array-contains-any", ["west_coast", "east_coast"]
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
