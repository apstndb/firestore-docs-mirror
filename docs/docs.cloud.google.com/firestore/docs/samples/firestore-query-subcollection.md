Demonstrates how to query a subcollection.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference landmarks = db.Collection("cities").Document("SF").Collection("landmarks");
QuerySnapshot querySnapshot = await landmarks.GetSnapshotAsync();
foreach (DocumentSnapshot document in querySnapshot.Documents)
{
    Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
db.collection("cities")
        .document("SF")
        .collection("landmarks")
        .get()
        .addOnCompleteListener(new OnCompleteListener<QuerySnapshot>() {
            @Override
            public void onComplete(@NonNull Task<QuerySnapshot> task) {
                if (task.isSuccessful()) {
                    for (QueryDocumentSnapshot document : task.getResult()) {
                        Log.d(TAG, document.getId() + " => " + document.getData());
                    }
                } else {
                    Log.d(TAG, "Error getting documents: ", task.getException());
                }
            }
        });
```

### Kotlin

``` kotlin
db.collection("cities")
    .document("SF")
    .collection("landmarks")
    .get()
    .addOnSuccessListener { result ->
        for (document in result) {
            Log.d(TAG, "${document.id} => ${document.data}")
        }
    }
    .addOnFailureListener { exception ->
        Log.d(TAG, "Error getting documents: ", exception)
    }
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const { collection, getDocs } = require("firebase/firestore");
// Query a reference to a subcollection
const querySnapshot = await getDocs(collection(db, "cities", "SF", "landmarks"));
querySnapshot.forEach((doc) => {
  // doc.data() is never undefined for query doc snapshots
  console.log(doc.id, " => ", doc.data());
});
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
