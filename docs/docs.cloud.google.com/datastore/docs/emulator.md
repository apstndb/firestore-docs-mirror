The [Google Cloud CLI](/sdk) provides a local, in-memory emulator for Firestore that you can use to test your Firestore in Datastore mode application. You can use the emulator with all Datastore mode client libraries. You should use the emulator only for local testing.

Use the `  gcloud emulators firestore  ` with `  --database-mode=datastore-mode  ` to test Firestore in Datastore mode behavior.

Don't use the emulator for production deployments. Because the emulator stores data only in memory, it doesn't persist data across runs.

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
    gcloud emulators firestore start --database-mode=datastore-mode
    ```
    
    The emulator prints the host and port number where it is running.
    
    By default, the emulator attempts to use `  127.0.0.1:8080  ` . To bind the emulator to a specific host and port, use the optional `  --host-port  ` flag, replacing HOST and PORT :
    
    ``` text
    gcloud emulators firestore start --database-mode=datastore-mode --host-port=HOST:PORT
    ```

2.  Use the keyboard shortcut `  Control + C  ` to stop the emulator.

**Note:** The default port for the emulator is `  8080  ` . This differs from the legacy Cloud Datastore emulator which used default port `  8081  ` .

## Connect to the emulator

To connect a client library and app to the emulator, set the `  DATASTORE_EMULATOR_HOST  ` environment variable. When this environment variable is set, the client libraries automatically connect to the emulator.

``` text
export DATASTORE_EMULATOR_HOST="HOST:PORT"
```

## Import entities into the emulator

The emulator's import feature lets you load entities from a set of entity export files into the emulator. The entity export files can come from an export of your Datastore mode database or from an emulator instance.

You can import entities into the emulator in two ways. The first is to add the flag `  import-data  ` to your emulator start command. The second method is to send a POST import request to the emulator. You can use [curl](https://curl.haxx.se/) or a similar tool. Refer to the following examples.

### Protocol

``` bash
curl -X POST http://localhost:8080/emulator/v1/projects/PROJECT_ID:import \
-H 'Content-Type: application/json' \
-d '{"database":"DATABASE", "export_directory":"EXPORT_DIRECTORY"}'
```

Modify `  localhost:8080  ` if the emulator uses a different port.

### CLI Flag

``` bash
gcloud emulators firestore start --database-mode=datastore-mode --import-data=EXPORT_DIRECTORY
```

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [DATABASE]  ` is the database path. For example a project with default database would look like the following:
    
    `  {"database":"projects/myProject/databases/"}  `

  - `  [EXPORT_DIRECTORY]  ` is the path to the `  overall_export_metadata  ` file of your entity export files. For example:
    
    `  {"export_directory":"/home/user/myexports/2024-03-26T19:39:33_443/2024-03-26T19:39:33_443.overall_export_metadata"}  `

**Note:** Exporting entities of specific kinds or namespaces is not supported.

## Export entities in the emulator

The emulator's export feature lets you save entities in the emulator into a set of entity export files. You can then use an import operation to load the entities in the entity export files into your Datastore mode database or into an emulator instance.

You can export entities from the emulator in two ways. The first is to add the flag `  export-on-exit  ` to your emulator start command. The second method is to send a `  POST  ` export request to the emulator. You can use [curl](https://curl.haxx.se/) or a similar tool. Refer to the following examples.

### Protocol

``` bash
curl -X POST http://localhost:8080/emulator/v1/projects/PROJECT_ID:export \
-H 'Content-Type: application/json' \
-d '{"database":"DATABASE_PATH", "export_directory":"EXPORT_DIRECTORY"}'
```

Modify `  localhost:8080  ` if the emulator uses a different port.

### CLI Flag

``` bash
gcloud emulators firestore start --database-mode=datastore-mode --export-on-exit=EXPORT_DIRECTORY
```

where:

  - `  [PROJECT_ID]  ` is the ID of your project.

  - `  [DATABASE_PATH]  ` is the database path. For example a project with default database would look like the following:
    
    `  {"database":"projects/myProject/databases/"}  `

  - `  [EXPORT_DIRECTORY]  ` specifies the directory where the emulator saves the entity export files. This directory must not already contain a set of entity export files. For example:
    
    `  {"export_directory":"/home/user/myexports/2024-03-26/"}  `

**Note:** Exporting entities of specific kinds or namespaces is not supported.

## Persist data in the emulator

By default, the Firestore emulator does not persist data to disk. To persist emulator data, run the following command to use import and export flags to load and save the data across emulator instances:

``` text
gcloud emulators firestore start --database-mode=datastore-mode --import-data=EXPORT_DIRECTORY --export-on-exit=EXPORT_DIRECTORY
```

## Reset emulator data

The Firestore emulator includes a REST endpoint for resetting all the data in the emulator. You can use this endpoint to clear data between tests without shutting down the emulator.

To reset all the data in the emulator, perform an HTTP `  POST  ` operation against the following endpoint, replacing HOST and PORT with the host and port you selected and replacing PROJECT\_ID with your own project ID:

``` text
http://HOST:PORT/reset
```

Adjust the host and port if the emulator does not use `  127.0.0.1:8080  ` . Your code should await REST confirmation that the reset finished or failed.

You can perform this operation from the shell using `  curl  ` :

``` text
$ curl -X POST "http://HOST:PORT/reset"
```

## How the emulator differs from production

The emulator attempts to faithfully replicate the behavior of the production service with some notable limitations.

### Concurrency and consistency

The emulator supports only pessimistic concurrency and strong consistency. The emulator does not support optimistic concurrency and eventual consistency settings.

### Transactions

The emulator doesn't attempt to mimic the transaction behavior that's seen in production. It uses a simple locking approach and doesn't attempt to mirror the various concurrency modes offered in the production environment.

When you're testing features that involve multiple concurrent writes to one document, the emulator might be slow to complete write requests. It might take up to 30 seconds for the emulator to release the locks. If you need to adjust the test timeout intervals, then do so.

The emulator doesn't also attempt to mimic all of the [production limits](/firestore/quotas#writes_and_transactions) , such as timeouts & size limits, which involve transactions. If you test features that depend on these production limits, then we recommend that you use a production environment instead of an emulator.

### Indexes

The emulator does not track composite indexes and instead executes any valid query. Make sure to test your app against a real Datastore mode instance to determine which indexes you require.

### Limits

The emulator does not enforce all limits enforced in production. For example, the emulator may allow transactions that would be rejected as too large by the production service. Make sure that you are familiar with the [documented limits](/datastore/docs/concepts/limits) and that you design your app to proactively avoid them.

## What's next

  - Learn how to work with [Entities, properties, and keys](/datastore/docs/concepts/entities)
  - Learn about [queries](/datastore/docs/concepts/queries)
