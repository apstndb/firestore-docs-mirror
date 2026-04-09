Getting started with Firestore

## Code sample

### Kotlin

``` kotlin
// Create the client.
val db = FirestoreOptions.newBuilder()
    .build()
    .service

// Fetch the document reference and data object.
val docRef = db.collection(collectionName).document(documentName)
val data = docRef
    .get() // future
    .get() // snapshot
    .data ?: error("Document $collectionName:$documentName not found") // MutableMap

// Print the retrieved data.
data.forEach { (key, value) -> println("$key: $value") }
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const {Firestore} = require('@google-cloud/firestore');

// Create a new client
const firestore = new Firestore();

async function quickstart() {
  // Obtain a document reference.
  const document = firestore.doc('posts/intro-to-firestore');

  // Enter new data into the document.
  await document.set({
    title: 'Welcome to Firestore',
    body: 'Hello World',
  });
  console.log('Entered new data into the document');

  // Update an existing document.
  await document.update({
    body: 'My first Firestore app',
  });
  console.log('Updated an existing document');

  // Read the document.
  const doc = await document.get();
  console.log('Read the document');

  // Delete the document.
  await document.delete();
  console.log('Deleted the document');
}
quickstart();
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
