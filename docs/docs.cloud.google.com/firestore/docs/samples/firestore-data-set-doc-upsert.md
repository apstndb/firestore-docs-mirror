Update a Firestore document using merge

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference docRef = db.Collection("cities").Document("LA");
Dictionary<string, object> update = new Dictionary<string, object>
{
    { "capital", false }
};
await docRef.SetAsync(update, SetOptions.MergeAll);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func updateDocCreateIfMissing(ctx context.Context, client *firestore.Client) error {
 _, err := client.Collection("cities").Doc("BJ").Set(ctx, map[string]interface{}{
     "capital": true,
 }, firestore.MergeAll)

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
// asynchronously update doc, create the document if missing
Map<String, Object> update = new HashMap<>();
update.put("capital", true);

ApiFuture<WriteResult> writeResult =
    db.collection("cities").document("BJ").set(update, SetOptions.merge());
// ...
System.out.println("Update time : " + writeResult.get().getUpdateTime());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const cityRef = db.collection('cities').doc('BJ');

const res = await cityRef.set({
  capital: true
}, { merge: true });
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('BJ');
$cityRef->set([
    'capital' => true
], ['merge' => true]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("cities").document("BJ")

city_ref.set({"capital": True}, merge=True)
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/LA"
city_ref.set({ capital: false }, merge: true)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
