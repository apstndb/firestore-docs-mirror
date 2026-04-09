Add a Firestore document with nested fields

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference frankDocRef = db.Collection("users").Document("frank");
Dictionary<string, object> initialData = new Dictionary<string, object>
{
    { "Name", "Frank" },
    { "Age", 12 }
};

Dictionary<string, object> favorites = new Dictionary<string, object>
{
    { "Food", "Pizza" },
    { "Color", "Blue" },
    { "Subject", "Recess" },
};
initialData.Add("Favorites", favorites);
await frankDocRef.SetAsync(initialData);

// Update age and favorite color
Dictionary<string, object> updates = new Dictionary<string, object>
{
    { "Age", 13 },
    { "Favorites.Color", "Red" },
};

// Asynchronously update the document
await frankDocRef.UpdateAsync(updates);
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/firestore"
)

func updateDocNested(ctx context.Context, client *firestore.Client) error {
 initialData := map[string]interface{}{
     "name": "Frank",
     "age":  12,
     "favorites": map[string]interface{}{
         "food":    "Pizza",
         "color":   "Blue",
         "subject": "recess",
     },
 }

 // ...

 _, err := client.Collection("users").Doc("frank").Set(ctx, map[string]interface{}{
     "age": 13,
     "favorites": map[string]interface{}{
         "color": "Red",
     },
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
// Create an initial document to update
DocumentReference frankDocRef = db.collection("users").document("frank");
Map<String, Object> initialData = new HashMap<>();
initialData.put("name", "Frank");
initialData.put("age", 12);

Map<String, Object> favorites = new HashMap<>();
favorites.put("food", "Pizza");
favorites.put("color", "Blue");
favorites.put("subject", "Recess");
initialData.put("favorites", favorites);

ApiFuture<WriteResult> initialResult = frankDocRef.set(initialData);
// Confirm that data has been successfully saved by blocking on the operation
initialResult.get();

// Update age and favorite color
Map<String, Object> updates = new HashMap<>();
updates.put("age", 13);
updates.put("favorites.color", "Red");

// Async update document
ApiFuture<WriteResult> writeResult = frankDocRef.update(updates);
// ...
System.out.println("Update time : " + writeResult.get().getUpdateTime());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const initialData = {
  name: 'Frank',
  age: 12,
  favorites: {
    food: 'Pizza',
    color: 'Blue',
    subject: 'recess'
  }
};

// ...
const res = await db.collection('users').doc('Frank').update({
  age: 13,
  'favorites.color': 'Red'
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
// Create an initial document to update
$frankRef = $db->collection('samples/php/users')->document('frank');
$frankRef->set([
    'first' => 'Frank',
    'last' => 'Franklin',
    'favorites' => ['food' => 'Pizza', 'color' => 'Blue', 'subject' => 'Recess'],
    'age' => 12
]);

// Update age and favorite color
$frankRef->update([
    ['path' => 'age', 'value' => 13],
    ['path' => 'favorites.color', 'value' => 'Red']
]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Create an initial document to update
frank_ref = db.collection("users").document("frank")
frank_ref.set(
    {
        "name": "Frank",
        "favorites": {"food": "Pizza", "color": "Blue", "subject": "Recess"},
        "age": 12,
    }
)

# Update age and favorite color
frank_ref.update({"age": 13, "favorites.color": "Red"})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# Create an initial document to update
frank_ref = firestore.doc "#{collection_path}/frank"
frank_ref.set(
  {
    name:      "Frank",
    favorites: {
      food:    "Pizza",
      color:   "Blue",
      subject: "Recess"
    },
    age:       12
  }
)

# Update age and favorite color
frank_ref.update({ age: 13, "favorites.color": "Red" })
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
