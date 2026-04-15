Query a Firestore collection with an in filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.Collection("cities");
    Query query = citiesRef.WhereIn("Country", new[] { "USA", "Japan" });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities := client.Collection("cities")
    query := cities.Where("country", "in", []string{"USA", "Japan"}).Documents(ctx)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.collection("cities");
    
    Query query = citiesRef.whereIn("country", Arrays.asList("USA", "Japan"));

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const usaOrJapan = await citiesRef.where('country', 'in', ['USA', 'Japan']).get();

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $rangeQuery = $citiesRef->where('country', 'in', ['USA', 'Japan']);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(filter=FieldFilter("country", "in", ["USA", "Japan"]))
    return query

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = firestore.col collection_path
    usr_or_japan = cities_ref.where "country", "in", ["USA", "Japan"]

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
