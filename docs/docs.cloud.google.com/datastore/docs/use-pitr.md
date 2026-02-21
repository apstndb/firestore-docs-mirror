This page describes how to use point-in-time recovery (PITR) to retain and recover data in Firestore in Datastore mode.

To understand PITR concepts, see [Point-in-time recovery](/datastore/docs/pitr) .

## Permissions

To get the permissions that you need to manage PITR settings, ask your administrator to grant you the [Cloud Datastore Owner](/iam/docs/roles-permissions/firestore#datastore.owner) ( `  roles/datastore.owner  ` ) IAM role on the project whose PITR settings you want to enable. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to manage PITR settings. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to manage PITR settings:

  - To enable PITR when creating a database: `  datastore.databases.create  `
  - To update PITR settings on existing database: `  datastore.databases.update  ` , `  datastore.databases.list  `
  - To perform reads from PITR data: `  datastore.databases.get  ` , `  datastore.entities.get  ` , `  datastore.entities.list  ` , `  datastore.namespaces.get  ` , `  datastore.namespaces.list  ` , `  datastore.statistics.get  ` , `  datastore.statistics.list  `
  - To export PITR data: `  datastore.databases.export  `
  - To import PITR data: `  datastore.databases.import  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Before you begin

Note the following points before you start using PITR:

  - You can't start reading from seven days in the past immediately after you enable PITR.
  - If you want to enable PITR when you create a database, you must use the `  gcloud firestore databases create  ` command. Enabling PITR while creating a database using the Google Cloud console is not supported.
  - Datastore mode starts retaining versions from the point forward after enabling PITR.
  - You cannot read PITR data in the PITR window after you disable PITR.
  - If you re-enable PITR immediately after disabling it, the past PITR data is no longer available. Any PITR data created before disabling PITR will be deleted after the PITR expiration date.
  - If you accidentally deleted data in the last hour and PITR is disabled, you can restore your data by enabling PITR within one hour of deletion.
  - Any read performed on expired PITR data fails.

## Enable PITR

Before using PITR, [enable billing for your Google Cloud project](/billing/docs/how-to/modify-project#enable_billing_for_a_project) . Only Google Cloud projects with billing enabled can use the PITR feature.

To enable PITR for your database:

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Disaster Recovery** .

4.  Click **Edit** to edit the settings.

5.  Select the **Enable point-in-time recovery** checkbox, and then click **Save** .

Enabling PITR would incur storage costs. See [Pricing](https://cloud.google.com/datastore/pricing) for more information.

To disable PITR, clear the **Enable point-in-time recovery** checkbox from the Disaster Recovery page in the Google Cloud console.

### gcloud

Enable PITR during database creation with the [`  gcloud firestore databases create  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/create) command as follows:

``` text
gcloud firestore databases create\
  --location=LOCATION\
  [--database=DATABASE_ID; default="(default)"]\
  [--type=TYPE; default="firestore-native"]\
  --enable-pitr
```

Replace the values as follows:

  - `  LOCATION  ` - location where you want to create your database.
  - `  DATABASE_ID  ` - set to the database ID or (default).
  - `  TYPE  ` - set to datastore-mode.

