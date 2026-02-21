Querying Firestore collections with one range

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query stateQuery = citiesRef.WhereEqualTo("State", "CA");
Query populationQuery = citiesRef.WhereGreaterThan("Population", 1000000);
Query nameQuery = citiesRef.WhereGreaterThanOrEqualTo("Name", "San Francisco");
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
countryQuery := cities.Where("state", "==", "CA")
popQuery := cities.Where("population", "<", 1000000)
cityQuery := cities.Where("name", ">=", "San Francisco")
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query stateQuery = cities.whereEqualTo("state", "CA");
Query populationQuery = cities.whereLessThan("population", 1000000L);
Query nameQuery = cities.whereGreaterThanOrEqualTo("name", "San Francisco");
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const stateQueryRes = await citiesRef.where('state', '==', 'CA').get();
const populationQueryRes = await citiesRef.where('population', '<', 1000000).get();
const nameQueryRes = await citiesRef.where('name', '>=', 'San Francisco').get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$stateQuery = $citiesRef->where('state', '=', 'CA');
$populationQuery = $citiesRef->where('population', '>', 1000000);
$nameQuery = $citiesRef->where('name', '>=', 'San Francisco');
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

cities_ref.where(filter=FieldFilter("state", "==", "CA"))
cities_ref.where(filter=FieldFilter("population", "<", 1000000))
cities_ref.where(filter=FieldFilter("name", ">=", "San Francisco"))
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
state_query      = cities_ref.where "state", "=", "CA"
population_query = cities_ref.where "population", ">", 1_000_000
name_query       = cities_ref.where "name", ">=", "San Francisco"
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
