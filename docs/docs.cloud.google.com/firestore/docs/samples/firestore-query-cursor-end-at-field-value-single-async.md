Query a Firestore collection with a cursor end at filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Paginate data with query cursors](https://docs.cloud.google.com/firestore/native/docs/query-data/query-cursors)
  - [Paginate data with query cursors](https://firebase.google.com/docs/firestore/query-data/query-cursors)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    query_end_at = cities_ref.order_by("population").end_at({"population": 1000000})

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
