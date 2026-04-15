Query a Firestore collection with an array\_contains filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.Collection("cities");
    Query query = citiesRef.WhereArrayContains("Regions", "west_coast");

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    query := cities.Where("regions", "array-contains", "west_coast").Documents(ctx)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.collection("cities");
    Query westCoastQuery = citiesRef.whereArrayContains("regions", "west_coast");

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const westCoastCities = citiesRef.where('regions', 'array-contains',
      'west_coast').get();

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $containsQuery = $citiesRef->where('regions', 'array-contains', 'west_coast');

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(
        filter=FieldFilter("regions", "array_contains", "west_coast")
    )

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = firestore.col collection_path
    cities = cities_ref.where "regions", "array-contains", "west_coast"

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
