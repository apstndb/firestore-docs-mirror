Update a Firestore document containing an array field.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference washingtonRef = db.Collection("cities").Document("DC");

// Atomically add a new region to the "regions" array field.
await washingtonRef.UpdateAsync("Regions", FieldValue.ArrayUnion("greater_virginia"));

// Atomically remove a region from the "regions" array field.
await washingtonRef.UpdateAsync("Regions", FieldValue.ArrayRemove("east_coast"));
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
DocumentReference washingtonRef = db.collection("cities").document("DC");

// Atomically add a new region to the "regions" array field.
ApiFuture<WriteResult> arrayUnion =
    washingtonRef.update("regions", FieldValue.arrayUnion("greater_virginia"));
System.out.println("Update time : " + arrayUnion.get());

// Atomically remove a region from the "regions" array field.
ApiFuture<WriteResult> arrayRm =
    washingtonRef.update("regions", FieldValue.arrayRemove("east_coast"));
System.out.println("Update time : " + arrayRm.get());
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// ...
const washingtonRef = db.collection('cities').doc('DC');

// Atomically add a new region to the "regions" array field.
const unionRes = await washingtonRef.update({
  regions: FieldValue.arrayUnion('greater_virginia')
});
// Atomically remove a region from the "regions" array field.
const removeRes = await washingtonRef.update({
  regions: FieldValue.arrayRemove('east_coast')
});

// To add or remove multiple items, pass multiple arguments to arrayUnion/arrayRemove
const multipleUnionRes = await washingtonRef.update({
  regions: FieldValue.arrayUnion('south_carolina', 'texas')
  // Alternatively, you can use spread operator in ES6 syntax
  // const newRegions = ['south_carolina', 'texas']
  // regions: FieldValue.arrayUnion(...newRegions)
});
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$cityRef = $db->collection('samples/php/cities')->document('DC');

// Atomically add a new region to the "regions" array field.
$cityRef->update([
    ['path' => 'regions', 'value' => FieldValue::arrayUnion(['greater_virginia'])]
]);

// Atomically remove a region from the "regions" array field.
$cityRef->update([
    ['path' => 'regions', 'value' => FieldValue::arrayRemove(['east_coast'])]
]);
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
city_ref = db.collection("cities").document("DC")

# Atomically add a new region to the 'regions' array field.
city_ref.update({"regions": firestore.ArrayUnion(["greater_virginia"])})

# // Atomically remove a region from the 'regions' array field.
city_ref.update({"regions": firestore.ArrayRemove(["east_coast"])})
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
city_ref = firestore.doc "#{collection_path}/DC"

# Atomically add a new region to the 'regions' array field.
city_ref.update({ regions: firestore.field_array_union("greater_virginia") })

# Atomically remove a region from the 'regions' array field.
city_ref.update({ regions: firestore.field_array_delete("east_coast") })
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
