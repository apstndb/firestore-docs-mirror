Query a Firestore collection group with an eq filter

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query museums = db.CollectionGroup("landmarks").WhereEqualTo("Type", "museum");
QuerySnapshot querySnapshot = await museums.GetSnapshotAsync();
foreach (DocumentSnapshot document in querySnapshot.Documents)
{
    Console.WriteLine($"{document.Reference.Path}: {document.GetValue<string>("Name")}");
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

// collectionGroupQuery runs a collection group query over the data created by
// collectionGroupSetup.
func collectionGroupQuery(w io.Writer, projectID string) error {
 ctx := context.Background()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.CollectionGroup("landmarks").Where("type", "==", "museum").Documents(ctx)
 for {
     doc, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return fmt.Errorf("documents iterator: %w", err)
     }
     fmt.Fprintf(w, "%s: %s", doc.Ref.ID, doc.Data()["name"])
 }

 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
final Query museums = db.collectionGroup("landmarks").whereEqualTo("type", "museum");
final ApiFuture<QuerySnapshot> querySnapshot = museums.get();
for (DocumentSnapshot document : querySnapshot.get().getDocuments()) {
  System.out.println(document.getId());
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const querySnapshot = await db.collectionGroup('landmarks').where('type', '==', 'museum').get();
querySnapshot.forEach((doc) => {
  console.log(doc.id, ' => ', doc.data());
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$museums = $db->collectionGroup('landmarks')->where('type', '==', 'museum');
foreach ($museums->documents() as $document) {
    printf('%s => %s' . PHP_EOL, $document->id(), $document->data()['name']);
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
museums = db.collection_group("landmarks").where(
    filter=FieldFilter("type", "==", "museum")
)
docs = museums.stream()
for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
museums = firestore.collection_group("landmarks").where("type", "==", "museum")
museums.get do |museum|
  puts "#{museum[:type]} name is #{museum[:name]}."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