You can disable PITR using the [`  gcloud firestore databases update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command as follows:

``` text
gcloud firestore databases update\
  [--database=DATABASE_ID; default="(default)"]\
  --no-enable-pitr
```

Replace the values as follows:

  - `  DATABASE_ID  ` - set to the database ID or (default).

## Get the retention period and earliest version time

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Disaster Recovery** .

4.  In the **Settings** section, note the **Retention period** and **Earliest version time** .
    
      - **Retention period** : the period in which Datastore mode retains all versions of data for the database. The value is one hour when PITR is disabled and seven days when PITR is enabled.
      - **Earliest version time** : the earliest timestamp at which earlier versions of the data can be read in the PITR window. This value is continuously updated by Datastore mode and becomes stale the moment it is queried. If you are using this value to recover data, make sure to account for the time from the moment w̦hen the value is queried to the moment when you initiate the recovery.
      - **Point-in-time recovery** : shows `  Enabled  ` , if PITR is enabled. If PITR is disabled, you will see `  Disabled  ` .

### gcloud

Run the [gcloud firestore databases describe](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/describe) command as follows:

``` text
gcloud firestore databases describe --database=DATABASE_ID
```

Replace `  DATABASE_ID  ` with the database ID or `  (default)  ` .

Here's the output:

``` text
    appEngineIntegrationMode: ENABLED
    concurrencyMode: PESSIMISTIC
    createTime: '2021-03-24T17:02:35.234Z'
    deleteProtectionState: DELETE_PROTECTION_DISABLED
    earliestVersionTime: '2023-06-12T16:17:25.222474Z'
    etag: IIDayqOevv8CMNTvyNK4uv8C
    keyPrefix: s
    locationId: nam5
    name: projects/PROJECT_ID/databases/(default)
    pointInTimeRecoveryEnablement: POINT_IN_TIME_RECOVERY_DISABLED
    type: DATASTORE_MODE
    uid: 5230c382-dcd2-468f-8cb3-2a1acfde2b32
    updateTime: '2021-11-17T17:48:22.171180Z'
    versionRetentionPeriod: 3600s
```

where,

  - `  earliestVersionTime  ` - timestamp of the earliest PITR data stored.
  - `  pointInTimeRecoveryEnablement  ` : shows `  POINT_IN_TIME_RECOVERY_ENABLED  ` , if PITR is enabled. If PITR is disabled, you will either see `  POINT_IN_TIME_RECOVERY_DISABLED  ` or the `  pointInTimeRecoveryEnablement  ` field might not be displayed.
  - `  versionRetentionPeriod  ` - time period for which PITR data is retained in milliseconds. The value can be one hour when PITR is disabled or seven days if PITR is enabled.

## Read PITR data

You can read PITR data using the client libraries, REST API methods, or FirestoreIO Apache Beam connector.

### Client libraries

**Note:** You can read from PITR data in the server client libraries, namely Go, Java, Node.js, PHP, and Python.

### Java

You must use the `  readTime  ` method in the `  ReadOption  ` class to read PITR data. You cannot use the `  ReadOnly  ` transaction to perform reads. See [ReadOption](https://github.com/googleapis/java-datastore/blob/main/google-cloud-datastore/src/main/java/com/google/cloud/datastore/ReadOption.java) sample code, for more information.

``` text
  Datastore datastore = ...
  Timestamp timestamp = ...

  // lookup
  Key key = ...
  Entity entity = datastore.get(key, ReadOption.readTime(timestamp));

  // runQuery
  Query<Entity> query = ...
  QueryResults<Entity> queryResult = datastore.run(query, ReadOption.readTime(timestamp));

  // runAggregationQuery
  AggregationQuery countAggregationQuery = ...
  Long count = getOnlyElement(datastore.runAggregation(countAggregationQuery, ReadOption.readTime(timestamp))).get("total_count");
```

For a complete list of `  readTime  ` examples, see the [GitHub repository](https://github.com/googleapis/java-datastore/blob/main/google-cloud-datastore/src/test/java/com/google/cloud/datastore/it/ITDatastoreTest.java) .

### Python

Use PITR read in Datastore mode Python SDK using the `  readTime  ` method or use the `  ReadOnly  ` transaction with `  readTime  ` to perform reads.

``` text
  from datetime import datetime, timezone

  read_time = datetime.now(tz=timezone.utc)

  key = …
  # read without PITR read time
  entity = client.get(key)

  # read with PITR read time
  entity = client.get(key, read_time=read_time)

  # PITR read using read_only transaction
  with client.transaction(read_only=True, read_time=read_time):
      entity = client.get(key)

  query = client.query…
  # run query without PITR read time
  iterator = query.fetch()

  # run query with PITR read time
  iterator = query.fetch(read_time=read_time)

  # PITR read query using read_only transaction
  with client.transaction(read_only=True, read_time=read_time):
      iterator = query.fetch()
```

For a complete list of `  readTime  ` examples, see the [GitHub](https://github.com/googleapis/python-datastore/blob/main/tests/system/test_read_consistency.py) repository.

### REST API

PITR reads are supported in the Datastore mode V1 read methods, which are [lookup](/datastore/docs/reference/data/rest/v1/projects/lookup) , [runQuery](/datastore/docs/reference/data/rest/v1/projects/runQuery) , and [runAggregationQuery](/datastore/docs/reference/data/rest/v1/projects/runAggregationQuery) .

To perform a read using the REST methods, try one of the following options:

1.  In the your read method request, pass the `  readTime  ` value as a supported PITR timestamp in the `  readOptions  ` method. A PITR timestamp can be either a microsecond precision timestamp within the past hour or a whole minute timestamp beyond the past hour, but not earlier than the `  earliestVersionTime  ` .

2.  Use the `  readTime  ` parameter together with the `  BeginTransaction  ` method as part of a [`  ReadOnly  ` transaction](/java/docs/reference/google-cloud-datastore/latest/com.google.datastore.v1#transactionoptions.readonly) for multiple PITR reads.

### Apache Beam

Use the Datastore mode IO Apache Beam connector to read or write entities in a Datastore mode database at a large scale with Dataflow.

Specify the `  withReadTime(Instant readTime)  ` method on the [`  DatastoreV1.Read  `](https://beam.apache.org/releases/javadoc/current/org/apache/beam/sdk/io/gcp/datastore/DatastoreV1.Read.html) object. All the subsequent reads using the `  DatastoreV1.Read  ` object read from the same `  readTime  ` .

### Java

The following code shows how to use the `  withReadTime  ` method for PITR reads.

``` text
  com.google.datastore.v1.Query query = ...
    Instant readTime = Instant.ofEpochSecond(1684098540L);

    DatastoreV1.Read read =
            DatastoreIO.v1()
                .read()
                .withProjectId(project)
                .withQuery(query)
                .withNamespace(namespace)
                .withReadTime(readTime);

    PCollection<Entity> entities = pipeline.apply(read);
    ...
```

For a complete list of `  withReadTime  ` examples, see the [GitHub](https://github.com/apache/beam/blob/master/sdks/java/io/google-cloud-platform/src/test/java/org/apache/beam/sdk/io/gcp/datastore/V1ReadIT.java) repository.

## Clone from a database

You can clone an existing database at a selected timestamp into a new database:

  - The cloned database is a new database that will be created in the same location as the source database.
    
    To make a clone, Firestore uses [point-in-time recovery (PITR) data](/datastore/docs/pitr) of the source database. The cloned database includes all data and indexes.

  - By default, the cloned database will be encrypted in the same way as the source database, using either Google's default encryption or [CMEK encryption](/datastore/docs/use-cmek) . You can specify a different encryption type or use a different key for CMEK encryption.

  - The timestamp has a granularity of one minute and specifies a point of time in the past, in the period defined by the [PITR window](/datastore/docs/pitr#pitr_window) :
    
      - If PITR is enabled for your database, you select any minute in the last 7 days (or less if PITR was enabled less than 7 days ago).
      - If PITR isn't enabled, you can select any minute in the past hour.
      - You can check the earliest timestamp that you can pick [in your database's description](#get-period) .

**Note:** To clone databases, your Google Account must have the [`  datastore.databases.clone  ` IAM permission](#permissions) .

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click more\_vert **View more** in the table row for the database that you want to clone. Click **Clone** . The **Create a clone** dialog appears.

3.  In the **Create a clone** dialog, provide parameters for cloning the database:
    
    1.  In the **Give the clone an ID** field, a [database ID](manage-databases#database_id) for a new cloned database. This database ID must not be associated with an existing database.
    
    2.  In the **Clone from** field, select a point in time to use for cloning. The selected time corresponds to a PITR timestamp, at the minute granularity.

4.  Click **Create clone** .

**Note:** The cloned database will have the **same encryption configuration** as the source database. If you want to specify a different encryption configuration for the cloned database, you can use Google Cloud CLI commands.

### gcloud

Use the [`  gcloud firestore databases clone  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/clone) command to clone a database:

