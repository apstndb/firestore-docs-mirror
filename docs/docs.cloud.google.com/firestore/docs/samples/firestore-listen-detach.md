Unsubscribe from a Firestore watch listener

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get real-time updates](https://docs.cloud.google.com/firestore/native/docs/query-data/listen)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    await listener.StopAsync();

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // Сontext with timeout stops listening to changes.
    ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
    defer cancel()

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query query = db.collection("cities");
    ListenerRegistration registration =
        query.addSnapshotListener(
            new EventListener<QuerySnapshot>() {
              // ...
            });
    
    // ...
    
    // Stop listening to changes
    registration.remove();

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const unsub = db.collection('cities').onSnapshot(() => {
    });
    
    // ...
    
    // Stop listening for changes
    unsub();

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    # Terminate watch on a document
    doc_watch.unsubscribe()

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    listener.stop

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
