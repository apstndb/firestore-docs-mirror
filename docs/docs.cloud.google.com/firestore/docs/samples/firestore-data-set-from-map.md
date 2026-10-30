---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-data-set-from-map
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-data-set-from-map
title: Add a Firestore document using a map
description: Add a Firestore document using a map
data_source: docs.cloud.google.com
---

Add a Firestore document using a map

## Explore further

For detailed documentation that includes this code sample, see the following:

- [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### C#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```csharp
DocumentReference docRef = db.Collection("cities").Document("LA");
Dictionary<string, object> city = new Dictionary<string, object>
{
    { "name", "Los Angeles" },
    { "state", "CA" },
    { "country", "USA" }
};
await docRef.SetAsync(city);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```go
import (
    "context"
    "log"

    "cloud.google.com/go/firestore"
)

func addDocAsMap(ctx context.Context, client *firestore.Client) error {
    _, err := client.Collection("cities").Doc("LA").Set(ctx, map[string]interface{}{
        "name":    "Los Angeles",
        "state":   "CA",
        "country": "USA",
    })
    if err != nil {
        // Handle any errors in an appropriate way, such as returning them.
        log.Printf("An error has occurred: %s", err)
    }

    return err
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```java
// Create a Map to store the data we want to set
Map<String, Object> docData = new HashMap<>();
docData.put("name", "Los Angeles");
docData.put("state", "CA");
docData.put("country", "USA");
docData.put("regions", Arrays.asList("west_coast", "socal"));
// Add a new document (asynchronously) in collection "cities" with id "LA"
ApiFuture<WriteResult> future = db.collection("cities").document("LA").set(docData);
// ...
// future.get() blocks on response
System.out.println("Update time : " + future.get().getUpdateTime());
```

### Kotlin

```kotlin
import com.google.api.gax.rpc.ApiException
import com.google.api.gax.rpc.NotFoundException
import com.google.cloud.firestore.FirestoreOptions
import java.util.concurrent.ExecutionException

/**
 * Writes a document with structured fields into a Firestore collection. Setting
 * a document creates the record if it does not exist or overwrites its fields.
 *
 * @param projectId Google Cloud project identifier (for example, "example-project-id").
 * @param collectionId Target Firestore collection identifier (for example, "cities").
 * @param documentId Target Firestore document identifier (for example, "LA").
 */
fun setDocument(projectId: String, collectionId: String, documentId: String) {
  val options =
    FirestoreOptions.getDefaultInstance()
      .toBuilder()
      .setProjectId(projectId)
      .build()

  val documentData =
    mapOf(
      "name" to "Los Angeles",
      "state" to "CA",
      "country" to "USA",
    )

  try {
    options.service.use { firestore ->
      val documentReference =
        firestore.collection(collectionId).document(documentId)
      println("Writing document '$documentId' in collection '$collectionId'...")
      val writeResult = documentReference.set(documentData).get()

      println("Resource ID: ${documentReference.path}")
      println("Collection ID: $collectionId")
      println("Document ID: $documentId")
      println("Update Time: ${writeResult.updateTime}")
    }
  } catch (err: ExecutionException) {
    val message =
      when (val cause = err.cause) {
        is NotFoundException ->
          "error: Firestore database not found in project '$projectId': ${cause.message}"
        is ApiException ->
          "error: failed to write document '$documentId' in collection '$collectionId' for project '$projectId': ${cause.message}"
        else ->
          "error: execution failed while writing document '$documentId' in collection '$collectionId' for project '$projectId': ${err.message}"
      }
    System.err.println(message)
  } catch (err: InterruptedException) {
    Thread.currentThread().interrupt()
    System.err.println(
      "error: interrupted while writing document '$documentId' in collection '$collectionId' for project '$projectId': ${err.message}"
    )
  }
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```javascript
const data = {
  name: 'Los Angeles',
  state: 'CA',
  country: 'USA'
};

// Add a new document in collection "cities" with ID 'LA'
const res = await db.collection('cities').doc('LA').set(data);
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```php
$data = [
    'name' => 'Los Angeles',
    'state' => 'CA',
    'country' => 'USA'
];
$db->collection('samples/php/cities')->document('LA')->set($data);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```python
data = {"name": "Los Angeles", "state": "CA", "country": "USA"}

# Add a new doc in collection 'cities' with ID 'LA'
db.collection("cities").document("LA").set(data)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```ruby
city_ref = firestore.doc "#{collection_path}/LA"

data = {
  name:    "Los Angeles",
  state:   "CA",
  country: "USA"
}

city_ref.set data
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
