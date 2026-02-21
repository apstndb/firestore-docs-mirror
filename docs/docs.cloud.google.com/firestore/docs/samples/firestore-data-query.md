Query a Firestore collection

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)
  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query capitalQuery = db.Collection("cities").WhereEqualTo("Capital", true);
QuerySnapshot capitalQuerySnapshot = await capitalQuery.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in capitalQuerySnapshot.Documents)
{
    Console.WriteLine("Document data for {0} document:", documentSnapshot.Id);
    Dictionary<string, object> city = documentSnapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city)
    {
        Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
    }
    Console.WriteLine("");
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
)

func multipleDocs(ctx context.Context, client *firestore.Client) error {
 fmt.Println("All capital cities:")
 iter := client.Collection("cities").Where("capital", "==", true).Documents(ctx)
 for {
     doc, err := iter.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Println(doc.Data())
 }
 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// asynchronously retrieve multiple documents
ApiFuture<QuerySnapshot> future = db.collection("cities").whereEqualTo("capital", true).get();
// future.get() blocks on response
List<QueryDocumentSnapshot> documents = future.get().getDocuments();
for (DocumentSnapshot document : documents) {
  System.out.println(document.getId() + " => " + document.toObject(City.class));
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const citiesRef = db.collection('cities');
const snapshot = await citiesRef.where('capital', '==', true).get();
if (snapshot.empty) {
  console.log('No matching documents.');
  return;
}  

snapshot.forEach(doc => {
  console.log(doc.id, '=>', doc.data());
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$query = $citiesRef->where('capital', '=', true);
$documents = $query->documents();
foreach ($documents as $document) {
    if ($document->exists()) {
        printf('Document data for document %s:' . PHP_EOL, $document->id());
        print_r($document->data());
        printf(PHP_EOL);
    } else {
        printf('Document %s does not exist!' . PHP_EOL, $document->id());
    }
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Note: Use of CollectionRef stream() is prefered to get()
docs = (
    db.collection("cities")
    .where(filter=FieldFilter("capital", "==", True))
    .stream()
)

for doc in docs:
    print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
cities_ref = firestore.col collection_path

query = cities_ref.where "capital", "=", true

query.get do |city|
  puts "#{city.document_id} data: #{city.data}."
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