``` text
gcloud firestore databases clone \
--source-database='SOURCE_DATABASE' \
--snapshot-time='PITR_TIMESTAMP' \
--destination-database='DESTINATION_DATABASE_ID'
```

Replace the following:

  - SOURCE\_DATABASE : the database name of an existing database that you want to clone. The name uses the format `  projects/ PROJECT_ID /databases/ SOURCE_DATABASE_ID  ` .

  - PITR\_TIMESTAMP : a [PITR timestamp](#get-period) in the [RFC 3339 format](https://tools.ietf.org/html/rfc3339) , at minute granularity. For example: `  2025-06-01T10:20:00.00Z  ` or `  2025-06-01T10:30:00.00-07:00  ` .

  - DESTINATION\_DATABASE\_ID : a [database ID](manage-databases#database_id) for a new cloned database. This database ID must not be associated with an existing database.

Example:

``` text
gcloud firestore databases clone \
--source-database='projects/example-project/databases/(default)' \
--snapshot-time='2025-06-01T10:20:00.00Z' \
--destination-database='example-dest-db'
```

### Change the cloned database's encryption configuration

By default, the cloned database will have the same encryption configuration as the source database. To change the encryption configuration, use the `  --encryption-type  ` argument:

  - (Default) `  use-source-encryption  ` : use the same encryption configuration as the source database.
  - `  google-default-encryption  ` : use Google's default encryption.
  - `  customer-managed-encryption  ` : use CMEK encryption. Specify a [key ID](https://cloud.google.com/kms/docs/getting-resource-ids#getting_the_id_for_a_key_and_version) in the `  --kms-key-name  ` argument.

The following example shows how to configure CMEK encryption for the cloned database:

``` text
gcloud firestore databases clone \
--source-database='projects/example-project/databases/(default)' \
--snapshot-time='2025-06-01T10:20:00.00Z' \
--destination-database='example-dest-db' \
--encryption-type='customer-managed-encryption' \
--kms-key-name='projects/example-project/locations/us-central1/keyRings/example-key-ring/cryptoKeys/example-key'
```

## Export and import from PITR data

You can export your database to Cloud Storage from PITR data using the [`  gcloud firestore export  `](/sdk/gcloud/reference/firestore/export) command. You can export PITR data where the timestamp is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, the export operation fails.

The PITR export operation supports all filters, including export of all entities and export of specific kinds or namespaces.

1.  Export the database, specifying the `  snapshot-time  ` parameter to the required recovery timestamp.
    
    ### gcloud
    
    Run the following command to export the database to your bucket.
    
    ``` text
    gcloud firestore export gs://[BUCKET_NAME_PATH] \
        --snapshot-time=[PITR_TIMESTAMP] \
        --collection-ids=[COLLECTION_IDS] \
        --namespace-ids=[NAMESPACE_IDS]
    ```
    
    Where,
    
      - `  BUCKET_NAME_PATH  ` - a valid Cloud Storage bucket with an optional path prefix where export files are stored.
      - `  PITR_TIMESTAMP  ` - a PITR timestamp at the minute granularity, for example, `  2023-05-26T10:20:00.00Z  ` or `  2023-10-19T10:30:00.00-07:00  ` .
      - `  COLLECTION_IDS  ` - a list of collection IDs or collection group IDs, for example- `  'specific collection group1'  ` , `  'specific collection group2'  ` .
      - `  NAMESPACE_IDS  ` - a list of namespace IDs, for example- `  'customer'  ` , `  'orders'  ` .
    
    [Exporting a specific subset of kinds and/or namespaces with an entity filter](/datastore/docs/export-import-entities#exporting_specific_kinds_or_namespaces) is also supported.
    
    Note the following points before exporting PITR data:
    
      - Specify the timestamp in [RFC 3339 format](https://tools.ietf.org/html/rfc3339) . For example, `  2023-05-26T10:20:00.00Z  ` or `  2023-10-19T10:30:00.00-07:00  ` .
      - Make sure that the timestamp you specify is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, you will get an error. The timestamp must be a whole minute, even if the specified time is within the past hour.
      - You won't be charged for a failed PITR export.

2.  Import to a database.
    
    Use the steps in [Import all entities](/datastore/docs/export-import-entities#importing_all_entities) to import your exported database. If any entity already exists in your database, it will be overwritten. [Importing a specific subset of kinds and/or namespaces with an entity filter](/datastore/docs/export-import-entities#importing_specific_kinds_or_namespaces) is also supported.
