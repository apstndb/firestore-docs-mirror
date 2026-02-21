Ordering and limiting Firestore queries in descending order (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Order and limit data](/firestore/native/docs/query-data/order-limit-data)
  - [Order and limit data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/order-limit-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
results = query.stream()
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
