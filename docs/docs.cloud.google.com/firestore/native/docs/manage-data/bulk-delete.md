# Bulk delete data

Use the managed bulk delete service to delete data from your database. This feature supports deletion against one or more collection groups.

This page describes how to delete documents in bulk using the managed bulk delete service. The Firestore managed bulk delete service is available through the [`  gcloud  `](https://cloud.google.com/sdk/gcloud/) command-line tool and the Firestore [REST API](/firestore/docs/reference/rest/v1/projects.databases/bulkDeleteDocuments) .

**Caution:** Bulk deleting data from Firestore incurs one delete operation per document deleted and some read operations based on a fraction of total documents read. However, these operations don't appear in the usage section of the console. Make sure that you understand this before issuing bulk deletes to avoid billed charges.

## Before you begin

Before you can use the managed bulk delete service, you must complete the following tasks:

1.  [Enable billing for your Google Cloud project.](https://cloud.google.com/billing/docs/how-to/modify-project) Only Google Cloud projects with billing enabled can use the bulk delete functionality.

2.  Make sure your account has the necessary permissions for Firestore. **If you are the project owner, your account has the required permissions.** Otherwise, the following roles grant the necessary permissions for bulk delete operations:
    
      - [Firestore roles:](https://cloud.google.com/firestore/docs/security/iam#predefined_roles) `  Owner  ` , `  Cloud Datastore Owner  ` , or `  Cloud Datastore Bulk Admin  `
        **Note:** These Datastore roles also grant permissions in Firestore.

### Set up `     gcloud    ` for your project

You can initiate bulk delete operations through the Google Cloud console or the `  gcloud  ` command-line tool. To use `  gcloud  ` , set up the command-line tool and connect to your project in one of the following ways:

  - Access `  gcloud  ` from the Google Cloud console using [Cloud Shell](https://cloud.google.com/shell/) .
    
    Make sure `  gcloud  ` is configured for the correct project:
    
    ``` text
    gcloud config set project [PROJECT_ID]
    ```

  - [Install and initialize the Google Cloud SDK.](https://cloud.google.com/sdk/docs/quickstarts)

## Bulk delete data

A bulk delete operation first finds all applicable documents in your database and deletes them in batches. You may still query or read these documents while the results may vary based on the progress made. Bulk delete doesn't delete any documents added or modified after the operation starts.

**Note:** If you plan to delete all documents in the database, see the [database deletion feature](/firestore/docs/manage-databases#delete-database) instead.

### Bulk delete specific collection groups

### gcloud

To bulk delete specific collection groups, use the [`  --collection-ids  `](https://cloud.google.com/sdk/gcloud/reference/beta/firestore/bulk-delete#FLAGS) flag. The operation deletes only the collection groups with the given IDs.

**Note:** Bulk deleting a collection won't automatically delete all the child collections. You also need to specify the child collection groups.

``` text
gcloud firestore bulk-delete \
--collection-ids=[COLLECTION_GROUP_ID_1_OR_KIND_1],[COLLECTION_GROUP_ID_2_OR_KIND_2],[SUBCOLLECTION_GROUP_ID_1_OR_KIND_3] \
--database=[DATABASE]
```

## Manage bulk delete operations

After you start a bulk delete operation, Firestore assigns the operation a unique name. You can use the operation name to delete, cancel, or check the status of the operation.

Operation names are prefixed with `  projects/[PROJECT_ID]/databases/[DATABASE_ID]/operations/  ` , for example:

``` text
projects/my-project/databases/(default)/operations/ASA1MTAwNDQxNAgadGx1YWZlZAcSeWx0aGdpbi1zYm9qLW5pbWRhEgopEg
```

However, you can leave out the prefix when specifying an operation name for the `  describe  ` , `  cancel  ` , and `  delete  ` commands.

### List all bulk delete operations

### gcloud

Use the [`  operations list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/list) command to see all running and recently completed operations, including bulk delete operations:

``` text
gcloud firestore operations list
```

### Check operation status

### gcloud

Use the [`  operations describe  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/describe) command to show the status of a bulk delete operation.

``` text
gcloud firestore operations describe [OPERATION_NAME]
```

#### Estimate the completion time

A request for the status of a long-running operation returns the metrics `  workEstimated  ` and `  workCompleted  ` . Each of these metrics is returned in both number of bytes and number of documents:

  - `  workEstimated  ` shows the estimated total number of bytes and documents an operation will process. Firestore might omit this metric if it can't make an estimate.

  - `  workCompleted  ` shows the number of bytes and documents deleted so far. After the operation completes, the value shows the total number of bytes and documents that were actually processed, which might be larger than the value of `  workEstimated  ` .

Divide `  workCompleted  ` by `  workEstimated  ` for a rough progress estimate. This estimate might be inaccurate, because it depends on delayed statistics collection.

### Cancel an operation

### gcloud

Use the [`  operations cancel  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel) command to stop an operation in progress:

``` text
gcloud firestore operations cancel [OPERATION_NAME]
```

Cancelling a running operation doesn't undo the operation. A cancelled bulk delete operation doesn't recover the deleted documents.

### Delete an operation

Use the [`  gcloud firestore operations delete  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/delete) command to remove a completed operation from the list of recent operations. To cancel a running operation, use the earlier cancellation operation.

``` text
gcloud firestore operations delete [OPERATION_NAME]
```

## Billing and pricing for bulk delete operations

You are required to enable billing for your Google Cloud project before you use the managed bulk delete service.

Bulk delete operations are charged for document reads and deletes at the rates listed in [Firestore pricing](/firestore/docs/pricing) . Bulk delete operations incur one index entry read per document found and one delete operation per document deleted. You are charged one read operation for up to 1000 index entries read. For example, for a bulk delete operation that deleted 1500 documents, you will be charged with 2 documents reads and 1500 document deletes.

Note that Firestore charges on the actual work done. If the operation is cancelled or failed due to user error, you will be charged with progress made. Firestore won't charge reads or deletes for the documents that are not eventually deleted, such as documents that are modified after the delete operation started. The cost will be attributed on the day of operation completion.

Bulk delete operations doesn't trigger your [Google Cloud budget](https://cloud.google.com/billing/docs/how-to/budgets) alerts until after completion. Similarly, reads and deletes performed during a bulk delete operation are applied to your free tier usage after the operation is complete. Bulk delete operations don't affect the usage shown in the usage section of the console.

### View bulk delete costs

Bulk delete operations apply the `  goog-firestoremanaged:bulkdelete  ` label to billed operations. In the [Cloud Billing reports page](https://cloud.google.com/billing/docs/how-to/reports#getting_started) , you can use this label to view costs related to bulk delete operations.

## Best practices

[Avoid skipping over deleted data](/firestore/docs/best-practices#avoid-skipping) which might slow down the queries.
