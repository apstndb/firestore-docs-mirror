# Use Firestore emulator locally

The [Google Cloud CLI](/sdk) provides a local, in-memory emulator for Firestore that you can use to test your application. You can use the emulator with all Firestore client libraries. You should use the emulator only for local testing.

Do not use the emulator for production deployments. Because the emulator stores data only in memory, it will not persist data across runs.

**Tip:** The instructions on this page show you how to run the Firestore emulator using the gcloud CLI. The same Firestore emulator is also available through the [Firebase Local Emulator Suite](https://firebase.google.com/docs/emulator-suite#what-is-emulator-suite) . The emulator suite bundles several emulators and helps you test these services together. To access the Firestore emulator through the emulator suite, see [Introduction to Firebase Local Emulator Suite](https://firebase.google.com/docs/emulator-suite) .

## Install the emulator

**Note:** The Firestore emulator will be updated to require Java 21 in the upcoming Google Cloud CLI release 528.0.0. Upgrade to Java 21 or later to continue using the latest version of the emulator.

To install the Firestore emulator, install and update the gcloud CLI:

1.  [Install the gcloud CLI](/sdk/docs/install) .

2.  Update your gcloud CLI installation to get the latest features:
    
    ``` text
    gcloud components update
    ```

## Run the emulator

1.  Run the following command to start the emulator:
    
    ``` text
    gcloud emulators firestore start
    ```
    
    The emulator prints the host and port number where it is running.
    
    By default, the emulator attempts to use `  127.0.0.1:8080  ` . To bind the emulator to a specific host and port, use the optional `  --host-port  ` flag, replacing HOST and PORT :
    
    ``` text
    gcloud emulators firestore start --host-port=HOST:PORT
    ```

2.  Type `  Control + C  ` to stop the emulator. The emulator may also be stopped with a POST to `  /shutdown  ` . For example:
    
    ``` text
    curl -d '' HOST:PORT/shutdown
    ```

## Connect to the emulator

How you connect to the emulator depends on the type of client library, server client library, or mobile/web SDK.

### Server client libraries

To connect a Firestore server client library (C\#, Go, Java, Node.js, PHP, Python, and Ruby), set the `  FIRESTORE_EMULATOR_HOST  ` environment variable. When this environment variable is set, the server client libraries automatically connect to the emulator.

``` text
export FIRESTORE_EMULATOR_HOST="HOST:PORT"
```

### Android, Apple platforms, and Web SDKs

The following examples demonstrate how to connect the Android, Apple platforms, and Web SDKs to the Firestore emulator:

##### Android

``` text
// 10.0.2.2 is the special IP address to connect to the 'localhost' of
// the host computer from an Android emulator.
FirebaseFirestore firestore = FirebaseFirestore.getInstance();
firestore.useEmulator("10.0.2.2", 8080);

FirebaseFirestoreSettings settings = new FirebaseFirestoreSettings.Builder()
        .setPersistenceEnabled(false)
        .build();
firestore.setFirestoreSettings(settings);EmulatorSuite.java
```

##### Swift

``` text
let settings = Firestore.firestore().settings
settings.host = "127.0.0.1:8080"
settings.cacheSettings = MemoryCacheSettings()
settings.isSSLEnabled = false
Firestore.firestore().settings = settingsViewController.swift
```

### Web version 9

``` javascript
import { getFirestore, connectFirestoreEmulator } from "firebase/firestore";

// firebaseApps previously initialized using initializeApp()
const db = getFirestore();
connectFirestoreEmulator(db, '127.0.0.1', 8080);fs_emulator_connect.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
// Firebase previously initialized using firebase.initializeApp().
var db = firebase.firestore();
if (location.hostname === "localhost") {
  db.useEmulator("127.0.0.1", 8080);
}emulator-suite.js
```

The Firestore in Native Mode emulator clears database contents when shut down. Since the offline cache of the Firestore SDK is not automatically cleared, you may want to disable local persistence in your emulator configuration to avoid discrepancies between the emulated database and local caches; in the Web SDK, persistence is disabled by default.

## Clear emulator data

The Firestore emulator includes a REST endpoint for deleting all the data currently in the emulator. You can use this endpoint to clear data between tests without shutting down the emulator.

To delete all data in the emulator, perform an HTTP `  DELETE  ` operation against the following endpoint, replacing HOST and PORT with the host and port you selected and replacing PROJECT\_ID with your own project ID:

``` text
http://HOST:PORT/emulator/v1/projects/PROJECT_ID/databases/(default)/documents
```

Adjust the host and port if the emulator does not use `  127.0.0.1:8080  ` . Your code should await REST confirmation that the deletion finished or failed.

You can perform this operation from the shell using `  curl  ` :

``` text
$ curl -v -X DELETE "http://HOST:PORT/emulator/v1/projects/PROJECT_ID/databases/(default)/documents"
```

## How the Firestore emulator differs from production

The Firestore emulator attempts to faithfully replicate the behavior of the production service with some notable limitations.

### Transactions

The emulator doesn't attempt to mimic the transaction behavior that's seen in production. It uses a simple locking approach and doesn't attempt to mirror the various concurrency modes offered in the production environment.

When you're testing features that involve multiple concurrent writes to one document, the emulator might be slow to complete write requests. It might take up to 30 seconds for the emulator to release the locks. If you need to adjust the test timeout intervals, then do so.

The emulator doesn't also attempt to mimic all of the [production limits](/firestore/quotas#writes_and_transactions) , such as timeouts & size limits, which involve transactions. If you test features that depend on these production limits, then we recommend that you use a production environment instead of an emulator.

### Indexes

The emulator does not track composite indexes and will instead execute any valid query. Make sure to test your app against a real Firestore instance to determine which indexes you require.

### Limits

The emulator does not enforce all limits enforced in production. For example, the emulator may allow transactions that would be rejected as too large by the production service. Make sure you are familiar with the [documented limits](/firestore/docs/quotas) and that you design your app to proactively avoid them.
