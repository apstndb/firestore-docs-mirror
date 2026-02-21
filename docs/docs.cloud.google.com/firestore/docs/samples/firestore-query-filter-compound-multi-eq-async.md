Query a Firestore collection with multiple eq filters (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

denver_query = cities_ref.where(filter=FieldFilter("state", "==", "CO")).where(
    filter=FieldFilter("name", "==", "Denver")
)
large_us_cities_query = cities_ref.where(
    filter=FieldFilter("state", "==", "CA")
).where(filter=FieldFilter("population", ">", 1000000))
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
