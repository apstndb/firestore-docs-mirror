An example Firestore query with an invalid range

## Code sample

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := cities.Where("state", ">=", "CA").Where("population", ">", 1000000)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query invalidRangeQuery =
    cities.whereGreaterThanOrEqualTo("state", "CA").whereGreaterThan("population", 100000);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
citiesRef.where('state', '>=', 'CA').where('population', '>', 1000000);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
cities_ref.where(filter=FieldFilter("state", ">=", "CA")).where(
    filter=FieldFilter("population", ">=", 1000000)
)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
invalid_range_query = cities_ref.where("state", ">=", "CA").where("population", ">", 1_000_000)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
