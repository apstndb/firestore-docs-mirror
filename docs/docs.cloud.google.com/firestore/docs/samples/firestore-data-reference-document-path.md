Create a Firestore document reference from a document path

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Data model](https://docs.cloud.google.com/firestore/native/docs/data-model)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference documentRef = db.Document("users/alovelace");

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "cloud.google.com/go/firestore"
    )
    
    func createDocReferenceFromString(client *firestore.Client) {
     // Reference to a document with id "alovelace" in the collection "users"
     alovelaceRef := client.Doc("users/alovelace")
    
     _ = alovelaceRef
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // Reference to a document with id "alovelace" in the collection "users"
    DocumentReference document = db.document("users/alovelace");

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const alovelaceDocumentRef = db.doc('users/alovelace');

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $document = $db->document('users/alovelace');

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    a_lovelace_ref = db.document("users/alovelace")

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    document_path_ref = firestore.doc "users/alovelace"

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
