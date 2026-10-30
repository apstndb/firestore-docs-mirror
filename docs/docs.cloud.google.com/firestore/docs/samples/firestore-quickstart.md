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

```kotlin
import com.google.api.gax.rpc.ApiException
import com.google.api.gax.rpc.NotFoundException
import com.google.cloud.firestore.FirestoreOptions
import java.util.concurrent.ExecutionException

/**
 * Retrieves all documents from a Firestore collection and prints their metadata
 * and fields.
 *
 * @param projectId Google Cloud project identifier (for example, "example-project-id").
 * @param collectionId Firestore collection identifier to query (for example, "example-collection").
 */
fun getCollectionDocuments(projectId: String, collectionId: String) {
  val options =
    FirestoreOptions.getDefaultInstance()
      .toBuilder()
      .setProjectId(projectId)
      .build()

  try {
    options.service.use { firestore ->
      val collectionReference = firestore.collection(collectionId)
      println("Retrieving documents from collection '$collectionId'...")
      val querySnapshot = collectionReference.get().get()

      println("Resource ID: ${collectionReference.path}")
      println("Document Count: ${querySnapshot.documents.size}")
      println("Read Time: ${querySnapshot.readTime}")
      for (document in querySnapshot.documents) {
        println("Document ID: ${document.id}")
        println("Creation Date: ${document.createTime}")
        println("Data: ${document.data}")
        println("Update Time: ${document.updateTime}")
      }
    }
  } catch (err: ExecutionException) {
    val message =
      when (val cause = err.cause) {
        is NotFoundException ->
          "error: Firestore database not found in project '$projectId': ${cause.message}"
        is ApiException ->
          "error: failed to retrieve collection '$collectionId' in project '$projectId': ${cause.message}"
        else ->
          "error: execution failed while querying collection '$collectionId' in project '$projectId': ${err.message}"
      }
    System.err.println(message)
  } catch (err: InterruptedException) {
    Thread.currentThread().interrupt()
    System.err.println(
      "error: interrupted while querying collection '$collectionId' in project '$projectId': ${err.message}"
    )
  }
}
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
