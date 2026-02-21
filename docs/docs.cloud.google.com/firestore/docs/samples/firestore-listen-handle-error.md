Handle Firestore watch listener errors

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get real-time updates](/firestore/native/docs/query-data/listen)
  - [Get realtime updates with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/listen)

## Code sample

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

// listenErrors demonstrates how to handle listening errors.
func listenErrors(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Snapshots(ctx)
 for {
     snap, err := it.Next()
     // Canceled will be returned when ctx is cancelled and DeadlineExceeded will
     // be returned when ctx reaches its deadline.
     if e := status.Code(err); e == codes.Canceled || e == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if snap != nil {
         for _, change := range snap.Changes {
             if change.Kind == firestore.DocumentAdded {
                 fmt.Fprintf(w, "New city: %v\n", change.Doc.Data())
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
              if (dc.getType() == Type.ADDED) {
                System.out.println("New city: " + dc.getDocument().getData());
              }
            }
          }
        });
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
db.collection('cities')
  .onSnapshot((snapshot) => {
    //...
  }, (error) => {
    //...
  });
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
listener = firestore.col(collection_path).listen do |snapshot|
  snapshot.changes.each do |change|
    puts "New city: #{change.doc.document_id}" if change.added?
  end
end

# Register to be notified when unhandled errors occur.
listener.on_error do |error|
  puts "Listen failed: #{error.message}"
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
