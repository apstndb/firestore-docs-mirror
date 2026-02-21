# Create and manage databases

This page describes how to create, update, and delete Firestore with MongoDB compatibility databases. You can create multiple Firestore databases per project. You can use multiple databases to set up production and testing environments, to isolate customer data, and for data regionalization.

## Free tier usage

Firestore offers [free tier](/firestore/mongodb-compatibility/quotas) that lets you get started at no cost.

The free tier applies to only one Firestore database per project. The first database that is created in a project without a free tier database will get the free tier. If the database with the free tier applied is deleted, the next database created will receive the free tier.

## Before you begin

You must complete the following before creating a database:

1.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

2.  Assign appropriate Identity and Access Management roles as described in the next section.

### Required roles

To create and manage databases, you need the `  Owner  ` or `  Datastore Owner  ` Identity and Access Management role. These roles grant the required permissions.

#### Required permissions

To manage databases, you need the following permissions:

  - Create a database: `  datastore.databases.create  `
  - Read database configuration: `  datastore.databases.getMetadata  `
  - Configure a database: `  datastore.databases.update  `
  - Delete a database: `  datastore.databases.delete  `
  - Clone a database: `  datastore.databases.clone  `

## Create a database

To create a Firestore with MongoDB compatibility database, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click **Create a Firestore Database** .

3.  Enter a database ID.

4.  Select Enterprise Edition.

5.  Select **Firestore with MongoDB compatibility** .

6.  Select a location for your database.

7.  (Optional) If you need to customize your encryption, click **Show Encryption Options** and configure encryption options.

8.  Click **Create Database** .

##### Firebase CLI

``` text
firebase firestore:databases:create --edition EDITION DATABASE_ID \
--location=LOCATION
```

##### gcloud CLI

Use the [`  gcloud firestore databases create  `](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/create) command and set `  --edition=enterprise  ` .

``` text
gcloud firestore databases create \
--database=DATABASE_ID \
--location=LOCATION \
--edition=enterprise \
--enable-mongodb-compatible-data-access
```

