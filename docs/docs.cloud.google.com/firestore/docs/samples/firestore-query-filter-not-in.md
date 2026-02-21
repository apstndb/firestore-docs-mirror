Query a Firestore collection with a not in filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
CollectionReference citiesRef = db.collection("cities");

Query query = citiesRef.whereNotIn("country", Arrays.asList("USA", "Japan"));
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const notUsaOrJapan = await citiesRef.where('country', 'not-in', ['USA', 'Japan']).get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$stateQuery = $citiesRef->where(
    'country',
    \Google\Cloud\Firestore\V1\StructuredQuery\FieldFilter\Operator::NOT_IN,
    ['USA', 'Japan']
);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

query = cities_ref.where(filter=FieldFilter("country", "not-in", ["USA", "Japan"]))
return query
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path
usr_or_japan = cities_ref.where "country", "not_in", ["USA", "Japan"]
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
