Create a Firestore subcollection reference (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Data model](https://docs.cloud.google.com/firestore/native/docs/data-model)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    room_a_ref = db.collection("rooms").document("roomA")
    message_ref = room_a_ref.collection("messages").document("message1")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
