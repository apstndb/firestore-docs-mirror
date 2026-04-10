Retrieve Firestore Document as Map (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = db.collection("cities").document("SF")
    
    doc = await doc_ref.get()
    if doc.exists:
        print(f"Document data: {doc.to_dict()}")
    else:
        print("No such document!")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
