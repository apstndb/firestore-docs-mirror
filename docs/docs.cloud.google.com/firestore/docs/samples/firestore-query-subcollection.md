Demonstrates how to query a subcollection.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference landmarks = db.Collection("cities").Document("SF").Collection("landmarks");
    QuerySnapshot querySnapshot = await landmarks.GetSnapshotAsync();
    foreach (DocumentSnapshot document in querySnapshot.Documents)
    {
        Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
    }

### Kotlin

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
