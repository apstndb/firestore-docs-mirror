This page describes how to create, update, and delete Firestore in Datastore mode databases. You can create multiple Firestore databases per project. You can use multiple databases to set up production and testing environments, to isolate customer data, and for data regionalization.

## The `     (default)    ` database

If you don't specify a database, the Datastore mode client libraries and the Google Cloud CLI connect to the `  (default)  ` database by default.

## Required roles

To create and manage databases, you need the `  Owner  ` or `  Datastore Owner  ` Identity and Access Management role. These roles grant the required permissions.

### Required permissions

To manage databases, you require the following permissions:

  - Create a database: `  datastore.databases.create  `
  - Read database configuration: `  datastore.databases.getMetadata  `
  - Configure a database: `  datastore.databases.update  `
  - Delete a database: `  datastore.databases.delete  `
  - Clone a database: `  datastore.databases.clone  `

## Create a database

To create a database, use one of the following methods:

##### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click **Create a Firestore database** .

3.  Enter a database ID.

4.  Select a Firestore edition. See the [editions overview](/firestore/native/docs/editions-overview) to learn more about each edition.

5.  Select a data access mode. The data access mode configures which API and which client libraries you can use with your database.

6.  If you select Firestore in Native mode:
    
      - Configure your initial security rules. Select **Restrictive** if you don't plan to use the Firebase mobile and web SDKs.
      - If you selected Enterprise edition, enable or disable real-time updates for your database.

7.  Select a location.

8.  (Optional) If you need Customer-managed encryption keys (CMEK), expand and configure the **encryption options** .

9.  Click **Create Database** .

##### gcloud

