**Note:** This content applies to the emulator for legacy Cloud Datastore. To emulate Firestore in Datastore mode, [use `  gcloud emulators firestore start --database-mode=datastore-mode  `](/datastore/docs/emulator) instead.

The Datastore emulator provides local emulation of the production Datastore environment. You can use the emulator to develop and test your application locally. In addition, the emulator can help you generate indexes for your production Datastore instance and delete unneeded indexes. This page guides you through installing the emulator, starting the emulator, and setting environment variables to connect your application to the emulator.

**Note:** To access the emulator from App Engine, see [Using the Local Development Server](/appengine/docs/standard/python/tools/using-local-server#using_the_local_datastore) .

## Known issues

By default, the Datastore emulator does not emulate [features introduced by Firestore in Datastore mode](/datastore/docs/firestore-or-datastore#in_datastore_mode) . The following default emulator behaviors do not match Datastore mode:

  - The emulator simulates eventual consistency, by default. Firestore in Datastore mode is strongly consistent.
  - The emulator does not allow non-ancestor queries within transactions. Firestore in Datastore mode no longer has this limitation.
  - The emulator does not support `  IN  ` , `  !=  ` , and `  NOT-IN  ` queries.
  - The emulator does not support aggregation queries like `  COUNT(*)  ` .

However, the [--use-firestore-in-datastore-mode](/sdk/gcloud/reference/beta/emulators/datastore/start) flag helps loosen some of the restrictions above for Firestore in Datastore Mode.

  - The emulator simulates strongly consistent non-ancestor queries.
  - The emulator allows for non-ancestor queries within transactions.
  - The emulator removes the limitation of 25 entity groups in a transaction.

To emulate Firestore in Datastore mode, [use `  gcloud emulators firestore start --database-mode=datastore-mode  `](/datastore/docs/emulator) instead.

## Before you begin

To use the Datastore emulator you need:

  - A Java JRE (version 21 or greater)
  - The [Google Cloud CLI](/sdk)
  - An application built using the [Google Cloud Client Libraries](/sdk/cloud-client-libraries)

## Installing the emulator

The Datastore emulator is a component of the gcloud CLI. Use the [`  gcloud components install  `](/sdk/gcloud/reference/components/install) command to install the Datastore emulator:

``` text
gcloud components install cloud-datastore-emulator
```

## Emulator data directories

The emulator simulates Datastore by creating `  /WEB-INF/appengine-generated/local_db.bin  ` in a specified data directory and storing data in `  local_db.bin  ` . By default, the emulator uses the data directory `  ~/.config/gcloud/emulators/datastore/  ` . The `  local_db.bin  ` file persists between sessions of the emulator. You can set up multiple data directories and think of each as a separate, local Datastore mode instance. To clear the contents of a `  local_db.bin  ` file, stop the emulator and manually delete the file.

## Starting the emulator

Start the emulator by executing [`  datastore start  `](/sdk/gcloud/reference/beta/emulators/datastore/start) from a command prompt:

``` text
gcloud beta emulators datastore start [flags]
```

where `  [flags]  ` are optional command-line arguments supplied to the gcloud CLI. For example:

  - [`  --data-dir=[DATA_DIR]  `](/sdk/gcloud/reference/beta/emulators/datastore/start) changes the emulator's data directory. The emulator creates the `  /WEB-INF/appengine-generated/local_db.bin  ` file inside `  [DATA_DIR]  ` or, if available, uses an existing file.

  - [`  --no-store-on-disk  `](/sdk/gcloud/reference/beta/emulators/datastore/start) configures the emulator not to persist any data to disk for the emulator session.

See the [`  gcloud beta emulators datastore start  `](/sdk/gcloud/reference/beta/emulators/datastore/start) reference for the full list of optional flags.

After you start the emulator, you should see a message similar to the following:

``` text
...
[datastore] Dev App Server is now running.
```

To stop the emulator, type Control-C at the command prompt.

## Setting environment variables

After you start the emulator, you need to set environment variables so that your application connects to the emulator instead of your production Datastore mode database. Set these environment variables on the same machine that you use to run your application.

You need to set the environment variables each time you start the emulator. The environment variables depend on dynamically assigned port numbers that could change when you restart the emulator.

**Note:** If you use the .NET client library, [use this method to read the environment variables and connect to the emulator](https://googleapis.github.io/google-cloud-dotnet/docs/Google.Cloud.Datastore.V1/#using-the-datastore-emulator) .

### Automatically setting the variables

If your application and the emulator run on the same machine, you can set the environment variables automatically:

### Linux / macOS

Run `  env-init  ` using command substitution:

``` text
$(gcloud beta emulators datastore env-init)
```

### Windows

Create and run a batch file using output from `  env-init  ` :

``` text
gcloud beta emulators datastore env-init > set_vars.cmd && set_vars.cmd
```

Your application will now connect to the Datastore emulator.

### Manually setting the variables

If your application and the emulator run on different machines, set the environment variables manually:

1.  Run the `  env-init  ` command:
    
    ``` text
    gcloud beta emulators datastore env-init
    ```

2.  On the machine that runs your application, set the environment variables and values as directed by the output of the `  env-init  ` command. For example:
    
    Linux / macOS
    
    ``` text
    export DATASTORE_DATASET=my-project-id
    export DATASTORE_EMULATOR_HOST=::1:8432
    export DATASTORE_EMULATOR_HOST_PATH=::1:8432/datastore
    export DATASTORE_HOST=http://::1:8432
    export DATASTORE_PROJECT_ID=my-project-id
    ```
    
    Windows
    
    ``` text
    set DATASTORE_DATASET=my-project-id
    set DATASTORE_EMULATOR_HOST=::1:8432
    set DATASTORE_EMULATOR_HOST_PATH=::1:8432/datastore
    set DATASTORE_HOST=http://::1:8432
    set DATASTORE_PROJECT_ID=my-project-id
    ```

Your application will now connect to the Datastore emulator. Note that the project id and port provided by the command will differ from the above example.

## Updating and deleting indexes

By running your application using the emulator, you can generate indexes for your production Datastore mode database, as well as delete unneeded indexes. Learn more at [Using the gcloud CLI](/datastore/docs/tools) .

## Removing environment variables

After you finish using the emulator, stop the emulator (Control-C) and remove the environment variables so your application will connect to your production Datastore mode database.

### Automatically removing the variables

If your application and the emulator run on the same machine, you can remove the environment variables automatically:

### Linux / macOS

Run `  env-unset  ` using command substitution:

``` text
$(gcloud beta emulators datastore env-unset)
```

### Windows

Create and run a batch file using output from `  env-unset  ` :

``` text
gcloud beta emulators datastore env-unset > remove_vars.cmd && remove_vars.cmd
```

Your application will now connect to your production Datastore mode database.

### Manually removing the variables

If your application and the emulator run on different machines, remove the environment variables manually:

1.  Run the `  env-unset  ` command:
    
    ``` text
    gcloud beta emulators datastore env-unset
    ```

2.  On the machine that runs your application, remove the environment variables as directed by the output of the `  env-unset  ` command. For example:
    
    Linux / macOS
    
    ``` text
    unset DATASTORE_DATASET
    unset DATASTORE_EMULATOR_HOST
    unset DATASTORE_EMULATOR_HOST_PATH
    unset DATASTORE_HOST
    unset DATASTORE_PROJECT_ID
    ```
    
    Windows
    
    ``` text
    set DATASTORE_DATASET=
    set DATASTORE_EMULATOR_HOST=
    set DATASTORE_EMULATOR_HOST_PATH=
    set DATASTORE_HOST=
    set DATASTORE_PROJECT_ID=
    ```

Your application will now connect to your production Datastore mode database.
