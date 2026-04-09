Delete a Firestore collection and documents within (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Delete data from Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/delete-data)
  - [Delete documents and fields](/firestore/native/docs/manage-data/delete-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
async def delete_collection(coll_ref):

    await db.recursive_delete(coll_ref)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
