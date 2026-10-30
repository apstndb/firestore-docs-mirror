---
name: documents/docs.cloud.google.com/firestore/docs/samples/firestore-setup-dataset-read
uri: https://docs.cloud.google.com/firestore/docs/samples/firestore-setup-dataset-read
title: Getting Firestore documents from a collection
description: Getting Firestore documents from a collection
data_source: docs.cloud.google.com
---

Getting Firestore documents from a collection

## Explore further

For detailed documentation that includes this code sample, see the following:

- [Quickstart: Create a Firestore database by using a server client library](https://docs.cloud.google.com/firestore/native/docs/create-database-server-client-library)

## Code sample

### C#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```csharp
CollectionReference usersRef = db.Collection("users");
QuerySnapshot snapshot = await usersRef.GetSnapshotAsync();
foreach (DocumentSnapshot document in snapshot.Documents)
{
    Console.WriteLine("User: {0}", document.Id);
    Dictionary<string, object> documentDictionary = document.ToDictionary();
    Console.WriteLine("First: {0}", documentDictionary["First"]);
    if (documentDictionary.ContainsKey("Middle"))
    {
        Console.WriteLine("Middle: {0}", documentDictionary["Middle"]);
    }
    Console.WriteLine("Last: {0}", documentDictionary["Last"]);
    Console.WriteLine("Born: {0}", documentDictionary["Born"]);
    Console.WriteLine();
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```go
iter := client.Collection("users").Documents(ctx)
for {
    doc, err := iter.Next()
    if err == iterator.Done {
        break
    }
    if err != nil {
        log.Fatalf("Failed to iterate: %v", err)
    }
    fmt.Println(doc.Data())
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```java
// asynchronously retrieve all users
ApiFuture<QuerySnapshot> query = db.collection("users").get();
// ...
// query.get() blocks on response
QuerySnapshot querySnapshot = query.get();
List<QueryDocumentSnapshot> documents = querySnapshot.getDocuments();
for (QueryDocumentSnapshot document : documents) {
  System.out.println("User: " + document.getId());
  System.out.println("First: " + document.getString("first"));
  if (document.contains("middle")) {
    System.out.println("Middle: " + document.getString("middle"));
  }
  System.out.println("Last: " + document.getString("last"));
  System.out.println("Born: " + document.getLong("born"));
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
const snapshot = await db.collection('users').get();
snapshot.forEach((doc) => {
  console.log(doc.id, '=>', doc.data());
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```php
$usersRef = $db->collection('samples/php/users');
$snapshot = $usersRef->documents();
foreach ($snapshot as $user) {
    printf('User: %s' . PHP_EOL, $user->id());
    printf('First: %s' . PHP_EOL, $user['first']);
    if (!empty($user['middle'])) {
        printf('Middle: %s' . PHP_EOL, $user['middle']);
    }
    printf('Last: %s' . PHP_EOL, $user['last']);
    printf('Born: %d' . PHP_EOL, $user['born']);
    printf(PHP_EOL);
}
printf('Retrieved and printed out all documents from the users collection.' . PHP_EOL);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```python
users_ref = db.collection("users")
docs = users_ref.stream()

for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```ruby
users_ref = firestore.col collection_path
users_ref.get do |user|
  puts "#{user.document_id} data: #{user.data}."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
