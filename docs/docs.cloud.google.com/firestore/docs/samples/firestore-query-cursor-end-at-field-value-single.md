Query a Firestore collection with a cursor end at filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = citiesRef.OrderBy("Population").EndAt(1000000);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := client.Collection("cities").OrderBy("population", firestore.Asc).EndAt(1000000)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query query = cities.orderBy("population").endAt(4921000L);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const endAtRes = await db.collection('cities')
  .orderBy('population')
  .endAt(1000000)
  .get();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef
    ->orderBy('population')
    ->endAt([1000000]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
query_end_at = cities_ref.order_by("population").end_at({"population": 1000000})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = cities_ref.order("population").end_at(1_000_000)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
