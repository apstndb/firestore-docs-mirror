---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-data-get-all-documents
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-data-get-all-documents
title: Get all documents
description: Get all documents within a Firestore Collection
data_source: docs.cloud.google.com
---

Get all documents within a Firestore Collection

## Explore further

For detailed documentation that includes this code sample, see the following:

- [Getting data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)

## Code sample

### C#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```csharp
Query allCitiesQuery = db.Collection("cities");
QuerySnapshot allCitiesQuerySnapshot = await allCitiesQuery.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in allCitiesQuerySnapshot.Documents)
{
    Console.WriteLine("Document data for {0} document:", documentSnapshot.Id);
    Dictionary<string, object> city = documentSnapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city)
    {
        Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
    }
    Console.WriteLine("");
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```go
import (
    "context"
    "fmt"

    "cloud.google.com/go/firestore"
    "google.golang.org/api/iterator"
)

func allDocs(ctx context.Context, client *firestore.Client) error {
    fmt.Println("All cities:")
    iter := client.Collection("cities").Documents(ctx)
    defer iter.Stop()
    for {
        doc, err := iter.Next()
        if err == iterator.Done {
            break
        }
        if err != nil {
            return err
        }
        fmt.Println(doc.Data())
    }
    return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```java
// asynchronously retrieve all documents
ApiFuture<QuerySnapshot> future = db.collection("cities").get();
// future.get() blocks on response
List<QueryDocumentSnapshot> documents = future.get().getDocuments();
for (QueryDocumentSnapshot document : documents) {
  System.out.println(document.getId() + " => " + document.toObject(City.class));
}
```

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

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```javascript
const citiesRef = db.collection('cities');
const snapshot = await citiesRef.get();
snapshot.forEach(doc => {
  console.log(doc.id, '=>', doc.data());
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```php
$citiesRef = $db->collection('samples/php/cities');
$documents = $citiesRef->documents();
foreach ($documents as $document) {
    if ($document->exists()) {
        printf('Document data for document %s:' . PHP_EOL, $document->id());
        print_r($document->data());
        printf(PHP_EOL);
    } else {
        printf('Document %s does not exist!' . PHP_EOL, $document->id());
    }
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```python
docs = db.collection("cities").stream()

for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```ruby
cities_ref = firestore.col collection_path
cities_ref.get do |city|
  puts "#{city.document_id} data: #{city.data}."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
