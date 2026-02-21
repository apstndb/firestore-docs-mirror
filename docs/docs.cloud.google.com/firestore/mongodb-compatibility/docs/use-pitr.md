# Work with point-in-time recovery (PITR)

This page describes how to use point-in-time recovery (PITR) to retain and recover data in Firestore with MongoDB compatibility.

To understand PITR concepts, see [Point-in-time recovery](/firestore/mongodb-compatibility/docs/pitr) .

## Permissions

To get the permissions that you need to manage PITR settings, ask your administrator to grant you the [Cloud Datastore Owner](/iam/docs/roles-permissions/firestore#datastore.owner) ( `  roles/datastore.owner  ` ) IAM role on the project whose PITR settings you want to enable. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to manage PITR settings. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to manage PITR settings:

  - To enable PITR when creating a database: `  datastore.databases.create  `
  - To update PITR settings on existing database: `  datastore.databases.update  ` , `  datastore.databases.list  `
  - To perform reads from PITR data: `  datastore.databases.get  ` , `  datastore.entities.get  ` , `  datastore.entities.list  `
  - To export PITR data: `  datastore.databases.export  `
  - To import PITR data: `  datastore.databases.import  `
  - To clone a database: `  datastore.databases.clone  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Before you begin

Note the following points before you start using PITR:

  - You can't start reading from seven days in the past immediately after you enable PITR.
  - If you want to enable PITR when you create a database, you must use the `  gcloud firestore databases create  ` command. Enabling PITR while creating a database using the Google Cloud console is not supported.
  - Firestore with MongoDB compatibility starts retaining versions from the point forward after enabling PITR.
  - You cannot read PITR data in the PITR window after you disable PITR.
  - If you re-enable PITR immediately after disabling it, the past PITR data is no longer available. Any PITR data created before disabling PITR will be deleted after the PITR expiration date.
  - If you accidentally deleted data in the last hour and PITR is disabled, you can restore your data by enabling PITR within one hour of deletion.
  - Any read performed on expired PITR data fails.

## Enable PITR

Before using PITR, [enable billing for your Google Cloud project](https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project) . Only Google Cloud projects with billing enabled can use the PITR functionality.

To enable PITR for your database:

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Disaster Recovery** .

4.  Click **Edit** to edit the settings.

5.  Select the **Enable point-in-time recovery** checkbox, and then click **Save** .

Enabling PITR incurs storage costs. See [Pricing](/firestore/enterprise/pricing) for more information.

To disable PITR, clear the **Enable point-in-time recovery** checkbox from the Disaster Recovery page in the Google Cloud console.

### gcloud

Enable PITR during database creation with the [`  gcloud firestore databases create  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/create) and the `  --enable-ptir  ` command as follows:

``` text
gcloud firestore databases create\
  --location=LOCATION\
  --database=DATABASE_ID\
  --edition=enterprise\
  --enable-pitr
```

Replace the values as follows:

  - `  LOCATION  ` - location where you want to create your database.
  - `  DATABASE_ID  ` - set to a database ID.

