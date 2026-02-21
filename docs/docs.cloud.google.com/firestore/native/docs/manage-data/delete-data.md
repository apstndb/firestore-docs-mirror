# Delete documents and fields

The following examples demonstrate how to delete documents, fields, and collections.

## Delete documents

To delete a document, use the following language-specific `  delete()  ` methods:

### Web version 9

Use the `  deleteDoc()  ` method:

``` javascript
import { doc, deleteDoc } from "firebase/firestore";

await deleteDoc(doc(db, "cities", "DC"));delete_document.js
```

### Web version 8

Use the `  delete()  ` method:

``` javascript
db.collection("cities").doc("DC").delete().then(() => {
    console.log("Document successfully deleted!");
}).catch((error) => {
    console.error("Error removing document: ", error);
});test.firestore.js
```

##### Swift

Use the `  delete()  ` method:

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
do {
  try await db.collection("cities").document("DC").delete()
  print("Document successfully removed!")
} catch {
  print("Error removing document: \(error)")
}ViewController.swift
```

##### Objective-C

Use the `  deleteDocumentWithCompletion:  ` method:

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"DC"]
    deleteDocumentWithCompletion:^(NSError * _Nullable error) {
      if (error != nil) {
        NSLog(@"Error removing document: %@", error);
      } else {
        NSLog(@"Document successfully removed!");
      }
}];ViewController.m
```

##### Kotlin  
Android

Use the `  delete()  ` method:

``` kotlin
db.collection("cities").document("DC")
    .delete()
    .addOnSuccessListener { Log.d(TAG, "DocumentSnapshot successfully deleted!") }
    .addOnFailureListener { e -> Log.w(TAG, "Error deleting document", e) }DocSnippets.kt
```

##### Java  
Android

Use the `  delete()  ` method:

``` java
db.collection("cities").document("DC")
        .delete()
        .addOnSuccessListener(new OnSuccessListener<Void>() {
            @Override
            public void onSuccess(Void aVoid) {
                Log.d(TAG, "DocumentSnapshot successfully deleted!");
            }
        })
        .addOnFailureListener(new OnFailureListener() {
            @Override
            public void onFailure(@NonNull Exception e) {
                Log.w(TAG, "Error deleting document", e);
            }
        });DocSnippets.java
```

### Dart

Use the `  delete()  ` method:

``` dart
db.collection("cities").doc("DC").delete().then(
      (doc) => print("Document deleted"),
      onError: (e) => print("Error updating document $e"),
    );firestore.dart
```

##### Java

Use the `  delete()  ` method:

``` java
// asynchronously delete a document
ApiFuture<WriteResult> writeResult = db.collection("cities").document("DC").delete();
// ...
System.out.println("Update time : " + writeResult.get().getUpdateTime());ManageDataSnippets.java
```

##### Python

Use the `  delete()  ` method:

``` python
db.collection("cities").document("DC").delete()snippets.py
```

##### Python  
(Async)

Use the `  delete()  ` method:

``` python
await db.collection("cities").document("DC").delete()snippets.py
```

##### C++

Use the `  Delete()  ` method:

``` cpp
db->Collection("cities").Document("DC").Delete().OnCompletion(
    [](const Future<void>& future) {
      if (future.error() == Error::kErrorOk) {
        std::cout << "DocumentSnapshot successfully deleted!" << std::endl;
      } else {
        std::cout << "Error deleting document: " << future.error_message()
                  << std::endl;
      }
    });snippets.cpp
```

##### Node.js

Use the `  delete()  ` method:

``` javascript
const res = await db.collection('cities').doc('DC').delete();index.js
```

##### Go

Use the `  Delete()  ` method:

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func deleteDoc(ctx context.Context, client *firestore.Client) error {
 _, err := client.Collection("cities").Doc("DC").Delete(ctx)
 if err != nil {
     // Handle any errors in an appropriate way, such as returning them.
     log.Printf("An error has occurred: %s", err)
 }

 return err
}
save_data_delete_doc.go
```

##### PHP

Use the `  delete()  ` method:

``` php
$db->collection('samples/php/cities')->document('DC')->delete();data_delete_doc.php
```

##### Unity

Use the `  DeleteAsync()  ` method:

``` text
DocumentReference cityRef = db.Collection("cities").Document("DC");
cityRef.DeleteAsync();
```

##### C\#

Use the `  DeleteAsync()  ` method:

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("DC");
await cityRef.DeleteAsync();Program.cs
```

##### Ruby

Use the `  delete()  ` method:

``` ruby
city_ref = firestore.doc "#{collection_path}/DC"
city_ref.deletedelete_data.rb
```

**Warning:** Deleting a document does not delete its subcollections\!

When you delete a document, Firestore does not automatically delete the documents within its subcollections. You can still access the subcollection documents by reference. For example, you can access the document at path `  /mycoll/mydoc/mysubcoll/mysubdoc  ` even if you delete the ancestor document at `  /mycoll/mydoc  ` .

Non-existent ancestor documents [appear in the console](../using-console#non-existent_ancestor_documents) , but they do not appear in query results and snapshots.

If you want to delete a document and all the documents within its subcollections, you must do so manually. For more information, see [Delete Collections](#collections) .

## Delete fields

To delete specific fields from a document, use the following language-specific `  FieldValue.delete()  ` methods when you update a document:

### Web version 9

Use the `  deleteField()  ` method:

``` javascript
import { doc, updateDoc, deleteField } from "firebase/firestore";

const cityRef = doc(db, 'cities', 'BJ');

// Remove the 'capital' field from the document
await updateDoc(cityRef, {
    capital: deleteField()
});update_delete_field.js
```

### Web version 8

Use the `  FieldValue.delete()  ` method:

``` javascript
var cityRef = db.collection('cities').doc('BJ');

// Remove the 'capital' field from the document
var removeCapital = cityRef.update({
    capital: firebase.firestore.FieldValue.delete()
});test.firestore.js
```

##### Swift

Use the `  FieldValue.delete()  ` method:

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
do {

  try await db.collection("cities").document("BJ").updateData([
    "capital": FieldValue.delete(),
  ])
  print("Document successfully updated")
} catch {
  print("Error updating document: \(error)")
}ViewController.swift
```

##### Objective-C

Use the `  fieldValueForDelete:  ` method:

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"BJ"] updateData:@{
  @"capital": [FIRFieldValue fieldValueForDelete]
} completion:^(NSError * _Nullable error) {
  if (error != nil) {
    NSLog(@"Error updating document: %@", error);
  } else {
    NSLog(@"Document successfully updated");
  }
}];ViewController.m
```

##### Kotlin  
Android

Use the `  FieldValue.delete()  ` method:

``` kotlin
val docRef = db.collection("cities").document("BJ")

// Remove the 'capital' field from the document
val updates = hashMapOf<String, Any>(
    "capital" to FieldValue.delete(),
)

docRef.update(updates).addOnCompleteListener { }DocSnippets.kt
```

##### Java  
Android

Use the `  FieldValue.delete()  ` method:

``` java
DocumentReference docRef = db.collection("cities").document("BJ");

// Remove the 'capital' field from the document
Map<String,Object> updates = new HashMap<>();
updates.put("capital", FieldValue.delete());

docRef.update(updates).addOnCompleteListener(new OnCompleteListener<Void>() {
    // ...
    // ...DocSnippets.java
```

### Dart

Use the `  FieldValue.delete()  ` method:

``` dart
final docRef = db.collection("cities").doc("BJ");

// Remove the 'capital' field from the document
final updates = <String, dynamic>{
  "capital": FieldValue.delete(),
};

docRef.update(updates);firestore.dart
```

##### Java

Use the `  FieldValue.delete()  ` method:

``` java
DocumentReference docRef = db.collection("cities").document("BJ");
Map<String, Object> updates = new HashMap<>();
updates.put("capital", FieldValue.delete());
// Update and delete the "capital" field in the document
ApiFuture<WriteResult> writeResult = docRef.update(updates);
System.out.println("Update time : " + writeResult.get());ManageDataSnippets.java
```

##### Python

Use the `  firestore.DELETE_FIELD  ` method:

``` python
city_ref = db.collection("cities").document("BJ")
city_ref.update({"capital": firestore.DELETE_FIELD})snippets.py
```

##### Python  
(Async)

Use the `  firestore.DELETE_FIELD  ` method:

``` python
city_ref = db.collection("cities").document("BJ")
await city_ref.update({"capital": firestore.DELETE_FIELD})snippets.py
```

##### C++

Use the `  FieldValue::Delete()  ` method:

``` cpp
DocumentReference doc_ref = db->Collection("cities").Document("BJ");
doc_ref.Update({{"capital", FieldValue::Delete()}})
    .OnCompletion([](const Future<void>& future) { /*...*/ });snippets.cpp
```

##### Node.js

Use the `  FieldValue.delete()  ` method:

``` javascript
// Create a document reference
const cityRef = db.collection('cities').doc('BJ');

// Remove the 'capital' field from the document
const res = await cityRef.update({
  capital: FieldValue.delete()
});index.js
```

##### Go

Use the `  firestore.Delete  ` method:

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func deleteField(ctx context.Context, client *firestore.Client) error {
 _, err := client.Collection("cities").Doc("BJ").Update(ctx, []firestore.Update{
     {
         Path:  "capital",
         Value: firestore.Delete,
     },
 })
 if err != nil {
     // Handle any errors in an appropriate way, such as returning them.
     log.Printf("An error has occurred: %s", err)
 }

 // ...
 return err
}
save_data_delete_field.go
```

##### PHP

Use the `  FieldValue::deleteField()  ` method:

``` php
$cityRef = $db->collection('samples/php/cities')->document('BJ');
$cityRef->update([
    ['path' => 'capital', 'value' => FieldValue::deleteField()]
]);data_delete_field.php
```

##### Unity

Use the `  FieldValue.Delete  ` method:

``` text
DocumentReference cityRef = db.Collection("cities").Document("BJ");
Dictionary<string, object> updates = new Dictionary<string, object>
{
    { "Capital", FieldValue.Delete }
};
```

##### C\#

Use the `  FieldValue.Delete  ` method:

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("BJ");
Dictionary<string, object> updates = new Dictionary<string, object>
{
    { "Capital", FieldValue.Delete }
};
await cityRef.UpdateAsync(updates);Program.cs
```

##### Ruby

Use the `  firestore.field_delete  ` method:

``` ruby
city_ref = firestore.doc "#{collection_path}/BJ"
city_ref.update({ capital: firestore.field_delete })delete_data.rb
```

## Delete collections

To delete an entire collection or subcollection in Firestore, retrieve (read) all the documents within the collection or subcollection and delete them. This process incurs both read and delete costs. If you have larger collections, you may want to delete the documents in smaller batches to avoid out-of-memory errors. Repeat the process until you've deleted the entire collection or subcollection.

Deleting a collection requires coordinating an unbounded number of individual delete requests. If you need to delete entire collections, do so only from a trusted server environment. While it is possible to delete a collection from a mobile/web client, doing so has negative security and performance implications.

The following snippets are simplified for clarity and don't include error handling, security, deleting subcollections, or performance optimizations. To learn more about one recommended approach to deleting collections in production, see [Deleting Collections and Subcollections](../solutions/delete-collections) .

##### Web

``` text
// Deleting collections from a Web client is not recommended.
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` text
// Deleting collections from an Apple client is not recommended.
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` text
// Deleting collections from an Apple client is not recommended.
  
```

##### Kotlin  
Android

``` text
// Deleting collections from an Android client is not recommended.
```

##### Java  
Android

``` text
// Deleting collections from an Android client is not recommended.
```

### Dart

Deleting collections from the client is not recommended.

##### Java

``` java
/**
 * Delete a collection in batches to avoid out-of-memory errors. Batch size may be tuned based on
 * document size (atmost 1MB) and application requirements.
 */
void deleteCollection(CollectionReference collection, int batchSize) {
  try {
    // retrieve a small batch of documents to avoid out-of-memory errors
    ApiFuture<QuerySnapshot> future = collection.limit(batchSize).get();
    int deleted = 0;
    // future.get() blocks on document retrieval
    List<QueryDocumentSnapshot> documents = future.get().getDocuments();
    for (QueryDocumentSnapshot document : documents) {
      document.getReference().delete();
      ++deleted;
    }
    if (deleted >= batchSize) {
      // retrieve and delete another batch
      deleteCollection(collection, batchSize);
    }
  } catch (Exception e) {
    System.err.println("Error deleting collection : " + e.getMessage());
  }
}
ManageDataSnippets.java
```

##### Python

``` python
def delete_collection(coll_ref):

    print(f"Recursively deleting collection: {coll_ref}")
    db.recursive_delete(coll_ref)
snippets.py
```

##### Python  
(Async)

``` python
async def delete_collection(coll_ref):

    await db.recursive_delete(coll_ref)
snippets.py
```

##### C++

``` text
// This is not supported. Delete data using CLI as discussed below.
  
```

##### Node.js

``` javascript
async function deleteCollection(db, collectionPath) {
  const collectionRef = db.collection(collectionPath);
  return await db.recursiveDelete(collectionRef);
}
index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

func deleteCollection(w io.Writer, projectID, collectionName string,
 batchSize int) error {

 // Instantiate a client
 ctx := context.Background()
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return err
 }

 col := client.Collection(collectionName)
 bulkwriter := client.BulkWriter(ctx)

 for {
     // Get a batch of documents
     iter := col.Limit(batchSize).Documents(ctx)
     numDeleted := 0

     // Iterate through the documents, adding
     // a delete operation for each one to the BulkWriter.
     for {
         doc, err := iter.Next()
         if err == iterator.Done {
             break
         }
         if err != nil {
             return err
         }

         bulkwriter.Delete(doc.Ref)
         numDeleted++
     }

     // If there are no documents to delete,
     // the process is over.
     if numDeleted == 0 {
         bulkwriter.End()
         break
     }

     bulkwriter.Flush()
 }
 fmt.Fprintf(w, "Deleted collection \"%s\"", collectionName)
 return nil
}
save_data_delete_collection.go
```

##### PHP

``` php
function data_delete_collection(string $projectId, string $collectionName, int $batchSize)
{
    // Create the Cloud Firestore client
    $db = new FirestoreClient([
        'projectId' => $projectId,
    ]);
    $collectionReference = $db->collection($collectionName);
    $documents = $collectionReference->limit($batchSize)->documents();
    while (!$documents->isEmpty()) {
        foreach ($documents as $document) {
            printf('Deleting document %s' . PHP_EOL, $document->id());
            $document->reference()->delete();
        }
        $documents = $collectionReference->limit($batchSize)->documents();
    }
}data_delete_collection.php
```

##### Unity

``` text
// This is not supported. Delete data using CLI as discussed below.
```

##### C\#

``` csharp
private static async Task DeleteCollection(CollectionReference collectionReference, int batchSize)
{
    QuerySnapshot snapshot = await collectionReference.Limit(batchSize).GetSnapshotAsync();
    IReadOnlyList<DocumentSnapshot> documents = snapshot.Documents;
    while (documents.Count > 0)
    {
        foreach (DocumentSnapshot document in documents)
        {
            Console.WriteLine("Deleting document {0}", document.Id);
            await document.Reference.DeleteAsync();
        }
        snapshot = await collectionReference.Limit(batchSize).GetSnapshotAsync();
        documents = snapshot.Documents;
    }
    Console.WriteLine("Finished deleting all documents from the collection.");
}Program.cs
```

##### Ruby

``` ruby
cities_ref = firestore.col collection_path
query      = cities_ref

query.get do |document_snapshot|
  puts "Deleting document #{document_snapshot.document_id}."
  document_ref = document_snapshot.ref
  document_ref.delete
enddelete_data.rb
```

## Delete data with TTL policies

A TTL policy designates a given field as the expiration time for documents in a given collection group. TTL delete operations count towards your document delete costs.

For information about setting TTL, see [Manage data retention with TTL policies](/firestore/native/docs/ttl) .

## Bulk deletion jobs

Firestore supports several tools for bulk deletion. You should select a tool based on the number of documents you need to delete and the level of configurability you need.

**Note:** Deleting a large number of documents [can impact latency](/firestore/native/docs/best-practices#avoid-skipping) . If latency is caused by too many recent deletes, the issue should automatically resolve after some time. If the issue does not resolve, [contact support](https://cloud.google.com/support-hub) .

For smaller jobs of thousands of documents, use the console or the Firebase CLI. For larger jobs, these tools might start to timeout and require you to run the tool multiple times.

### Console

You can [delete documents and collections from the Firestore page in the console](../using-console#delete_data) . Deleting a document from the console deletes all of the nested data in that document, including any subcollections.

### Firebase CLI

You can also use the [Firebase CLI](//firebase.google.com/docs/cli) to delete documents and collections. Use the following command to delete data:

**Note:** Deleting data with the Firebase CLI incurs read and delete costs. For more information, see [Pricing](https://firebase.google.com/docs/firestore/pricing#pricing_by_location) .

``` text
firebase firestore:delete  --database=DATABASE_ID PATH
```

Replace DATABASE\_ID with your database ID and PATH with a path to a document or collection.

For large deletion jobs (millions of documents), use one of the following:

### Managed bulk delete

Firestore supports bulk deleting one or more collection groups. For more information, see [Bulk delete data](/firestore/native/docs/manage-data/bulk-delete) .

### Dataflow connector

You can use [Dataflow](https://cloud.google.com/dataflow/docs/overview) for bulk operations on your database. This option is the most configurable, but also requires more set up than other bulk delete options. See the Firestore connector for Dataflow introduction [blog post](https://cloud.google.com/blog/topics/developers-practitioners/using-firestore-and-apache-beam-data-processing) has an example of deleting all documents in a collection group.