Replace the following:

  - DATABASE\_ID : a [valid database ID](#database_id) .
  - LOCATION : the name of a [Firestore with MongoDB compatibility multi-region or region](/firestore/mongodb-compatibility/docs/locations#types) .

To enable deletion protection, add the `  --delete-protection  ` flag. You cannot delete a database with deletion protection enabled until you disable this setting. This setting is disabled by default.

``` text
gcloud firestore databases create \
--database=DATABASE_ID \
--location=LOCATION \
--edition=enterprise \
--delete-protection
```

To add [tags](/firestore/mongodb-compatibility/docs/tags) to the database, use the [`  --tags  `](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/create#--tags) flag. For example:

  - `  --tags=123/environment=production,123/costCenter=marketing  `
  - `  --tags=tagKeys/333=tagValues/444  `

##### Terraform

Use the [`  google_firestore_database  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/firestore_database) resource and set `  database_edition  ` to `  ENTERPRISE  `

``` text
resource "google_firestore_database" "database" {
  name             = "DATABASE_ID"
  location_id      = "LOCATION"
  type             = "FIRESTORE_NATIVE"
  database_edition = "ENTERPRISE"

  // Optional
  delete_protection_state = "DELETE_PROTECTION_STATE"
}
```

Replace the following:

  - DATABASE\_ID : a [valid database ID](#database_id) .
  - LOCATION : the name of a [Firestore with MongoDB compatibility multi-region or region](/firestore/mongodb-compatibility/docs/locations#types) .
  - DELETE\_PROTECTION\_ENABLEMENT : Either `  DELETE_PROTECTION_ENABLED  ` or `  DELETE_PROTECTION_DISABLED  ` .

To enable deletion protection, set `  delete_protection_state  ` to `  DELETE_PROTECTION_ENABLED  ` . You cannot delete a database with deletion protection enabled until you disable this setting. This setting is disabled by default.

### Database ID

Valid database IDs include IDs that conform to the following:

  - Includes only letters, numbers, and hyphen ( `  -  ` ) characters.
  - Letters must be lowercase.
  - The first character must be a letter.
  - The last character must be a letter or number.
  - Minimum of 4 characters.
  - Maximum of 63 characters.
  - Must not be a UUID or resemble a UUID. For example, don't use an ID like `  f47ac10b-58cc-0372-8567-0e02b2c3d479  ` .

If you delete a database, you cannot immediately re-use the database ID until after 5 minutes.

### Delete protection

Use delete protection to prevent accidental deletion of a database. Delete protection works in the following way:

  - You cannot delete a database with delete protection enabled until you disable delete protection.
  - Delete protection is disabled by default.
  - You can enable delete protection when you create the database or you can [update a database configuration](#update_database_configuration) to enable delete protection.

## List databases

Use one of the following methods to list your databases:

##### Console

In the Google Cloud console, go to the **Databases** page.

##### gcloud CLI

Use the [`  gcloud firestore databases list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/list) command to list all the databases in your project.

``` text
gcloud firestore databases list
```

### View database details

To view details about a single database, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select a database from the list of databases.

##### gcloud CLI

Use the [`  gcloud firestore databases describe  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/describe) command:

``` text
gcloud firestore databases describe --database=DATABASE_ID
```

Replace DATABASE\_ID with a database ID.

## Update database configuration

To update the configuration settings of a database, use the [`  gcloud firestore databases update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command.

Use this command to change, enable, or disable delete protection.

### Update the delete protection setting

To enable delete protection on a database, use the `  gcloud firestore databases update  ` command with the `  --delete-protection  ` flag. For example:

##### gcloud CLI

``` text
gcloud firestore databases update --database=DATABASE_ID --delete-protection
```

Replace DATABASE\_ID with a database ID.

To disable delete protection on a database, use the `  gcloud firestore databases update  ` command with the `  --no-delete-protection  ` flag. For example:

##### gcloud CLI

``` text
gcloud firestore databases update --database=DATABASE_ID --no-delete-protection
```

Replace DATABASE\_ID with a database ID.

## Delete a database

To delete a database, use the console or command-line tool. Deleting a database does not incur charges for delete operations.

If the database has the delete protection setting enabled, you must first [disable delete protection](#update_the_delete_protection_setting) .

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click more\_vert **View more** in the **Actions** column for the database you want to delete. Click **Delete** . A dialog appears.

3.  In the **Delete database?** dialog, confirm deletion by typing the database ID in the text field. Click **Delete** . The console informs you of operation success or failure.
    
    If the operation fails, [view the database details](#view_database_details) and verify that delete protection is disabled. To disable delete protection, see [Update the delete protection setting](#update_the_delete_protection_setting) .

##### gcloud CLI

Use the [\`gcloud firestore databases delete\`](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/delete) command.

``` text
gcloud firestore databases delete --database=DATABASE_ID
```

Replace DATABASE\_ID with the ID of the database to delete.

## Clone a database

You can clone an existing database at a selected timestamp into a new database:

  - The cloned database is a new database that will be created in the same location as the source database.
    
    To make a clone, Firestore uses [point-in-time recovery (PITR) data](/firestore/mongodb-compatibility/docs/pitr) of the source database. The cloned database includes all data and indexes.

  - By default, the cloned database will be encrypted in the same way as the source database, using either Google's default encryption or [CMEK encryption](/firestore/mongodb-compatibility/docs/use-cmek) . You can specify a different encryption type or use a different key for CMEK encryption.

  - The timestamp has a granularity of one minute and specifies a point of time in the past, in the period defined by the [PITR window](/firestore/mongodb-compatibility/docs/pitr#pitr_window) :
    
      - If PITR is enabled for your database, you select any minute in the last 7 days (or less if PITR was enabled less than 7 days ago).
      - If PITR isn't enabled, you can select any minute in the past hour.
      - You can check the earliest timestamp that you can pick [in your database's description](/firestore/mongodb-compatibility/docs/use-pitr#get-period) .

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

  - PITR\_TIMESTAMP : a [PITR timestamp](/firestore/mongodb-compatibility/docs/use-pitr#get-period) in the [RFC 3339 format](https://tools.ietf.org/html/rfc3339) , at minute granularity. For example: `  2025-06-01T10:20:00.00Z  ` or `  2025-06-01T10:30:00.00-07:00  ` .

  - DESTINATION\_DATABASE\_ID : a [database ID](#database_id) for a new cloned database. This database ID must not be associated with an existing database.

Example:

``` text
gcloud firestore databases clone \
--source-database='projects/example-project/databases/example-source-db' \
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
--source-database='projects/example-project/databases/example-source-db' \
--snapshot-time='2025-06-01T10:20:00.00Z' \
--destination-database='example-dest-db' \
--encryption-type='customer-managed-encryption' \
--kms-key-name='projects/example-project/locations/us-central1/keyRings/example-key-ring/cryptoKeys/example-key'
```

## Configure per-database access permissions

You can use [Identity and Access Management Conditions](/iam/docs/conditions-overview) to configure access permissions on a per-database level. The following examples use the Google Cloud CLI to assign conditional access for one or more databases. You can also [define IAM conditions in the Google Cloud console](/iam/docs/managing-conditional-role-bindings) .

**Warning:** The Google Cloud console does not allow nor deny access to databases based on IAM conditions configured at the database level. IAM conditions are enforced when accessing databases outside of the Google Cloud console such as with the REST API or the client libraries.

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
  - `  EMAIL  ` : an email address that represents a specific account. For example, `  alice@example.com  ` .
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
  - `  EMAIL  ` : an email address that represents a specific account. For example, `  alice@example.com  ` .
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
  - `  EMAIL  ` : an email address that represents a specific account. For example, `  alice@example.com  ` .

## Limitations

You can have a maximum of 100 databases per project. You can [contact support](/support-hub) to request an increase to this limit.

## What's next

  - Run the [Quickstart: Create a database and connect to it](/firestore/mongodb-compatibility/docs/create-and-query-database) .
  - Learn about [Behavior differences](/firestore/mongodb-compatibility/docs/behavior-differences) .
  - Learn about [Cloud Monitoring metrics for Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/use-monitoring-dashboard) .