You can disable PITR using the [`  gcloud firestore databases update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command as follows:

``` text
gcloud firestore databases update\
  --database=DATABASE_ID\
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
    
      - **Retention period** : the period in which Firestore with MongoDB compatibility retains all versions of data for the database. The value is one hour when PITR is disabled and seven days when PITR is enabled.
      - **Earliest version time** : the earliest timestamp at which older versions of the data can be read in the PITR window. This value is continuously updated by Firestore with MongoDB compatibility and becomes stale the moment it is queried. If you are using this value to recover data, make sure to account for the time from the moment w̦hen the value is queried to the moment when you initiate the recovery.
      - **Point-in-time recovery** : shows `  Enabled  ` , if PITR is enabled. If PITR is disabled, you will see `  Disabled  ` .

### gcloud

Run the [gcloud firestore databases describe](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/describe) command as follows:

``` text
gcloud firestore databases describe --database=DATABASE_ID
```

Replace `  DATABASE_ID  ` with the database ID or `  '(default)'  ` .

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
    name: projects/PROJECT_ID/databases/DATABASE_ID
    pointInTimeRecoveryEnablement: POINT_IN_TIME_RECOVERY_DISABLED
    type: FIRESTORE_NATIVE
    uid: 5230c382-dcd2-468f-8cb3-2a1acfde2b32
    updateTime: '2021-11-17T17:48:22.171180Z'
    versionRetentionPeriod: 3600s
```

where,

  - `  earliestVersionTime  ` : timestamp of the earliest PITR data stored.
  - `  pointInTimeRecoveryEnablement  ` : shows `  POINT_IN_TIME_RECOVERY_ENABLED  ` , if PITR is enabled. If PITR is disabled, you will either see `  POINT_IN_TIME_RECOVERY_DISABLED  ` or the `  pointInTimeRecoveryEnablement  ` field might not be displayed.
  - `  versionRetentionPeriod  ` : time period for which PITR data is retained in milliseconds. The value can be one hour when PITR is disabled or seven days if PITR is enabled.

## Read PITR data

You can read PITR data using the snapshot session in various MongoDB client drivers. Set a `  snapshotTimestamp  ` on the session. The following example uses the MongoDB Java driver, and a similar feature is available in other drivers:

### Java

``` text
    var session =
        mongoClient.startSession(ClientSessionOptions.builder().snapshot(true).build());
  session.setSnapshotTimestamp(new BsonTimestamp(seconds, nanos));

  // run a find query with PITR timestamp
  collection.find(session, <filter>).toList();

  // run an aggregation query pipeline with PITR timestamp
  collection.aggregate(session, <aggregation pipeline stages>).toList();

  // run distinct command with PITR timestamp
  collection.distinct(session, <field>, <return value type class>).toList();
```

**Note:** **Firestore interpretes snapshot timestamp differently from MongoDB** . Except for this difference, Firestore with MongoDB compatibility supports this MongoDB client driver feature and does not require you to use a non-standard client to access your database.

In MongoDB, the `  BsonTimestamp  ` is a MongoDB internal only BSON type of 64 bits. The first 32 bits represents the epoch timestamp seconds and the latter 32 bits represents an ordinal operation count within a MongoDB cluster.

In Firestore with MongoDB compatibility, the snapshot timestamp, which still uses a `  BsonTimestamp  ` value type, interprets the first 32 bits as epoch timestamp seconds, but the latter 32 bits as nanoseconds within the second. Note that not all nanosecond PITR snapshots are supported. Microseconds timestamps in the past 1 hour are allowed, and timestamps of whole minutes from the past 7 days are allowed. See the [point-in-time recovery (PITR) overview](/firestore/mongodb-compatibility/docs/pitr#pitr_window) for what read timestamps are supported.

## Clone from a database

You can clone an existing database at a selected timestamp into a new database:

  - The cloned database is a new database that will be created in the same location as the source database.
    
    To make a clone, Firestore uses [point-in-time recovery (PITR) data](/firestore/mongodb-compatibility/docs/pitr) of the source database. The cloned database includes all data and indexes.

  - By default, the cloned database will be encrypted in the same way as the source database, using either Google's default encryption or [CMEK encryption](/firestore/mongodb-compatibility/docs/use-cmek) . You can specify a different encryption type or use a different key for CMEK encryption.

  - The timestamp has a granularity of one minute and specifies a point of time in the past, in the period defined by the [PITR window](/firestore/mongodb-compatibility/docs/pitr#pitr_window) :
    
      - If PITR is enabled for your database, you select any minute in the last 7 days (or less if PITR was enabled less than 7 days ago).
      - If PITR isn't enabled, you can select any minute in the past hour.
      - You can check the earliest timestamp that you can pick [in your database's description](#get-period) .

**Note:** To clone databases, your Google Account must have the [`  datastore.databases.clone  ` IAM permission](#permissions) .

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click more\_vert **View more** in the table row for the database that you want to clone. Click **Clone** . The **Create a clone** dialog appears.

3.  In the **Create a clone** dialog, provide parameters for cloning the database:
    
    1.  In the **Give the clone an ID** field, a [database ID](create-databases#database_id) for a new cloned database. This database ID must not be associated with an existing database.
    
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

  - DESTINATION\_DATABASE\_ID : a [database ID](create-databases#database_id) for a new cloned database. This database ID must not be associated with an existing database.

Example:

``` text
gcloud firestore databases clone \
--source-database='projects/example-project/databases/(default)' \
--snapshot-time='2025-06-01T10:20:00.00Z' \
--destination-database='example-dest-db'
```

If you want to bind to some tags while cloning a database, use the previous command with the `  --tags  ` flag, which is an optional list of tags KEY=VALUE pairs to bind.

Example:

``` text
gcloud firestore databases clone \
--source-database='projects/example-project/databases/(default)' \
--snapshot-time='2025-06-01T10:20:00.00Z' \
--destination-database='example-dest-db' \
--tags=key1=value1,key2=value2
```

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

### Firebase CLI

Use the `  firebase firestore:databases:clone  ` command to clone a database:

``` text
firebase firestore:databases:clone \
'SOURCE_DATABASE' \
'DESTINATION_DATABASE' \
--snapshot-time 'PITR_TIMESTAMP'
```

Replace the following:

  - SOURCE\_DATABASE : the database name of an existing database that you want to clone. The name uses the format `  projects/ PROJECT_ID /databases/ SOURCE_DATABASE_ID  ` .

  - DESTINATION\_DATABASE : a database name for a new cloned database. The name uses the format `  projects/ PROJECT_ID /databases/ DESTINATION_DATABASE_ID  ` . This database name must not be associated with an existing database.

  - PITR\_TIMESTAMP : a [PITR timestamp](#get-period) in the [RFC 3339 format](https://tools.ietf.org/html/rfc3339) , at minute granularity. For example: `  2025-06-01T10:20:00.00Z  ` or `  2025-06-01T10:30:00.00-07:00  ` . If unspecified, the chosen snapshot will be the current time, rounded down to the minute.

By default, the cloned database will have the same encryption configuration as the source database. To change the encryption configuration, use the `  --encryption-type  ` argument:

  - (Default) `  USE_SOURCE_ENCRYPTION  ` : use the same encryption configuration as the source database.
  - `  GOOGLE_DEFAULT_ENCRYPTION  ` : use Google's default encryption.
  - `  CUSTOMER_MANAGED_ENCRYPTION  ` : use CMEK encryption. Specify a [key ID](https://cloud.google.com/kms/docs/getting-resource-ids#getting_the_id_for_a_key_and_version) in the `  --kms-key-name  ` argument.

The following example shows how to configure CMEK encryption for the cloned database:

``` text
firebase firestore:databases:clone \
'projects/example-project/databases/(default)' \
'projects/example-project/databases/example-dest-db' \
--snapshot-time 'PITR_TIMESTAMP' \
--encryption-type CUSTOMER_MANAGED_ENCRYPTION
```

## Export and import from PITR data

You can export your database to Cloud Storage from PITR data using the [`  gcloud firestore export  `](https://cloud.google.com/sdk/gcloud/reference/firestore/export) command. You can export PITR data where the timestamp is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, the export operation fails.

The PITR export operation supports all filters, including export of all documents and export of specific collections.

1.  Export the database, specifying the `  snapshot-time  ` parameter to the chosen recovery timestamp.
    
    ### gcloud
    
    Run the following command to export the database to your bucket.
    
    ``` text
    gcloud firestore export gs://BUCKET_NAME_PATH \
        --snapshot-time=PITR_TIMESTAMP \
        --collection-ids=COLLECTION_IDS
    ```
    
    Replace the following:
    
      - `  BUCKET_NAME_PATH  ` - a valid Cloud Storage bucket with an optional path prefix where export files are stored.
      - `  PITR_TIMESTAMP  ` - a PITR timestamp at the minute granularity, for example, `  2023-05-26T10:20:00.00Z  ` or `  2023-10-19T10:30:00.00-07:00  ` .
      - `  COLLECTION_IDS  ` - a list of collection IDs or collection group IDs, for example- `  'specific-collection-group1','specific-collection-group2'  ` .
    
    Note the following points before exporting PITR data:
    
      - Specify the timestamp in [RFC 3339 format](https://tools.ietf.org/html/rfc3339) . For example, `  2023-05-26T10:20:00.00Z  ` or `  2023-10-19T10:30:00.00-07:00  ` .
      - Make sure that the timestamp you specify is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, an error is generated. The timestamp must be a whole minute, even if the specified time is within the past hour.
      - You are not charged for a failed PITR export.

2.  Import to a database.
    
    Use the steps in [Import all documents](/firestore/mongodb-compatibility/docs/export-import#import_all_documents_from_an_export) to import your exported database. If any document already exists in your database, it will be overwritten.
