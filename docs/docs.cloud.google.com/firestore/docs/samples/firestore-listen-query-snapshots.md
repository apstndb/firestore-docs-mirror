Monitor query result changes with Firestore Watch

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
    Console.WriteLine("Callback received query snapshot.");
    Console.WriteLine("Current cities in California:");
    foreach (DocumentSnapshot documentSnapshot in snapshot.Documents)
    {
        Console.WriteLine(documentSnapshot.Id);
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
 "google.golang.org/api/iterator"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenMultiple listens to a query, returning the names of all cities
// for a state.
func listenMultiple(ctx context.Context, w io.Writer, projectID, collection string) error {
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
         for {
             doc, err := snap.Documents.Next()
             if err == iterator.Done {
                 break
             }
             if err != nil {
                 return fmt.Errorf("Documents.Next: %w", err)
             }
             fmt.Fprintf(w, "Current cities in California: %v\n", doc.Ref.ID)
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
              System.err.println("Listen failed:" + e);
              return;
            }

            List<String> cities = new ArrayList<>();
            for (DocumentSnapshot doc : snapshots) {
              if (doc.get("name") != null) {
                cities.add(doc.getString("name"));
              }
            }
            System.out.println("Current cites in CA: " + cities);
          }
        });
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = db.collection('cities').where('state', '==', 'CA');

const observer = query.onSnapshot(querySnapshot => {
  console.log(`Received query snapshot of size ${querySnapshot.size}`);
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
def on_snapshot(col_snapshot, changes, read_time):
    print("Callback received query snapshot.")
    print("Current cities in California:")
    for doc in col_snapshot:
        print(f"{doc.id}")
    callback_done.set()

col_query = db.collection("cities").where(filter=FieldFilter("state", "==", "CA"))

# Watch the collection query
query_watch = col_query.on_snapshot(on_snapshot)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = firestore.col(collection_path).where :state, :==, "CA"
docs = []

# Watch the collection query.
listener = query.listen do |snapshot|
  puts "Callback received query snapshot."
  puts "Current cities in California:"
  snapshot.docs.each do |doc|
    puts doc.document_id
    docs << doc
  end
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
