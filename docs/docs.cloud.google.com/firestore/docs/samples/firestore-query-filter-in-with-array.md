Query a Firestore collection with an in array filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.Collection("cities");
    Query query = citiesRef.WhereIn("Regions",
        new[] { new[] { "west_coast" }, new[] { "east_coast" } });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities := client.Collection("cities")
    query := cities.Where("regions", "in", [][]string{{"west_coast"}, {"east_coast"}}).Documents(ctx)

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference citiesRef = db.collection("cities");
    
    Query query =
        citiesRef.whereIn(
            "regions", Arrays.asList(Arrays.asList("west_coast"), Arrays.asList("east_coast")));

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const exactlyOneCoast = await citiesRef.where('regions', 'in',
        [['west_coast', 'east_coast']]).get();

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $rangeQuery = $citiesRef->where('regions', 'in', [['west_coast'], ['east_coast']]);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(
        filter=FieldFilter("regions", "in", [["west_coast"], ["east_coast"]])
    )
    return query

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = firestore.col collection_path
    exactly_one_cost = cities_ref.where "regions", "in", [["west_coast"], ["east_coast"]]

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
