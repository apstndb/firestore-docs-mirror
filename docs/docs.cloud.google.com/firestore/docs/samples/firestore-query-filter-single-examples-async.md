Querying Firestore collections with one range (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
cities_ref = db.collection("cities")

cities_ref.where(filter=FieldFilter("state", "==", "CA"))
cities_ref.where(filter=FieldFilter("population", "<", 1000000))
cities_ref.where(filter=FieldFilter("name", ">=", "San Francisco"))
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
