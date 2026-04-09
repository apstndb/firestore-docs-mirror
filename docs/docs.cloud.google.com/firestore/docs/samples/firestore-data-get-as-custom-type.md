Get a Firestore document using custom types.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference docRef = db.Collection("cities").Document("BJ");
DocumentSnapshot snapshot = await docRef.GetSnapshotAsync();
if (snapshot.Exists)
{
    Console.WriteLine("Document data for {0} document:", snapshot.Id);
    City city = snapshot.ConvertTo<City>();
    Console.WriteLine("Name: {0}", city.Name);
    Console.WriteLine("State: {0}", city.State);
    Console.WriteLine("Country: {0}", city.Country);
    Console.WriteLine("Capital: {0}", city.Capital);
    Console.WriteLine("Population: {0}", city.Population);
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

func docAsEntity(ctx context.Context, client *firestore.Client) (*City, error) {
 dsnap, err := client.Collection("cities").Doc("BJ").Get(ctx)
 if err != nil {
     return nil, err
 }
 var c City
 dsnap.DataTo(&c)
 fmt.Printf("Document data: %#v\n", c)
 return &c, nil
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
DocumentReference docRef = db.collection("cities").document("BJ");
// asynchronously retrieve the document
ApiFuture<DocumentSnapshot> future = docRef.get();
// block on response
DocumentSnapshot document = future.get();
City city = null;
if (document.exists()) {
  // convert document to POJO
  city = document.toObject(City.class);
  System.out.println(city);
} else {
  System.out.println("No such document!");
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$docRef = $db->collection('samples/php/cities')->document('SF');
$snapshot = $docRef->snapshot();
$city = City::fromArray($snapshot->data());

if ($snapshot->exists()) {
    printf('Document data:' . PHP_EOL);
    print((string) $city);
} else {
    printf('Document %s does not exist!' . PHP_EOL, $snapshot->id());
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
doc_ref = db.collection("cities").document("BJ")

doc = doc_ref.get()
city = City.from_dict(doc.to_dict())
print(city)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
