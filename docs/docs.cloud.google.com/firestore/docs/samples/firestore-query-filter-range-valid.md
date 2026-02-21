Use two ranges for a Firestore query

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query rangeQuery = citiesRef
    .WhereGreaterThanOrEqualTo("State", "CA")
    .WhereLessThanOrEqualTo("State", "IN");
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
stateQuery := cities.Where("state", ">=", "CA").Where("state", "<", "IN")
populationQuery := cities.Where("state", "==", "CA").Where("population", ">", 1000000)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query validQuery1 =
    cities.whereGreaterThanOrEqualTo("state", "CA").whereLessThanOrEqualTo("state", "IN");
Query validQuery2 = cities.whereEqualTo("state", "CA").whereGreaterThan("population", 1000000);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
citiesRef.where('state', '>=', 'CA').where('state', '<=', 'IN');
citiesRef.where('state', '==', 'CA').where('population', '>', 1000000);
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$rangeQuery = $citiesRef
    ->where('state', '>=', 'CA')
    ->where('state', '<=', 'IN');
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
cities_ref.where(filter=FieldFilter("state", ">=", "CA")).where(
    filter=FieldFilter("state", "<=", "IN")
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
range_query = cities_ref.where("state", ">=", "CA").where("state", "<=", "IN")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
