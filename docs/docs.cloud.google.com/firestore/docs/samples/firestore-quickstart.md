---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-quickstart
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-quickstart
title: Getting started with Firestore
description: Getting started with Firestore
data_source: docs.cloud.google.com
---

Getting started with Firestore

## Code sample

### Kotlin

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
