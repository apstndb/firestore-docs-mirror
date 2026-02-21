# Build presence in apps with Cloud Functions

Depending on the type of app you're building, you might find it useful to detect which of your users or devices are actively online — otherwise known as detecting "presence."

For example, if you're building an app like a social network or deploying a fleet of IoT devices, you could use this information to display a list of friends that are online and free to chat, or sort your IoT devices by "last seen."

Firestore doesn't natively support presence, but you can leverage other Firebase products to build a presence system.

## Solution: Cloud Functions with Realtime Database

To connect Firestore to Firebase Realtime Database's native presence feature, use Cloud Functions.

Use Realtime Database to report connection status, then use Cloud Functions to mirror that data into Firestore.

### Using presence in Realtime Database

First, consider how a traditional presence system works in Realtime Database.

### Web

``` javascript
// Fetch the current user's ID from Firebase Authentication.
var uid = firebase.auth().currentUser.uid;

// Create a reference to this user's specific status node.
// This is where we will store data about being online/offline.
var userStatusDatabaseRef = firebase.database().ref('/status/' + uid);

// We'll create two constants which we will write to 
// the Realtime database when this device is offline
// or online.
var isOfflineForDatabase = {
    state: 'offline',
    last_changed: firebase.database.ServerValue.TIMESTAMP,
};

var isOnlineForDatabase = {
    state: 'online',
    last_changed: firebase.database.ServerValue.TIMESTAMP,
};

// Create a reference to the special '.info/connected' path in 
// Realtime Database. This path returns `true` when connected
// and `false` when disconnected.
firebase.database().ref('.info/connected').on('value', function(snapshot) {
    // If we're not currently connected, don't do anything.
    if (snapshot.val() == false) {
        return;
    };

    // If we are currently connected, then use the 'onDisconnect()' 
    // method to add a set which will only trigger once this 
    // client has disconnected by closing the app, 
    // losing internet, or any other means.
    userStatusDatabaseRef.onDisconnect().set(isOfflineForDatabase).then(function() {
        // The promise returned from .onDisconnect().set() will
        // resolve as soon as the server acknowledges the onDisconnect() 
        // request, NOT once we've actually disconnected:
        // https://firebase.google.com/docs/reference/js/firebase.database.OnDisconnect

        // We can now safely set ourselves as 'online' knowing that the
        // server will mark us as offline once we lose connection.
        userStatusDatabaseRef.set(isOnlineForDatabase);
    });
});index.js
```

This example is a complete Realtime Database presence system. It handles multiple disconnections, crashes and so on.

### Connecting to Firestore

To implement a similar solution in Firestore use the same Realtime Database code, then use Cloud Functions to keep Realtime Database and Firestore in sync.

If you haven't already, add [Realtime Database](https://firebase.google.com/docs/database/) to your project and include the above presence solution.

Next you'll synchronize the presence state to Firestore through the following methods:

1.  Locally, to the offline device's Firestore cache so that the app knows it's offline.
2.  Globally, using a Cloud Function so that all other devices accessing Firestore know this specific device is offline.

**Note:** Remember that whenever you lose internet connectivity, you have no way to synchronize data, so you must write the same data to the same location, as shown in the following examples. This is necessary to ensure all devices receive the change in online status.

The functions recommended in this tutorial **cannot run in a client app** . They must be deployed to Cloud Functions for Firebase, and they require server-side logic from the Firebase Admin SDK. For detailed guidance, see the [Cloud Functions documentation](https://firebase.google.com/docs/functions/get-started?gen=2nd) .

#### Updating Firestore's local cache

Let's take a look at the changes required to fulfill the first issue - updating Firestore's local cache.

### Web

``` javascript
// ...
var userStatusFirestoreRef = firebase.firestore().doc('/status/' + uid);

// Firestore uses a different server timestamp value, so we'll 
// create two more constants for Firestore state.
var isOfflineForFirestore = {
    state: 'offline',
    last_changed: firebase.firestore.FieldValue.serverTimestamp(),
};

var isOnlineForFirestore = {
    state: 'online',
    last_changed: firebase.firestore.FieldValue.serverTimestamp(),
};

firebase.database().ref('.info/connected').on('value', function(snapshot) {
    if (snapshot.val() == false) {
        // Instead of simply returning, we'll also set Firestore's state
        // to 'offline'. This ensures that our Firestore cache is aware
        // of the switch to 'offline.'
        userStatusFirestoreRef.set(isOfflineForFirestore);
        return;
    };

    userStatusDatabaseRef.onDisconnect().set(isOfflineForDatabase).then(function() {
        userStatusDatabaseRef.set(isOnlineForDatabase);

        // We'll also add Firestore set here for when we come online.
        userStatusFirestoreRef.set(isOnlineForFirestore);
    });
});index.js
```

With these changes we've now ensured that the *local* Firestore state will always reflect the online/offline status of the device. This means you can listen to the `  /status/{uid}  ` document and use the data to change your UI to reflect connection status.

### Web

``` javascript
userStatusFirestoreRef.onSnapshot(function(doc) {
    var isOnline = doc.data().state == 'online';
    // ... use isOnline
});index.js
```

#### Updating Firestore globally

Although our application correctly reports online presence to itself, this status will not be accurate in other Firestore apps yet because our "offline" status write is local only and won't be synced up when a connection is restored. To counter this, we'll use a Cloud Function which watches the `  status/{uid}  ` path in Realtime Database. When the Realtime Database value changes the value will sync to Firestore so that all users' statuses are correct.

### Node.js

``` javascript
firebase.firestore().collection('status')
    .where('state', '==', 'online')
    .onSnapshot(function(snapshot) {
        snapshot.docChanges().forEach(function(change) {
            if (change.type === 'added') {
                var msg = 'User ' + change.doc.id + ' is online.';
                console.log(msg);
                // ...
            }
            if (change.type === 'removed') {
                var msg = 'User ' + change.doc.id + ' is offline.';
                console.log(msg);
                // ...
            }
        });
    });index.js
```

Once you deploy this function, you'll have a complete presence system running with Firestore. Below is an example of monitoring for any users who come online or go offline using a `  where()  ` query.

### Web

``` javascript
firebase.firestore().collection('status')
    .where('state', '==', 'online')
    .onSnapshot(function(snapshot) {
        snapshot.docChanges().forEach(function(change) {
            if (change.type === 'added') {
                var msg = 'User ' + change.doc.id + ' is online.';
                console.log(msg);
                // ...
            }
            if (change.type === 'removed') {
                var msg = 'User ' + change.doc.id + ' is offline.';
                console.log(msg);
                // ...
            }
        });
    });index.js
```

## Limitations

Using Realtime Database to add presence to your Firestore app is scalable and effective but has some limitations:

  - **Debouncing** - when listening to realtime changes in Firestore, this solution is likely to trigger multiple changes. If these changes trigger more events than you want, manually debounce the Firestore events.
  - **Connectivity** - this implementation measures connectivity to Realtime Database, not to Firestore. If the connection status to each database is not the same, this solution might report an incorrect presence state.
  - **Android** - on Android, the Realtime Database disconnects from the backend after 60 seconds of inactivity. Inactivity means no open listeners or pending operations. To keep the connection open, we recommended you add a value event listener to a path besides `  .info/connected  ` . For example you could do `  FirebaseDatabase.getInstance().getReference((new Date()).toString()).keepSynced()  ` at the start of each session. For more information, see [Detecting Connection State](https://firebase.google.com/docs/database/android/offline-capabilities#section-connection-state) .
