---
name: documents/docs.cloud.google.com/firestore/native/docs/migrate-standard-to-enterprise
uri: https://docs.cloud.google.com/firestore/native/docs/migrate-standard-to-enterprise
title: Migrate from Standard edition to Enterprise edition
description: Migrate data from a Standard edition Firestore database to an Enterprise edition database.
data_source: docs.cloud.google.com
---

# Migrate from Standard edition to Enterprise edition

To migrate data from a Firestore Standard edition database to a Firestore Enterprise edition database, we recommend using one of the following options:

  - The [import and export](https://docs.cloud.google.com/firestore/native/docs/manage-data/export-import) features. The data files from an import operation are compatible with both Enterprise edition and Standard edition.

  - The [`firestore-to-firestore`](https://github.com/GoogleCloudPlatform/DataflowTemplates/blob/main/v2/firestore-to-firestore/README_Cloud_Firestore_to_Firestore.md) Dataflow template. The Dataflow service lets you build data pipelines and the `firestore-to-firestore` template creates a batch pipeline between Firestore databases.

Import and export is the simpler option to run with less configuration options.

The Dataflow template is more customizable. You can extend the template code to perform partial migrations or transform data. You can also control worker counts and size.

Both options support migrations across projects and regions.

## Migrate data with export and import

To migrate data with export and import operations, see [Export and import data](https://docs.cloud.google.com/firestore/native/docs/manage-data/export-import) . To move data to a database in another project, see [Move data between projects](https://docs.cloud.google.com/firestore/native/docs/manage-data/move-data) .

## Migrate data with the Dataflow template

Use the following instructions to migrate data with the `firestore-to-firestore` Dataflow template.

### Before you begin

1.  Before you start the data migration, make sure that [point-in-time recovery (PITR)](https://docs.cloud.google.com/firestore/native/docs/use-pitr#enable) is enabled on the source database. The Dataflow job uses PITR to read data at a PITR timestamp. If PITR is disabled, the job fails if it runs longer than one hour.

2.  The `datastore.googleapis.com` API must be enabled to use this template.

3.  Assign the required roles described in the next section.

### Required roles

To migrate data from one database to another, assign the following roles. You might also be able to get the required permissions through custom roles or other predefined roles:

1.  To get the permissions that you need to create a new database and access Firestore data, ask your administrator to grant you the [Cloud Datastore Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore#datastore.owner) ( `roles/datastore.owner` ) Identity and Access Management (IAM) role on your project.

2.  To give the Dataflow job read and write access to your Firestore databases, assign the Dataflow worker service account (for example, `  PROJECT_NUMBER -compute@developer.gserviceaccount.com ` ) the [Cloud Datastore User](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore#datastore.user) ( `roles/datastore.user` ) IAM role on your project.
    
    For more information about Dataflow security, see [Dataflow security and permissions](https://docs.cloud.google.com/dataflow/docs/concepts/security-and-permissions) .

For more information about granting IAM roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### 1\. Create a new Firestore Enterprise edition database

To migrate data from a Standard edition database to an Enterprise edition database, you must first create the Enterprise edition destination database. See [Create a database](https://docs.cloud.google.com/firestore/native/docs/manage-databases#create_a_database) .

### 2\. Run the Dataflow `firestore-to-firestore` template

Configure and run your Dataflow job with the `firestore-to-firestore` template. The templates supports migrating the entire database or only specified collection groups.

#### Limitations

Consider the following limitations for the `firestore-to-firestore` Dataflow template:

  - The source database must be a Standard edition database.

  - The migration reads data at a specific read-time. We suggest enabling [point-in-time recovery (PITR)](https://docs.cloud.google.com/firestore/native/docs/use-pitr#enable) in the source database. If PITR is not enabled, data expires after one hour and that might not be enough time for the data migration to complete. PITR extends data retention to seven days.

  - Indexes are not migrated.

  - The Dataflow job doesn't migrate database configurations like time to live (TTL) policies, backups, PITR, and customer-managed encryption keys (CMEK).
    
    You must configure these settings on the new database. To improve the speed of the data migration, wait until after the migration to configure TTL, backups, and PITR on the destination database.

The following examples demonstrate how to run the template using the Google Cloud CLI.

#### Migrate all data

To migrate all data, use the following command:

    gcloud dataflow flex-template run "JOB_NAME" \
      --project "PROJECT" \
      --template-file-gcs-location gs://dataflow-templates-REGION_NAME/VERSION/flex/Cloud_Firestore_to_Firestore \
      --region REGION_NAME \
      --parameters "sourceProjectId=SOURCE_PROJECT_ID" \
      --parameters "sourceDatabaseId=SOURCE_DATABASE_ID" \
      --parameters "destinationProjectId=DESTINATION_PROJECT_ID" \
      --parameters "destinationDatabaseId=DESTINATION_DATABASE_ID" \
      --parameters "readTime=READ_TIME"

Replace the following:

  - `  JOB_NAME  ` : a name for the job.

  - `  PROJECT  ` : the ID of your Google Cloud project.

  - `  REGION_NAME  ` : the [Google Cloud location](https://docs.cloud.google.com/dataflow/docs/resources/locations) where you want to run the Dataflow job. Use a location that is near your databases.

  - `  VERSION  ` : the version of the template that you want to use. You can use the following values:
    
      - `latest` to use the latest version of the template, which is available in the *non-dated* parent folder in the bucket— [gs://dataflow-templates- REGION\_NAME /latest/](https://console.cloud.google.com/storage/browser/dataflow-templates/latest)
      - the version name, like `2023-09-12-00_RC00` , to use a specific version of the template, which can be found nested in the respective dated parent folder in the bucket— [gs://dataflow-templates- REGION\_NAME /](https://console.cloud.google.com/storage/browser/dataflow-templates)
    
    > **Caution:** The **latest** version of templates might update with breaking changes. To prevent these breaking changes from affecting production production workflows, use templates in the most recent **dated** parent folder.

  - `  SOURCE_PROJECT_ID  ` : the ID of the source Google Cloud project that contains the Firestore Standard edition database.

  - `  SOURCE_DATABASE_ID  ` : the ID of the source Firestore database.

  - `  DESTINATION_PROJECT_ID  ` : the ID of the destination Google Cloud project for the new Firestore database.

  - `  DESTINATION_DATABASE_ID  ` : the ID of the destination Firestore database.

  - `  READ_TIME  ` : the timestamp to read data from the source database. Set to a timestamp in the RFC 3339 format, at minute granularity such as `2026-05-15T16:31:00.00Z` .
    
    The earliest valid timestamp depends on your point-in-time recovery (PITR) settings. See [Get earliest version time](https://docs.cloud.google.com/firestore/native/docs/use-pitr#get-period) .

#### Migrate specified collection groups

To migrate only certain collection groups, use the following command:

    gcloud dataflow jobs run "JOB_NAME" \
      --project "PROJECT" \
      --gcs-location gs://dataflow-templates-REGION_NAME/VERSION/Cloud_Firestore_to_Firestore \
      --region REGION_NAME \
      --parameters "sourceProjectId=SOURCE_PROJECT_ID" \
      --parameters "sourceDatabaseId=SOURCE_DATABASE_ID" \
      --parameters "collectionGroupIds=COLLECTION_GROUP_IDS" \
      --parameters "destinationProjectId=DESTINATION_PROJECT_ID" \
      --parameters "destinationDatabaseId=DESTINATION_DATABASE_ID" \
      --parameters "readTime=READ_TIME"

Replace the following:

  - `  JOB_NAME  ` : a name for the job.

  - `  PROJECT  ` : the ID of your Google Cloud project.

  - `  REGION_NAME  ` : the [Google Cloud location](https://docs.cloud.google.com/dataflow/docs/resources/locations) where you want to run the Dataflow job. Use a location that is near your databases.

  - `  VERSION  ` : the version of the template that you want to use. You can use the following values:
    
      - `latest` to use the latest version of the template, which is available in the **non-dated** parent folder in the bucket— [gs://dataflow-templates- REGION\_NAME /latest/](https://console.cloud.google.com/storage/browser/dataflow-templates/latest)
      - the version name, like `2023-09-12-00_RC00` , to use a specific version of the template, which can be found nested in the respective dated parent folder in the bucket— [gs://dataflow-templates- REGION\_NAME /](https://console.cloud.google.com/storage/browser/dataflow-templates)
    
    > **Caution:** The **latest** version of templates might update with breaking changes. To prevent these breaking changes from affecting production production workflows, use templates in the most recent **dated** parent folder.

  - `  SOURCE_PROJECT_ID  ` : the ID of the source Google Cloud project that contains the Firestore Standard edition database.

  - `  SOURCE_DATABASE_ID  ` : the ID of the source Firestore database.

  - `  COLLECTION_GROUP_IDS  ` : a comma-separated list of collection group IDs to migrate.
    
    Sub-collections are not included recursively. For example, if you specify the `users` collection group, then the migration won't include a `messages` sub-collection at `/users/userid/messages` unless you also specify the `messages` collection group.

  - `  DESTINATION_PROJECT_ID  ` : the ID of the destination Google Cloud project for the new Firestore database.

  - `  DESTINATION_DATABASE_ID  ` : the ID of the destination Firestore database.

  - `  READ_TIME  ` : the timestamp to read data from the source database. Set to a timestamp in the RFC 3339 format, at minute granularity such as `2026-05-15T16:31:00.00Z` .
    
    The earliest valid timestamp depends on your point-in-time recovery (PITR) settings. See [Get earliest version time](https://docs.cloud.google.com/firestore/native/docs/use-pitr#get-period) .

### 3\. Configure the database

The `firestore-to-firestore` job migrates only data. **Indexes and other database settings are not migrated** . In addition to migrating data, consider configuring the following on the new database:

  - **Indexes** : Firestore Enterprise edition databases don't strictly require indexes to run queries and don't create automatic indexes by default. See the following to create indexes for your queries:
    
      - [Firestore Enterprise edition index overview](https://docs.cloud.google.com/firestore/native/docs/enterprise-index-overview) .
      - [Optimize query performance with indexes](https://docs.cloud.google.com/firestore/native/docs/enterprise-optimize-query-performance#use_indexes) .
      - You can use the Firebase CLI to [export indexes and deploy them to the new database](https://firebase.google.com/docs/reference/firestore/indexes) .
      - Use [Query Insights](https://docs.cloud.google.com/firestore/native/docs/query-insights) to identify queries you can optimize with an index.

  - **TTL** : [Create TTL policies](https://docs.cloud.google.com/firestore/native/docs/ttl) .

  - **Backups** : [Set up backups](https://docs.cloud.google.com/firestore/native/docs/backups) .

  - **PITR** : [Enable PITR](https://docs.cloud.google.com/firestore/native/docs/pitr) .

After configuring your database, you can continue testing your app with the new database. For a complete migration, update your applications to use the new database.

### Troubleshooting

For large databases, the job might fail if it reads too much data at once. To address this:

  - Increase the [`maxNumWorkers`](https://docs.cloud.google.com/dataflow/docs/reference/pipeline-options#resource_utilization) value.

  - [Increase worker memory](https://docs.cloud.google.com/dataflow/docs/guides/troubleshoot-oom#memory-per-vcpu) .

## What's next

  - Learn about querying data with [Pipeline operations](https://docs.cloud.google.com/firestore/native/docs/pipeline/overview) .
  - Learn about how to [optimize queries in Firestore Enterprise edition](https://docs.cloud.google.com/firestore/native/docs/enterprise-optimize-query-performance)
  - Understand how an [Enterprise edition database scales](https://docs.cloud.google.com/firestore/native/docs/understand-reads-writes-scale-enterprise) .
