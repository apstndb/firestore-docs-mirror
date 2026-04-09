Add data to Firestore (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Create a Firestore database by using a server client library](/firestore/native/docs/create-database-server-client-library)
  - [Get started with Cloud Firestore](https://firebase.google.com/docs/firestore/quickstart)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
doc_ref = db.collection("users").document("alovelace")
await doc_ref.set({"first": "Ada", "last": "Lovelace", "born": 1815})
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
