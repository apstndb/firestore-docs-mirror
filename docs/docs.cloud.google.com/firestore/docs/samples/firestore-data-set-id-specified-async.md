Add a Firestore document (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    await db.collection("cities").document("new-city-id").set(data)

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
