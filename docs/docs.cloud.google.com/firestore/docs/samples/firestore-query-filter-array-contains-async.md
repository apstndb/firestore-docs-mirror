Query a Firestore collection with an array\_contains filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    query = cities_ref.where(
        filter=FieldFilter("regions", "array_contains", "west_coast")
    )

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
