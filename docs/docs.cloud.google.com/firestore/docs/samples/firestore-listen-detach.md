Unsubscribe from a Firestore watch listener

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Get real-time updates](/firestore/native/docs/query-data/listen)
  - [Get realtime updates with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/listen)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
await listener.StopAsync();
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// Сontext with timeout stops listening to changes.
ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
defer cancel()
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query query = db.collection("cities");
ListenerRegistration registration =
    query.addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          // ...
        });

// ...

// Stop listening to changes
registration.remove();
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const unsub = db.collection('cities').onSnapshot(() => {
});

// ...

// Stop listening for changes
unsub();
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Terminate watch on a document
doc_watch.unsubscribe()
```

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
listener.stop
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
