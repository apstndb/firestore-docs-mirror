Create a Firestore document reference

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Cloud Firestore Data model](https://firebase.google.com/docs/firestore/data-model)
  - [Data model](https://docs.cloud.google.com/firestore/native/docs/data-model)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference documentRef = db.Collection("users").Document("alovelace");

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "cloud.google.com/go/firestore"
    )
    
    func createDocReference(client *firestore.Client) {
    
     alovelaceRef := client.Collection("users").Doc("alovelace")
    
     _ = alovelaceRef
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // Reference to a document with id "alovelace" in the collection "users"
    DocumentReference document = db.collection("users").document("alovelace");

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const alovelaceDocumentRef = db.collection('users').doc('alovelace');

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $document = $db->collection('samples/php/users')->document('alovelace');

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    a_lovelace_ref = db.collection("users").document("alovelace")

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    document_ref = firestore.col("users").doc("alovelace")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
