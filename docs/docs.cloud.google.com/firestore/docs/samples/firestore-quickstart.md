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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
