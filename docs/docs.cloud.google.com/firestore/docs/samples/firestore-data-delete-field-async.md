Delete a Firestore field (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Delete data from Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/delete-data)
  - [Delete documents and fields](https://docs.cloud.google.com/firestore/native/docs/manage-data/delete-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    city_ref = db.collection("cities").document("BJ")
    await city_ref.update({"capital": firestore.DELETE_FIELD})

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
