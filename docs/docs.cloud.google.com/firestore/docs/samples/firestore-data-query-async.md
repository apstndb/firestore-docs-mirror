Query a Firestore collection (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)
  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Note: Use of CollectionRef stream() is prefered to get()
docs = (
    db.collection("cities")
    .where(filter=FieldFilter("capital", "==", True))
    .stream()
)

async for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
