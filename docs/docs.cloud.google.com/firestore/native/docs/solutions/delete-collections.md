# Delete data with a callable Cloud Function

The page describes how to use a callable Cloud Function to delete data. Once you deploy this function, you can call it directly from your mobile app or website to recursively delete documents and collections. For example, you can use this solution to give select users the ability to delete entire collections.

For other ways to delete collections, see [Delete data](../manage-data/delete-data#collections) .

## Solution: Delete data with a callable Cloud Function

Deleting entire collections from a resource-limited mobile app can be difficult to implement for the following reasons:

  - There is no operation that atomically deletes a collection.
  - Deleting a document does not delete the documents in its subcollections.
  - If your documents have dynamic subcollections, it can be hard to know what data to delete for a given path.
  - Deleting a collection of more than 500 documents requires multiple batched write operations or hundreds of single deletes.
  - In many apps, it isn't appropriate to give end-users permission to delete entire collections.

Fortunately, you can write a [callable Cloud Function](https://firebase.google.com/docs/functions/callable) to run safe and performant deletes of entire collections or collection trees. The Cloud Function below implements a [callable function](https://firebase.google.com/docs/functions/callable) which means it can be called directly from your mobile app or website as you would for a local function.

To deploy the function and try a demo, see the [sample code](https://github.com/firebase/snippets-node/tree/master/firestore/solution-deletes) .

### Cloud Function

The Cloud Function below deletes a collection and all of its descendants.

Instead of implementing your own recursive delete logic for your Cloud Function, you can take advantage of the `  firestore:delete  ` command in the Firebase Command Line Interface (CLI). You can import any function of the Firebase CLI into your Node.js application using the `  firebase-tools  ` package.

**Note:** Deleting data with the Firebase CLI incurs read and delete costs. For more information, see [Pricing](https://firebase.google.com/docs/firestore/pricing) .

The Firebase CLI uses the Firestore REST API to find all documents under the specified path and delete them individually. This implementation requires no knowledge of your app's specific data hierarchy and will even find and delete "orphaned" documents that no longer have a parent.

### Node.js

``` javascript
/**
 * Initiate a recursive delete of documents at a given path.
 * 
 * The calling user must be authenticated and have the custom "admin" attribute
 * set to true on the auth token.
 * 
 * This delete is NOT an atomic operation and it's possible
 * that it may fail after only deleting some documents.
 * 
 * @param {string} data.path the document or collection path to delete.
 */
exports.recursiveDelete = functions
  .runWith({
    timeoutSeconds: 540,
    memory: '2GB'
  })
  .https.onCall(async (data, context) => {
    // Only allow admin users to execute this function.
    if (!(context.auth && context.auth.token && context.auth.token.admin)) {
      throw new functions.https.HttpsError(
        'permission-denied',
        'Must be an administrative user to initiate delete.'
      );
    }

    const path = data.path;
    console.log(
      `User ${context.auth.uid} has requested to delete path ${path}`
    );

    // Run a recursive delete on the given document or collection path.
    // The 'token' must be set in the functions config, and can be generated
    // at the command line by running 'firebase login:ci'.
    await firebase_tools.firestore
      .delete(path, {
        project: process.env.GCLOUD_PROJECT,
        recursive: true,
        force: true,
        token: functions.config().fb.token
      });

    return {
      path: path 
    };
  });index.js
```

### Client Invocation

To call the function, get a reference to the function from the Firebase SDK and pass the required parameters:

##### Web

``` javascript
/**
 * Call the 'recursiveDelete' callable function with a path to initiate
 * a server-side delete.
 */
function deleteAtPath(path) {
    var deleteFn = firebase.functions().httpsCallable('recursiveDelete');
    deleteFn({ path: path })
        .then(function(result) {
            logMessage('Delete success: ' + JSON.stringify(result));
        })
        .catch(function(err) {
            logMessage('Delete failed, see console,');
            console.warn(err);
        });
}index.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` text
    // Snippet not yet written
    
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` text
    // Snippet not yet written
    
```

##### Kotlin  
Android

``` kotlin
/**
 * Call the 'recursiveDelete' callable function with a path to initiate
 * a server-side delete.
 */
fun deleteAtPath(path: String) {
    val deleteFn = Firebase.functions.getHttpsCallable("recursiveDelete")
    deleteFn.call(hashMapOf("path" to path))
        .addOnSuccessListener {
            // Delete Success
            // ...
        }
        .addOnFailureListener {
            // Delete Failed
            // ...
        }
}SolutionDeletes.kt
```

##### Java  
Android

``` java
/**
 * Call the 'recursiveDelete' callable function with a path to initiate
 * a server-side delete.
 */
public void deleteAtPath(String path) {
    Map<String, Object> data = new HashMap<>();
    data.put("path", path);

    HttpsCallableReference deleteFn =
            FirebaseFunctions.getInstance().getHttpsCallable("recursiveDelete");
    deleteFn.call(data)
            .addOnSuccessListener(new OnSuccessListener<HttpsCallableResult>() {
                @Override
                public void onSuccess(HttpsCallableResult httpsCallableResult) {
                    // Delete Success
                    // ...
                }
            })
            .addOnFailureListener(new OnFailureListener() {
                @Override
                public void onFailure(@NonNull Exception e) {
                    // Delete failed
                    // ...
                }
            });
}SolutionDeletes.java
```

By using the client SDK for callable cloud functions, the users's authentication state and the `  path  ` parameter are seamlessly passed to the remote function. When the function completes, the client will receive a callback with the result or an exception. To learn about how to call a cloud function from Android, Apple, or another platform, read [the documentation](https://firebase.google.com/docs/functions/callable#call_the_function) .

**Warning:** Callable functions are not secure by default\! Make sure that your callable functions check the user's authorization before performing any sensitive actions like writing or deleting documents.

## Limitations

The solution shown above demonstrates deleting collections from a callable function, but you should be aware of the following limitations:

  - **Consistency** - the code above deletes documents one at a time. If you query while there is an ongoing delete operation, your results may reflect a partially complete state where only some targeted documents are deleted. There is also no guarantee that the delete operations will succeed or fail uniformly, so be prepared to handle cases of partial deletion.
  - **Timeouts** - the function above is configured to run for a maximum of 540 seconds before timing out. The deletion code can delete 4000 documents per second in the best case. If you need to delete more than 2,000,000 documents, you should consider running the operation on your own server so that it does not time out. For an example of how to delete a collection from your own server, see [Delete collections](../manage-data/delete-data#collections) .
  - Deleting a large number of documents might cause the data viewer in the Google Cloud console to load slowly or to return a timeout error.
