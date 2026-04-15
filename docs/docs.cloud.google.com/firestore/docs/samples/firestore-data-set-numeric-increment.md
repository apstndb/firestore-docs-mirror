Update a Firestore document field using Increment. If a field doesn't exist, Firestore creates the field, and then increments it.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference washingtonRef = db.Collection("cities").Document("DC");
    
    // Atomically increment the population of the city by 50.
    await washingtonRef.UpdateAsync("Regions", FieldValue.Increment(50));

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "fmt"
    
     "cloud.google.com/go/firestore"
    )
    
    // updateDocumentIncrement increments the population of the city document in the
    // cities collection by 50.
    func updateDocumentIncrement(projectID, city string) error {
     // projectID := "my-project"
    
     ctx := context.Background()
    
     client, err := firestore.NewClient(ctx, projectID)
     if err != nil {
         return fmt.Errorf("firestore.NewClient: %w", err)
     }
     defer client.Close()
    
     dc := client.Collection("cities").Doc(city)
     _, err = dc.Update(ctx, []firestore.Update{
         {Path: "population", Value: firestore.Increment(50)},
     })
     if err != nil {
         return fmt.Errorf("Update: %w", err)
     }
    
     return nil
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference washingtonRef = db.collection("cities").document("DC");
    
    // Atomically increment the population of the city by 50.
    final ApiFuture<WriteResult> updateFuture =
        washingtonRef.update("population", FieldValue.increment(50));

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // ...
    const washingtonRef = db.collection('cities').doc('DC');
    
    // Atomically increment the population of the city by 50.
    const res = await washingtonRef.update({
      population: FieldValue.increment(50)
    });

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $cityRef = $db->collection('samples/php/cities')->document('DC');
    
    // Atomically increment the population of the city by 50.
    $cityRef->update([
        ['path' => 'regions', 'value' => FieldValue::increment(50)]
    ]);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    washington_ref = db.collection("cities").document("DC")
    
    washington_ref.update({"population": firestore.Increment(50)})

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    city_ref = firestore.doc "#{collection_path}/DC"
    city_ref.update({ population: firestore.field_increment(50) })

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
