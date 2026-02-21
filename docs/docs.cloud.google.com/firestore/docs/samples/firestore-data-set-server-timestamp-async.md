Update a Firestore document Timestamp (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("objects").document("some-id")
await city_ref.update({"timestamp": firestore.SERVER_TIMESTAMP})
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
