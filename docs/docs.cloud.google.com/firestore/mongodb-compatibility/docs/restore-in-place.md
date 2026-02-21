# Perform an in-place restore operation

This page describes how to restore data in a backup to a database with the same name as the source database of the backup. Before you read this page, you should be familiar with [Back up and restore data](/firestore/mongodb-compatibility/docs/backups) .

## In-place restore

An in-place restore lets you restore a database from a backup to the source database that created the backup while the original database still exists. An in-place restore helps you avoid rerouting traffic or creating a database with a different name.

**Warning:** Once you start the in-place restore process, the original database is permanently lost, and you can't undo this operation.

A restore operation must use a destination database that doesn't already exist. You can, however, simulate an in-place restore by deleting the source database and then restoring from a backup to a new database with the same name as the source database.

### Perform an in-place restore

To perform an in-place restore, follow these steps:

1.  Identify the backup to use for the restore operation.
2.  Delete the existing database.
3.  Use the backup and the database ID of the deleted database to complete the restore operation.

### Before you begin

We recommend completing the following steps before starting the in-place restore process.

Retrieve and copy the index configuration of your database. Use the index configuration to re-create indexes after you complete the in-place restore operation. Use the following commands to retrieve the index configuration of your database:

  - Use [`  gcloud firestore indexes composite list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list) to retrieve a list of composite indexes:
    
    ``` text
        gcloud firestore indexes composite list --database=DATABASE_ID
    ```
    
    Replace DATABASE\_ID with the ID of your database.

  - Use [`  gcloud firestore indexes fields list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/fields/list) to retrieve a list of single-field (built-in) index exemptions.
    
    ``` text
        gcloud firestore indexes fields list --database=DATABASE_ID
    ```

### Perform an in-place restore

Complete the following steps to perform an in-place restore operation. This process requires downtime between the moment you delete the database and when the restore operation completes.

Once a restore operation begins, you cannot cancel the operation and must wait until the operation completes. The restore operation immediately occupies the database ID used in the operation.

1.  Use the [`  gcloud firestore backups list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/backups/list) command to identify the backup to use for the restore operation and note the resource name. The resource name uses the following format:
    
    ``` text
        projects/PROJECT_ID/locations/LOCATION/backups/BACKUP_ID
    ```

2.  Use the `  gcloud firestore databases delete  ` command to delete the existing database:
    
    ``` text
        gcloud firestore databases delete --database='DATABASE_ID'
    ```
    
    Replace DATABASE\_ID with the database ID.

3.  Wait at least 5 minutes after you delete the database for the database ID to become available again. Initiate a restore operation using the [`  gcloud firestore databases restore  `](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/restore) command:
    
    ``` text
    gcloud firestore databases restore \
    --source-backup=projects/PROJECT_ID/locations/LOCATION/backups/BACKUP_ID \
    --destination-database='DATABASE_ID'
    ```
    
    Replace DATABASE\_ID with the database ID.

## What's next

  - [Learn more about backup schedules and restore operations](/firestore/mongodb-compatibility/docs/backups)
  - [Learn about configuring point-in-time recovery (PITR)](/firestore/mongodb-compatibility/docs/pitr)
