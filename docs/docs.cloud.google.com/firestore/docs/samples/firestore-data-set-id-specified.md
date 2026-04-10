Add a Firestore document

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    await db.Collection("cities").Document("new-city-id").SetAsync(city);

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "log"
    
     "cloud.google.com/go/firestore"
    )
    
    func addDocWithID(ctx context.Context, client *firestore.Client) error {
     var data = make(map[string]interface{})
    
     _, err := client.Collection("cities").Doc("new-city-id").Set(ctx, data)
     if err != nil {
         // Handle any errors in an appropriate way, such as returning them.
         log.Printf("An error has occurred: %s", err)
     }
    
     return err
    }

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    db.collection("cities").document("new-city-id").set(data);

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    await db.collection('cities').doc('new-city-id').set(data);

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $db->collection('samples/php/cities')->document('new-city-id')->set($data);

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    db.collection("cities").document("new-city-id").set(data)

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    city_ref = firestore.doc "#{collection_path}/new-city-id"
    city_ref.set data

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
