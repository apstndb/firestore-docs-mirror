Query a Firestore collection with an array\_contains\_any filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.Collection("cities");
    Query query = citiesRef.WhereArrayContainsAny("Regions", new[] { "west_coast", "east_coast" });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities := client.Collection("cities")
    query := cities.Where("regions", "array-contains-any", []string{"west_coast", "east_coast"}).Documents(ctx)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.collection("cities");
    
    Query query =
        citiesRef.whereArrayContainsAny("regions", Arrays.asList("west_coast", "east_coast"));

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const coastalCities = await citiesRef.where('regions', 'array-contains-any',
        ['west_coast', 'east_coast']).get();

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $containsQuery = $citiesRef->where('regions', 'array-contains-any', ['west_coast', 'east_coast']);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(
        filter=FieldFilter(
            "regions", "array_contains_any", ["west_coast", "east_coast"]
        )
    )
    return query

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = firestore.col collection_path
    costal_cities = cities_ref.where "regions", "array-contains-any", ["west_coast", "east_coast"]

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
