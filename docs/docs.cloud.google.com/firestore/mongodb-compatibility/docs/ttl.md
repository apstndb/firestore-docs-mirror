# Manage data retention with TTL indexes

This page describes how to use the MongoDB API, the Google Cloud console, and the Google Cloud CLI to configure time to live (TTL) indexes.

## Time to live overview

Use TTL indexes to automatically remove stale data from your databases. A TTL index designates a given field as the expiration time for documents in a given collection. With TTL, you can decrease storage costs by cleaning out obsolete data. Data is typically deleted within 24 hours after its expiration time.

### Pricing

TTL delete operations count towards your document delete costs. For pricing of delete operations, see [Firestore Enterprise edition pricing](https://cloud.google.com/firestore/enterprise/pricing) .

### Limits and constraints

  - You can create only one TTL index per collection.
  - You can have a maximum of 500 TTL indexes.

### TTL deletion

Note the following key behaviors of TTL-driven deletion:

  - Deletion through TTL is not an instantaneous process. Expired documents continue to appear in queries and lookup requests until the TTL process actually deletes them. TTL trades deletion timeliness for the benefit of reduced total cost of ownership for deletions. Data is typically deleted within 24 hours after its expiration time.

  - Creating a TTL index on an existing collection results in a bulk deletion of all expired data according to the new TTL index. Note that this bulk deletion is also not instantaneous and depends on how much data exists for that collection.

  - If a document has an expiration time in the past and you add a new TTL index to the collection, the document will be deleted within 24 hours of when the TTL index finishes setup and becomes active.

  - TTL does not necessarily delete documents in the same order as their expiration timestamps.

  - Deletions are not done transactionally. Documents with the same expiration time are not necessarily deleted at the same time. If you require this behavior, perform the deletions using a client library.

  - Firestore with MongoDB compatibility will always honor the latest TTL field to determine the expiration. For example, if an expired but not-yet-deleted document has its TTL field updated to a later date, the document won't be expired and the new date will be used.

  - Firestore with MongoDB compatibility expires a document only when the TTL field is set to either a `  Date and time  ` / `  BSON Date  ` value or an `  Array  ` value containing a `  Date and time  ` / `  BSON Date  ` value. Leave the field absent or set to a value like `  null  ` to disable expirations on a per-document basis.

  - TTL is designed to minimize impact on other database activities. Deletions driven by TTL are treated with a lower priority. Other strategies are also in place to smooth out traffic spikes from TTL-driven deletes.

### TTL fields and non-TTL indexes

A TTL field can be indexed or unindexed. However, because a TTL field is a timestamp, including the field in a non-TTL index can affect performance at higher traffic rates. Including a timestamp field in a non-TTL index can create hotspots which is against best practices. Hotspots are high read, write, and delete rates to a narrow document range.

## Permissions

The principal creating or dropping a TTL index requires the following permission in the project:

  - Viewing TTL indexes requires the `  datastore.indexes.list  ` and `  datastore.indexes.get  ` permissions.
  - Creating or dropping TTL indexes requires the `  datastore.indexes.update  ` permission.
  - Checking the status of TTL operations requires `  datastore.operations.list  ` and `  datastore.operations.get  ` .

For roles that assign these permissions, see [Firestore Identity and Access Management roles](/firestore/mongodb-compatibility/docs/security/iam#predefined_roles) .

## Before you begin

Before you use the gcloud CLI to manage TTL indexes, use the [`  gcloud components update  `](https://cloud.google.com/sdk/gcloud/reference/components/update) command to update components to the latest available version:

``` text
gcloud components update
```

## Create a TTL index

When you create a TTL index, you designate a document field as the expiration time for documents in a collection.

TTL uses a specified field to identify documents that are eligible for deletion. The TTL field must be set to either a `  Timestamp  ` / `  BSON Date  ` value or an `  Array  ` value containing a `  Timestamp  ` / `  BSON Date  ` value. You can select a field that already exists or you can designate a field that you plan to add later.

**Note:** Some TTL indexes created before February 2026 don't apply to `  Timestamp  ` / `  BSON Date  ` values inside of `  Array  ` values. To update the index to apply to `  Array  ` values, drop and re-create the index.

Consider the following before you set the TTL field value:

  - The TTL field value can be a time in the future, now, or in the past. If the value is a time in the past, the document is immediately eligible for deletion. For example, you might create a TTL index with the field `  expireAt  ` , which you then add to existing documents.

  - Using any other data type or not setting the TTL field value will disable the TTL for the individual document.

To create a TTL index, follow these steps:

### MongoDB API

Include the `  expireAfterSeconds  ` index option when calling [`  createIndex()  `](https://www.mongodb.com/docs/manual/reference/method/db.collection.createIndex/) method:

``` text
db.COLLECTION_NAME.createIndex({"TTL_FIELD": 1, "expireAfterSeconds": EXPIRATION_OFFSET_SECONDS})
```

For example:

``` text
db.restaurants.createIndex({"ts": 1, "expireAfterSeconds": 3600})
```

`  expireAfterSeconds  ` identifies the TTL as a TTL index and is the offset between the timestamp value from the TTL field and the expiration time. If `  expireAfterSeconds  ` is set to `  0  ` , the expiration time is given directly by the timestamp value from the TTL field.

Note the following limitations:

  - TTL indexes must include exactly one field.
  - TTL indexes are not usable in queries.
  - You can create only one TTL index per collection.
  - [Audit logs](/firestore/mongodb-compatibility/docs/audit-logging) for TTL index creation with the MongoDB API use the method name `  google.firestore.admin.v1.FirestoreAdmin.UpdateField  ` .

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

4.  Click **Create Policy** .

5.  Enter a collection name and a timestamp field name.

6.  Click **Create** .

The console returns to the **Time-to-live** page. If the operation successfully starts, the page adds an entry to the TTL indexes table. On failure, the page displays an error message.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update) command to configure a TTL index. Add the `  --async  ` flag to prevent the gcloud CLI from waiting for the operation to complete.
    
    ``` text
     gcloud firestore fields ttls update
    ttl_field --collection-group=collection_name
    --enable-ttl 
    ```

### TTL index creation duration

Even on an empty database, it can take ten minutes or more to create a TTL index. Once you start an operation, closing the terminal does not cancel the operation.

## View TTL indexes

To view TTL indexes, follow these steps:

### MongoDB API

Use the [`  listIndexes()  `](https://www.mongodb.com/docs/manual/reference/method/db.collection.listIndexes/) method to view TTL indexes. For example:

``` text
db.restaurants.listIndexes()
```

Note that the output will include both TTL indexes and non-TTL indexes. TTL indexes will include the `  expireAfterSeconds  ` option.

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

The console lists TTL indexes for your database and includes each index's status.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/list) command to configure a TTL index. The following command lists all TTL indexes.
    
    ``` text
    gcloud firestore fields ttls list
    ```
    
    To list TTL indexes under a specific collection, use the following:
    
    ``` text
    gcloud firestore fields ttls list  --collection-group=collection_name
    ```

### View operation details

You can use the gcloud CLI to view more details about a TTL index that is in the `  CREATING  ` state.

Use the [`  operations list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/list) command to see all running and recently completed operations:

``` text
gcloud firestore operations list
```

The response includes an estimate of the operation's progress.

## Drop a TTL index

To drop a TTL index, follow these steps:

### MongoDB API

Use the [`  dropIndex()  `](https://www.mongodb.com/docs/manual/reference/method/db.collection.dropIndex/) method to drop a TTL index. For example:

**Drop a TTL index using index name**

``` text
db.restaurants.dropIndex("ts_1")
```

**Drop a TTL index using index definition**

``` text
db.restaurants.dropIndex({"ts": 1})
```

Note that [Audit logs](/firestore/mongodb-compatibility/docs/audit-logging) for dropping a TTL index with the MongoDB API use the method name `  google.firestore.admin.v1.FirestoreAdmin.UpdateField  ` .

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

4.  In the TTL index table, find the row for the TTL index. Within this table row, click the **Delete** (trashcan) button.

5.  Confirm by clicking **Delete** .

The console returns to the **Time-to-live** page. On success, Firestore with MongoDB compatibility removes the TTL index from the table.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls update  `](https://cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update) command to configure a TTL index. Add the `  --async  ` flag to prevent the gcloud CLI from waiting for the operation to complete.
    
    ``` text
    gcloud firestore fields ttls update ttl_field --collection-group=collection_name --disable-ttl
    ```

## Monitor TTL deletions

You can use Cloud Monitoring to view metrics about TTL-driven deletions. Firestore with MongoDB compatibility provides the following metrics for TTL:

<table>
<thead>
<tr class="header">
<th>Metric type</th>
<th>Metric name</th>
<th>Metric description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>firestore.googleapis.com/document/ttl_deletion_count</td>
<td>Time to live deletion count</td>
<td><p>Total count of documents deleted by TTL indexes.</p></td>
</tr>
<tr class="even">
<td>firestore.googleapis.com/document/ttl_expiration_to_deletion_delays</td>
<td>Time to live expiration to deletion delays</td>
<td><p>Time elapsed between when a document expired under a TTL index and when it was actually deleted.</p></td>
</tr>
</tbody>
</table>

To set up a dashboard with Firestore with MongoDB compatibility metrics, see [manage custom dashboard](https://cloud.google.com/monitoring/charts/dashboards) and [add dashboard widgets](https://cloud.google.com/monitoring/charts) .
