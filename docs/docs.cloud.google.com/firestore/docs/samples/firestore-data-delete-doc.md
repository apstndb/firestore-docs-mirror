Delete a single Firestore document

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Delete data from Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/delete-data)
  - [Delete documents and fields](/firestore/native/docs/manage-data/delete-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("DC");
await cityRef.DeleteAsync();
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func deleteDoc(ctx context.Context, client *firestore.Client) error {
 _, err := client.Collection("cities").Doc("DC").Delete(ctx)
 if err != nil {
     // Handle any errors in an appropriate way, such as returning them.
     log.Printf("An error has occurred: %s", err)
 }

 return err
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// asynchronously delete a document
ApiFuture<WriteResult> writeResult = db.collection("cities").document("DC").delete();
// ...
System.out.println("Update time : " + writeResult.get().getUpdateTime());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const res = await db.collection('cities').doc('DC').delete();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$db->collection('samples/php/cities')->document('DC')->delete();
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
db.collection("cities").document("DC").delete()
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/DC"
city_ref.delete
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
