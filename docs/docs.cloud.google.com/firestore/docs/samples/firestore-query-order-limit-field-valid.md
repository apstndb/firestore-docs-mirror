Ordering and limiting Firestore queries with a filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Order and limit data](/firestore/native/docs/query-data/order-limit-data)
  - [Order and limit data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/order-limit-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = citiesRef
    .WhereGreaterThan("Population", 2500000)
    .OrderBy("Population")
    .Limit(2);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := cities.Where("population", ">", 2500000).OrderBy("population", firestore.Desc).Limit(2)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query query = cities.whereGreaterThan("population", 2500000L).orderBy("population").limit(2);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const biggestRes = await citiesRef.where('population', '>', 2500000)
  .orderBy('population').limit(2).get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef
    ->where('population', '>', 2500000)
    ->orderBy('population')
    ->limit(2);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
query = (
    cities_ref.where(filter=FieldFilter("population", ">", 2500000))
    .order_by("population")
    .limit(2)
)
results = query.stream()
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = cities_ref.where("population", ">", 2_500_000).order("population").limit(2)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
