Query a Firestore collection with multiple eq filters (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    cities_ref = db.collection("cities")
    
    denver_query = cities_ref.where(filter=FieldFilter("state", "==", "CO")).where(
        filter=FieldFilter("name", "==", "Denver")
    )
    large_us_cities_query = cities_ref.where(
        filter=FieldFilter("state", "==", "CA")
    ).where(filter=FieldFilter("population", ">", 1000000))

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
