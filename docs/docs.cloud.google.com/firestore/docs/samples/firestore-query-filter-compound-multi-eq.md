Query a Firestore collection with multiple eq filters

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.Collection("cities");
    Query chainedQuery = citiesRef
        .WhereEqualTo("State", "CA")
        .WhereEqualTo("Name", "San Francisco");

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    denverQuery := cities.Where("name", "==", "Denver").Where("state", "==", "CO")
    caliQuery := cities.Where("state", "==", "CA").Where("population", "<=", 1000000)
    query := cities.Where("country", "==", "USA").Where("population", ">", 5000000)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query chainedQuery1 = cities.whereEqualTo("state", "CO").whereEqualTo("name", "Denver");

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    citiesRef.where('state', '==', 'CO').where('name', '==', 'Denver');
    citiesRef.where('state', '==', 'CA').where('population', '<', 1000000);

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $chainedQuery = $citiesRef
        ->where('state', '=', 'CA')
        ->where('name', '=', 'San Francisco');

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    denver_query = cities_ref.where(filter=FieldFilter("state", "==", "CO")).where(
        filter=FieldFilter("name", "==", "Denver")
    )
    large_us_cities_query = cities_ref.where(
        filter=FieldFilter("state", "==", "CA")
    ).where(filter=FieldFilter("population", ">", 1000000))

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    chained_query = cities_ref.where("state", "=", "CA").where("name", "=", "San Francisco")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
