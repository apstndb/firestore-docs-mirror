Create a Firestore subcollection reference

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Cloud Firestore Data model](https://firebase.google.com/docs/firestore/data-model)
  - [Data model](https://docs.cloud.google.com/firestore/native/docs/data-model)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference documentRef = db
        .Collection("Rooms").Document("RoomA")
        .Collection("Messages").Document("Message1");

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "cloud.google.com/go/firestore"
    )
    
    func createSubcollectionReference(client *firestore.Client) {
     messageRef := client.Collection("rooms").Doc("roomA").
         Collection("messages").Doc("message1")
    
     _ = messageRef
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // Reference to a document in subcollection "messages"
    DocumentReference document =
        db.collection("rooms").document("roomA").collection("messages").document("message1");

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const messageRef = db.collection('rooms').doc('roomA')
      .collection('messages').doc('message1');

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $document = $db
        ->collection('rooms')
        ->document('roomA')
        ->collection('messages')
        ->document('message1');

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    room_a_ref = db.collection("rooms").document("roomA")
    message_ref = room_a_ref.collection("messages").document("message1")

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    message_ref = firestore.col("rooms").doc("roomA").col("messages").doc("message1")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
