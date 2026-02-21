Retrieve Firestore Document as Map

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference docRef = db.Collection("cities").Document("SF");
DocumentSnapshot snapshot = await docRef.GetSnapshotAsync();
if (snapshot.Exists)
{
    Console.WriteLine("Document data for {0} document:", snapshot.Id);
    Dictionary<string, object> city = snapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city)
    {
        Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
    }
}
else
{
    Console.WriteLine("Document {0} does not exist!", snapshot.Id);
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"

 "cloud.google.com/go/firestore"
)

func docAsMap(ctx context.Context, client *firestore.Client) (map[string]interface{}, error) {
 dsnap, err := client.Collection("cities").Doc("SF").Get(ctx)
 if err != nil {
     return nil, err
 }
 m := dsnap.Data()
 fmt.Printf("Document data: %#v\n", m)
 return m, nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
DocumentReference docRef = db.collection("cities").document("SF");
// asynchronously retrieve the document
ApiFuture<DocumentSnapshot> future = docRef.get();
// ...
// future.get() blocks on response
DocumentSnapshot document = future.get();
if (document.exists()) {
  System.out.println("Document data: " + document.getData());
} else {
  System.out.println("No such document!");
}
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const cityRef = db.collection('cities').doc('SF');
const doc = await cityRef.get();
if (!doc.exists) {
  console.log('No such document!');
} else {
  console.log('Document data:', doc.data());
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$docRef = $db->collection('samples/php/cities')->document('SF');
$snapshot = $docRef->snapshot();

if ($snapshot->exists()) {
    printf('Document data:' . PHP_EOL);
    print_r($snapshot->data());
} else {
    printf('Document %s does not exist!' . PHP_EOL, $snapshot->id());
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
doc_ref = db.collection("cities").document("SF")

doc = doc_ref.get()
if doc.exists:
    print(f"Document data: {doc.to_dict()}")
else:
    print("No such document!")
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
doc_ref  = firestore.doc "#{collection_path}/SF"
snapshot = doc_ref.get
if snapshot.exists?
  puts "#{snapshot.document_id} data: #{snapshot.data}."
else
  puts "Document #{snapshot.document_id} does not exist!"
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
