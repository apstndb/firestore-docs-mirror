An example of an invalid order and limit Firestore query (async).

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")
query = cities_ref.where(filter=FieldFilter("population", ">", 2500000)).order_by(
    "country"
)
results = query.stream()
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
