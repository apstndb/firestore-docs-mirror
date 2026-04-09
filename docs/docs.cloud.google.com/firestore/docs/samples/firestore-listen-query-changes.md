Observe change types with Firestore watch listeners

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get real-time updates](/firestore/native/docs/query-data/listen)
  - [Get realtime updates with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/listen)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = db.Collection("cities").WhereEqualTo("State", "CA");

FirestoreChangeListener listener = query.Listen(snapshot =>
{
    foreach (DocumentChange change in snapshot.Changes)
    {
        if (change.ChangeType.ToString() == "Added")
        {
            Console.WriteLine("New city: {0}", change.Document.Id);
        }
        else if (change.ChangeType.ToString() == "Modified")
        {
            Console.WriteLine("Modified city: {0}", change.Document.Id);
        }
        else if (change.ChangeType.ToString() == "Removed")
        {
            Console.WriteLine("Removed city: {0}", change.Document.Id);
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

// listenChanges listens to a query, returning the list of document changes.
func listenChanges(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Where("state", "==", "CA").Snapshots(ctx)
 for {
     snap, err := it.Next()
     // DeadlineExceeded will be returned when ctx is cancelled.
     if status.Code(err) == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if snap != nil {
         for _, change := range snap.Changes {
             switch change.Kind {
             case firestore.DocumentAdded:
                 fmt.Fprintf(w, "New city: %v\n", change.Doc.Data())
             case firestore.DocumentModified:
                 fmt.Fprintf(w, "Modified city: %v\n", change.Doc.Data())
             case firestore.DocumentRemoved:
                 fmt.Fprintf(w, "Removed city: %v\n", change.Doc.Data())
             }
         }
     }
 }
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
db.collection("cities")
    .whereEqualTo("state", "CA")
    .addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          @Override
          public void onEvent(
              @Nullable QuerySnapshot snapshots, @Nullable FirestoreException e) {
            if (e != null) {
              System.err.println("Listen failed: " + e);
              return;
            }

            for (DocumentChange dc : snapshots.getDocumentChanges()) {
              switch (dc.getType()) {
                case ADDED:
                  System.out.println("New city: " + dc.getDocument().getData());
                  break;
                case MODIFIED:
                  System.out.println("Modified city: " + dc.getDocument().getData());
                  break;
                case REMOVED:
                  System.out.println("Removed city: " + dc.getDocument().getData());
                  break;
                default:
                  break;
              }
            }
          }
        });
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const observer = db.collection('cities').where('state', '==', 'CA')
  .onSnapshot(querySnapshot => {
    querySnapshot.docChanges().forEach(change => {
      if (change.type === 'added') {
        console.log('New city: ', change.doc.data());
      }
      if (change.type === 'modified') {
        console.log('Modified city: ', change.doc.data());
      }
      if (change.type === 'removed') {
        console.log('Removed city: ', change.doc.data());
      }
    });
  });
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create an Event for notifying main thread.
delete_done = threading.Event()

# Create a callback on_snapshot function to capture changes
def on_snapshot(col_snapshot, changes, read_time):
    print("Callback received query snapshot.")
    print("Current cities in California: ")
    for change in changes:
        if change.type.name == "ADDED":
            print(f"New city: {change.document.id}")
        elif change.type.name == "MODIFIED":
            print(f"Modified city: {change.document.id}")
        elif change.type.name == "REMOVED":
            print(f"Removed city: {change.document.id}")
            delete_done.set()

col_query = db.collection("cities").where(filter=FieldFilter("state", "==", "CA"))

# Watch the collection query
query_watch = col_query.on_snapshot(on_snapshot)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = firestore.col(collection_path).where :state, :==, "CA"
added = []
modified = []
removed = []

# Watch the collection query.
listener = query.listen do |snapshot|
  puts "Callback received query snapshot."
  puts "Current cities in California:"
  snapshot.changes.each do |change|
    if change.added?
      puts "New city: #{change.doc.document_id}"
      added << snapshot
    elsif change.modified?
      puts "Modified city: #{change.doc.document_id}"
      modified << snapshot
    elsif change.removed?
      puts "Removed city: #{change.doc.document_id}"
      removed << snapshot
    end
  end
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
