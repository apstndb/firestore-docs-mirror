Get Firestore documents in nested collections

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("SF");
IAsyncEnumerable<CollectionReference> subcollections = cityRef.ListCollectionsAsync();
IAsyncEnumerator<CollectionReference> subcollectionsEnumerator = subcollections.GetAsyncEnumerator(default);
while (await subcollectionsEnumerator.MoveNextAsync())
{
    CollectionReference subcollectionRef = subcollectionsEnumerator.Current;
    Console.WriteLine("Found subcollection with ID: {0}", subcollectionRef.Id);
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

func getCollections(ctx context.Context, client *firestore.Client) error {
 iter := client.Collection("cities").Doc("SF").Collections(ctx)
 for {
     collRef, err := iter.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return err
     }
     fmt.Printf("Found collection with id: %s\n", collRef.ID)
 }
 return nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Iterable<CollectionReference> collections =
    db.collection("cities").document("SF").listCollections();

for (CollectionReference collRef : collections) {
  System.out.println("Found subcollection with id: " + collRef.getId());
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const sfRef = db.collection('cities').doc('SF');
const collections = await sfRef.listCollections();
collections.forEach(collection => {
  console.log('Found subcollection with id:', collection.id);
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('SF');
$collections = $cityRef->collections();
foreach ($collections as $collection) {
    printf('Found subcollection with id: %s' . PHP_EOL, $collection->id());
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("cities").document("SF")
collections = city_ref.collections()
for collection in collections:
    for doc in collection.stream():
        print(f"{doc.id} => {doc.to_dict()}")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/SF"
city_ref.cols do |col|
  puts col.collection_id
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
