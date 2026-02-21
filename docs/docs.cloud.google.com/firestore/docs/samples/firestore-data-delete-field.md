Delete a Firestore field

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Delete data from Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/delete-data)
  - [Delete documents and fields](/firestore/native/docs/manage-data/delete-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("BJ");
Dictionary<string, object> updates = new Dictionary<string, object>
{
    { "Capital", FieldValue.Delete }
};
await cityRef.UpdateAsync(updates);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func deleteField(ctx context.Context, client *firestore.Client) error {
 _, err := client.Collection("cities").Doc("BJ").Update(ctx, []firestore.Update{
     {
         Path:  "capital",
         Value: firestore.Delete,
     },
 })
 if err != nil {
     // Handle any errors in an appropriate way, such as returning them.
     log.Printf("An error has occurred: %s", err)
 }

 // ...
 return err
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
DocumentReference docRef = db.collection("cities").document("BJ");
Map<String, Object> updates = new HashMap<>();
updates.put("capital", FieldValue.delete());
// Update and delete the "capital" field in the document
ApiFuture<WriteResult> writeResult = docRef.update(updates);
System.out.println("Update time : " + writeResult.get());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Create a document reference
const cityRef = db.collection('cities').doc('BJ');

// Remove the 'capital' field from the document
const res = await cityRef.update({
  capital: FieldValue.delete()
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('BJ');
$cityRef->update([
    ['path' => 'capital', 'value' => FieldValue::deleteField()]
]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("cities").document("BJ")
city_ref.update({"capital": firestore.DELETE_FIELD})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/BJ"
city_ref.update({ capital: firestore.field_delete })
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
