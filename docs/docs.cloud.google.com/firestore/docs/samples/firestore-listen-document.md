Create a Firestore watch listener

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get real-time updates](/firestore/native/docs/query-data/listen)
  - [Get realtime updates with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/listen)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference docRef = db.Collection("cities").Document("SF");
FirestoreChangeListener listener = docRef.Listen(snapshot =>
{
    Console.WriteLine("Callback received document snapshot.");
    Console.WriteLine("Document exists? {0}", snapshot.Exists);
    if (snapshot.Exists)
    {
        Console.WriteLine("Document data for {0} document:", snapshot.Id);
        Dictionary<string, object> city = snapshot.ToDictionary();
        foreach (KeyValuePair<string, object> pair in city)
        {
            Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
        }
    }
});
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/firestore"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenDocument listens to a single document.
func listenDocument(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 // Сontext with timeout stops listening to changes.
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Doc("SF").Snapshots(ctx)
 for {
     snap, err := it.Next()
     // DeadlineExceeded will be returned when ctx is cancelled.
     if status.Code(err) == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if !snap.Exists() {
         fmt.Fprintf(w, "Document no longer exists\n")
         return nil
     }
     fmt.Fprintf(w, "Received document snapshot: %v\n", ssnap.Data))
 }
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
DocumentReference docRef = db.collection("cities").document("SF");
docRef.addSnapshotListener(
    new EventListener<DocumentSnapshot>() {
      @Override
      public void onEvent(@Nullable DocumentSnapshot snapshot, @Nullable FirestoreException e) {
        if (e != null) {
          System.err.println("Listen failed: " + e);
          return;
        }

        if (snapshot != null && snapshot.exists()) {
          System.out.println("Current data: " + snapshot.getData());
        } else {
          System.out.print("Current data: null");
        }
      }
    });
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const doc = db.collection('cities').doc('SF');

const observer = doc.onSnapshot(docSnapshot => {
  console.log(`Received doc snapshot: ${docSnapshot}`);
  // ...
}, err => {
  console.log(`Encountered error: ${err}`);
});
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create an Event for notifying main thread.
callback_done = threading.Event()

# Create a callback on_snapshot function to capture changes
def on_snapshot(doc_snapshot, changes, read_time):
    for doc in doc_snapshot:
        print(f"Received document snapshot: {doc.id}")
    callback_done.set()

doc_ref = db.collection("cities").document("SF")

# Watch the document
doc_watch = doc_ref.on_snapshot(on_snapshot)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
doc_ref = firestore.col(collection_path).doc document_path
snapshots = []

# Watch the document.
listener = doc_ref.listen do |snapshot|
  puts "Received document snapshot: #{snapshot.document_id}"
  snapshots << snapshot
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
