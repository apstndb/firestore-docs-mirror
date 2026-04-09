Update a Firestore document field

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference cityRef = db.Collection("cities").Document("new-city-id");
Dictionary<string, object> updates = new Dictionary<string, object>
{
    { "Capital", false }
};
await cityRef.UpdateAsync(updates);

// You can also update a single field with: await cityRef.UpdateAsync("Capital", false);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func updateDoc(ctx context.Context, client *firestore.Client) error {
 // ...

 _, err := client.Collection("cities").Doc("DC").Update(ctx, []firestore.Update{
     {
         Path:  "capital",
         Value: true,
     },
 })
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
// Update an existing document
DocumentReference docRef = db.collection("cities").document("DC");

// (async) Update one field
ApiFuture<WriteResult> future = docRef.update("capital", true);

// ...
WriteResult result = future.get();
System.out.println("Write result: " + result);
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const cityRef = db.collection('cities').doc('DC');

// Set the 'capital' field of the city
const res = await cityRef.update({capital: true});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('DC');
$cityRef->update([
    ['path' => 'capital', 'value' => true]
]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("cities").document("DC")

# Set the capital field
city_ref.update({"capital": True})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/DC"
city_ref.update({ capital: true })
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
