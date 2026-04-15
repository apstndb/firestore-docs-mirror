Delete a Firestore collection and documents within (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Delete documents and fields](https://docs.cloud.google.com/firestore/native/docs/manage-data/delete-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    async def delete_collection(coll_ref):
    
        await db.recursive_delete(coll_ref)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
