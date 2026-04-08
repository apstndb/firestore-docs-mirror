Query a Firestore collection with a string eq filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create a reference to the cities collection
cities_ref = db.collection("cities")

# Create a query against the collection
query_ref = cities_ref.where(filter=FieldFilter("state", "==", "CA"))
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
