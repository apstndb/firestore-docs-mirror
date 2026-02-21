Query a Firestore collection group with an eq filter (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
museums = db.collection_group("landmarks").where(
    filter=FieldFilter("type", "==", "museum")
)
docs = museums.stream()
async for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
