An example of an invalid order and limit Firestore query

## Code sample

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// Note: This is an invalid query. It violates the constraint that range
// and order by are required to be on the same field.
query := cities.Where("population", ">", 2500000).OrderBy("country", firestore.Asc)
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query query = cities.whereGreaterThan("population", 2500000L).orderBy("country");
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
citiesRef.where('population', '>', 2500000).orderBy('country');
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
query = cities_ref.where(filter=FieldFilter("population", ">", 2500000)).order_by(
    "country"
)
results = query.stream()
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = cities_ref.where("population", ">", 2_500_000).order("country")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