Use the [`  gcloud firestore databases create  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/create) command.

  - To create a Firestore Standard edition database:
    
    ``` text
    gcloud firestore databases create \
    --database=DATABASE_ID \
    --location=LOCATION \
    --edition=standard
    --type=DATABASE_TYPE
    ```
    
    Replace the following:
    
      - DATABASE\_ID : a [valid database ID](#database_id) .
      - LOCATION : the name of a [Datastore mode multi-region or region](/datastore/docs/locations#types) .
      - DATABASE\_TYPE : either `  firestore-native  ` for Native mode or `  datastore-mode  ` for Datastore mode.

`  --delete-protection  ` is an optional flag to enable deletion protection. You cannot delete a database with deletion protection enabled until you disable this setting. This setting is disabled by default.

To add [tags](https://cloud.google.com/firestore/docs/tags) to the database, use the [`  --tags  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/create#--tags) flag. For example:

  - `  --tags=123/environment=production,123/costCenter=marketing  `
  - `  --tags=tagKeys/333=tagValues/444  `

##### Firebase CLI

``` text
firebase firestore:databases:create DATABASE_ID \
--location=LOCATION \
[--delete-protection DELETE_PROTECTION_ENABLEMENT]
```

Replace the following:

  - DATABASE\_ID : a [valid database ID](#database_id) .
  - LOCATION : the name of a [Datastore mode multi-region or region](/datastore/docs/locations#types) .
  - DELETE\_PROTECTION\_ENABLEMENT : Either `  ENABLED  ` or `  DISABLED  ` .

`  --delete-protection  ` is an optional argument to enable deletion protection. You cannot delete a database with deletion protection enabled until you disable this setting. This setting is disabled by default.

##### Terraform

``` text
resource "google_firestore_database" "database" {
  project     = "project-id"
  name        = DATABASE_ID
  location_id = LOCATION
  type        = DATABASE_TYPE

  // Optional
  delete_protection_state = DELETE_PROTECTION_STATE
}
```

Replace the following:

  - DATABASE\_ID : a [valid database ID](#database_id) .
  - LOCATION : the name of a [Datastore mode multi-region or region](/datastore/docs/locations#types) .
  - DATABASE\_TYPE : either `  FIRESTORE_NATIVE  ` for Native mode or `  DATASTORE_MODE  ` for Datastore mode.
  - DELETE\_PROTECTION\_ENABLEMENT : Either `  DELETE_PROTECTION_ENABLED  ` or `  DELETE_PROTECTION_DISABLED  ` .

`  delete_protection_state  ` is an optional argument to enable deletion protection. You cannot delete a database with deletion protection enabled until you disable this setting. This setting is disabled by default.

### Database ID

Valid database IDs include `  (default)  ` and IDs that conform to the following:

  - Includes only letters, numbers, and hyphen ( `  -  ` ) characters.
  - Letters must be lowercase.
  - The first character must be a letter.
  - The last character must be a letter or number.
  - Minimum of 4 characters.
  - Maximum of 63 characters.
  - Must not be a UUID or resemble a UUID. For example, don't use an ID like `  f47ac10b-58cc-0372-8567-0e02b2c3d479  ` .

If you delete a database, you cannot immediately re-use the database ID until after 5 minutes.

### Delete protection

Use delete protection to prevent accidental deletion of a database. You cannot delete a database with delete protection enabled until you disable delete protection. Delete protection is disabled by default. You can enable delete protection when you create the database or you can [update a database configuration](#update_database_configuration) to enable delete protection.

## Access a named database with a client library

A named database includes any database not named `  (default)  ` . By default, the Firebase SDKs and Google API Client Libraries connect to the `  (default)  ` Firestore database in a project. To create a client connected to a named database, set the database ID when you instantiate a client.

**Note:** To work with multiple databases, be sure to update to the latest [Firebase Client SDKs](/firestore/native/docs/reference/libraries#mobile-web-sdks) and [Google API Client Libraries](/firestore/native/docs/reference/libraries#google-cloud-client-libraries) .

## List databases

Use one of the following methods to list your databases:

##### Console

In the Google Cloud console, go to the **Databases** page.

**Note:** You can view and list your databases in the Google Cloud console. You can create the `  (default)  ` database using the Google Cloud console, but you must use the [Google Cloud CLI or another method](#create_a_database) to create a named database. To delete a database [use the Google Cloud CLI](#delete-database) .

##### gcloud

Use the [`  gcloud firestore databases list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/list) command to list all the databases in your project.

``` text
gcloud firestore databases list
```

##### Firebase CLI

Use the `  firebase firestore:databases:list  ` command to list all the databases in your project.

``` text
firebase firestore:databases:list
```

### View database details

To view details about a single database, use one of the following methods:

##### gcloud

Use the [`  gcloud firestore databases describe  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/describe) command:

``` text
gcloud firestore databases describe --database=DATABASE_ID
```

##### Firebase CLI

Use the `  firebase firestore:databases:get  ` command:

``` text
firebase firestore:databases:get DATABASE_ID
```

Replace DATABASE\_ID with a database ID.

## Update database configuration

To update the configurations settings of a database, use the [`  gcloud firestore databases update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command. Use this command to change the database type or to toggle delete protection.

### Change the database type

To update the type of a database, use the `  gcloud firestore databases update  ` command with the `  --type=  ` flag. You can change the type only if the database is empty.

##### gcloud

``` text
gcloud firestore databases update --database=DATABASE_ID \
--type=DATABASE_TYPE
```

Replace the following:

  - DATABASE\_ID : a database ID.
  - DATABASE\_TYPE : either `  firestore-native  ` for Native mode or `  datastore-mode  ` for Datastore mode.

### Update the delete protection setting

To enable delete protection on a database, use the `  gcloud firestore databases update  ` command with the `  --delete-protection  ` flag. For example:

##### gcloud

``` text
gcloud firestore databases update --database=DATABASE_ID --delete-protection
```

Replace DATABASE\_ID with a database ID.

To disable delete protection on a database, use the `  gcloud firestore databases update  ` command with the `  --no-delete-protection  ` flag. For example:

##### gcloud

``` text
gcloud firestore databases update --database=DATABASE_ID --no-delete-protection
```

Replace DATABASE\_ID with a database ID.

## Delete a database

To delete a database, use the console or command-line tool.

If the database has the delete protection setting enabled, you must first [disable delete protection](#update_the_delete_protection_setting) .

If the database contains [App Engine search data](https://cloud.google.com/appengine/docs/legacy/standard/python/search) or [blob entities](https://cloud.google.com/appengine/docs/legacy/standard/python/blobstore) , you must delete that data first.

Deleting a database does not automatically delete any [Eventarc triggers](/datastore/docs/eventarc) for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](https://cloud.google.com/eventarc/docs/managing-triggers#trigger-delete) .

Deleting a database does not incur charges for delete operations.

##### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click more\_vert **View more** in the table row for the database you want to delete. Click **Delete** . A dialog appears.

3.  In the **Delete database?** dialog, confirm deletion by typing the database ID in the text field. Click **Delete** . The console informs you of operation success or failure.
    
    If the operation fails, [view the database details](#view_database_details) and verify that delete protection is disabled. To disable delete protection, see [Update the delete protection setting](#update_the_delete_protection_setting) .

##### gcloud

Use the [\`gcloud firestore databases delete\`](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/delete) command.

``` text
gcloud firestore databases delete --database=DATABASE_ID
```

Replace DATABASE\_ID with the ID of the database to delete. To delete the default database use the ID `  '(default)'  `

## Clone a database

You can clone an existing database at a selected timestamp into a new database:

  - The cloned database is a new database that will be created in the same location as the source database.
    
    To make a clone, Firestore uses [point-in-time recovery (PITR) data](/datastore/docs/pitr) of the source database. The cloned database includes all data and indexes.

  - By default, the cloned database will be encrypted in the same way as the source database, using either Google's default encryption or [CMEK encryption](/datastore/docs/use-cmek) . You can specify a different encryption type or use a different key for CMEK encryption.

  - The timestamp has a granularity of one minute and specifies a point of time in the past, in the period defined by the [PITR window](/datastore/docs/pitr#pitr_window) :
    
      - If PITR is enabled for your database, you select any minute in the last 7 days (or less if PITR was enabled less than 7 days ago).
      - If PITR isn't enabled, you can select any minute in the past hour.
      - You can check the earliest timestamp that you can pick [in your database's description](/datastore/docs/use-pitr#get-period) .

**Note:** To clone databases, your Google Account must have the [`  datastore.databases.clone  ` IAM permission](#permissions) .

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click more\_vert **View more** in the table row for the database that you want to clone. Click **Clone** . The **Create a clone** dialog appears.

3.  In the **Create a clone** dialog, provide parameters for cloning the database:
    
    1.  In the **Give the clone an ID** field, a [database ID](#database_id) for a new cloned database. This database ID must not be associated with an existing database.
    
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

  - PITR\_TIMESTAMP : a [PITR timestamp](/datastore/docs/use-pitr#get-period) in the [RFC 3339 format](https://tools.ietf.org/html/rfc3339) , at minute granularity. For example: `  2025-06-01T10:20:00.00Z  ` or `  2025-06-01T10:30:00.00-07:00  ` .

  - DESTINATION\_DATABASE\_ID : a [database ID](#database_id) for a new cloned database. This database ID must not be associated with an existing database.

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
--destination-database='example-dest-db'
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

## Configure per-database access permissions

You can use [Identity and Access Management Conditions](https://cloud.google.com/iam/docs/conditions-overview) to configure access permissions on a per-database level. The following examples use the Google Cloud CLI to assign conditional access for one or more databases. You can also [define IAM conditions in the Google Cloud console](https://cloud.google.com/iam/docs/managing-conditional-role-bindings) .

**Warning:** The Google Cloud console does not allow/deny access to databases based on IAM conditions configured at the database level. This only applies to accessing databases with the Google Cloud console. IAM conditions are enforced when accessing databases outside of the Google Cloud console such as with the REST API or the client libraries.

### View existing IAM policies

``` text
gcloud projects get-iam-policy PROJECT_ID
```

Set `  PROJECT_ID  ` to your project ID.

### Grant access to a database

``` text
gcloud projects add-iam-policy-binding PROJECT_ID \
--member='user:EMAIL' \
--role='roles/datastore.user' \
--condition='expression=resource.name=="projects/PROJECT_ID/databases/DATABASE_ID",title=TITLE,description=DESCRIPTION'
```

Set the following:

  - `  PROJECT_ID  ` : your project ID
  - `  EMAIL  ` : an email address that represents a specific Google Account. For example, `  alice@example.com  ` .
  - `  DATABASE_ID  ` : a database ID.
  - `  TITLE  ` : an optional title for the expression.
  - `  DESCRIPTION  ` : an optional description of the expression.

### Grant access to all except one database

``` text
gcloud projects add-iam-policy-binding PROJECT_ID \
--member='user:EMAIL' \
--role='roles/datastore.user' \
--condition='expression=resource.name!="projects/PROJECT_ID/databases/DATABASE_ID",title=TITLE,description=DESCRIPTION'
```

Set the following:

  - `  PROJECT_ID  ` : your project ID
  - `  EMAIL  ` : an email address that represents a specific Google Account. For example, `  alice@example.com  ` .
  - `  DATABASE_ID  ` : a database ID.
  - `  TITLE  ` : an optional title for the expression.
  - `  DESCRIPTION  ` : an optional description of the expression.

### Remove policies for a given member and role

``` text
gcloud projects remove-iam-policy-binding PROJECT_ID \
--member='user:EMAIL' \
--role='roles/datastore.user' --all
```

Set the following:

  - `  PROJECT_ID  ` : your project ID
  - `  EMAIL  ` : an email address that represents a specific Google Account. For example, `  alice@example.com  ` .

## Cloud Monitoring

Firestore metrics are reported under two monitored resources.

  - [firestore.googleapis.com/Database](https://cloud.google.com/monitoring/api/resources#tag_firestore.googleapis.com/Database)
  - [firestore\_instance](https://cloud.google.com/monitoring/api/resources#tag_firestore_instance) (Legacy)

You can inspect aggregate metrics at the database level by looking at `  firestore.googleapis.com/Database  ` . The metrics reported under `  firestore_instance  ` are aggregated at the project level.

## Limitations

  - You can have a maximum of 100 databases per project. You can [contact support](/support-hub) to request an increase to this limit.
  - You cannot delete your `  (default)  ` database if it contains any [GAE search data](https://cloud.google.com/appengine/docs/legacy/standard/python/search) . Use the [index delete api](https://cloud.google.com/appengine/docs/legacy/standard/python/search#deleting_an_index) to delete GAE search data. If you recently deleted GAE Search data, there may be a waiting period before you are able to delete the database.
  - You cannot delete your `  (default)  ` database if it contains any [blob entities](https://cloud.google.com/appengine/docs/legacy/standard/python/blobstore) . Use the [Blobstore delete api](https://cloud.google.com/appengine/docs/legacy/standard/python/refdocs/google.appengine.ext.blobstore.blobstore#google.appengine.ext.blobstore.blobstore.delete) to delete Blobstore data. You can check if your `  (default)  ` database has Blobstore data by running the following GQL query in the Google Cloud console: `  SELECT * FROM __BlobInfo__  ` .
  - You cannot reuse a database ID until 5 minutes after the delete happens.
  - Cloud Function v1 does not support Firestore Named databases. Use [Cloud Firestore Triggers (2nd Gen)](https://cloud.google.com/functions/docs/calling/cloud-firestore) to configure events for named databases.
  - [Firestore function triggers v1](https://cloud.google.com/firestore/docs/extend-with-functions) and [Firestore event triggers](https://cloud.google.com/firestore/docs/eventarc) may stop working after the database is deleted, even if a new database is created with the same name.

## What's next

  - [Access your database](/datastore/docs/activate)
  - [Install a client library](/datastore/docs/reference/libraries)
  - [View code samples](/datastore/docs/samples)
