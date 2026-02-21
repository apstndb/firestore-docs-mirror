# Manage Enterprise edition indexes

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Indexing behavior depends on the edition of the database. This page describes how to manage your indexes for Firestore Enterprise edition. For Firestore Standard edition, see [Firestore Standard edition index overview](/firestore/docs/pipeline/standard-indexing) .

To learn more about Firestore Enterprise edition indexes, see [Indexes overview](/firestore/docs/pipeline/index-overview) .

## Before you begin

Before you can create an index in Firestore, make sure that you are assigned any of the following roles:

  - `  roles/datastore.owner  `
  - `  roles/datastore.indexAdmin  `
  - `  roles/editor  `
  - `  roles/owner  `

To grant a role, see [Grant a single role](https://cloud.google.com/iam/docs/granting-changing-revoking-access#single-role) . For more information about Firestore roles and associated permissions, see [Predefined roles](security/iam) .

If you have defined custom roles, assign all of the following permissions to create indexes:

  - `  datastore.indexes.create  `
  - `  datastore.indexes.delete  `
  - `  datastore.indexes.get  `
  - `  datastore.indexes.list  `
  - `  datastore.indexes.update  `

## Create an index

To create an index, complete the following steps:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select a database from the list of databases.

3.  In the navigation menu, click **Indexes** .

4.  Click **Create Index** .

5.  Enter a **Collection ID** .

6.  Add one or more field paths and select an index option for each.

7.  Select a field presence option, either non-sparse or sparse.

8.  Optionally, set the [unique index](/concepts/enterprise-index-overview#unique_indexes) option.

9.  Click **Create** .

10. Your new index is displayed in the list of indexes and Firestore begins creating your index. When your index is created, you will see a green check mark next to the index. If index is not created, see [Index building errors](/concepts/enterprise-index-overview#index-building-errors) for possible causes.

##### gcloud CLI

To create an index, use the [`  gcloud firestore indexes composite create  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/create) command.

``` text
gcloud firestore indexes composite create \
--database='DATABASE_ID' \
--collection-group=COLLECTION \
--field-config=FIELD_CONFIGURATION \
--query-scope=collection-group \
--density=dense
```

Replace the following:

  - DATABASE\_ID : a database ID.

  - COLLECTION : a collection name.

  - FIELD\_CONFIGURATION : a field configuration. For each field, add `  --field-config=field-path=  ` . For example:
    
    ``` text
        --field-config=field-path=user-id,order=descending \
        --field-config=field-path=score,order=descending
        
    ```
    
    For more information about configuring these fields, see [`  --field-config  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/create#--field-config) .

To create a sparse index, set `  --density=sparse-any  ` .

To create a unique index, add the `  --unique  ` flag.

##### Terraform

Use the [`  google_firestore_index  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/firestore_index) resource.

``` text
resource "google_firestore_index" "index" {
  database    = "DATABASE_ID"
  collection  = "COLLECTION"
  query_scope = "COLLECTION_GROUP"

  // You can include multiple field blocks
  fields {
    field_path = "FIELD_PATH"
    order      = "ORDER"
  }

  // Optional
  multikey = true
  density  = "DENSITY"
}
```

Replace the following:

  - DATABASE\_ID : The database ID for your chosen database
  - COLLECTION : The name of the collection to index
  - FIELD\_PATH : The name of the field to index
  - ORDER : One of `  ASCENDING  ` or `  DESCENDING  `
  - DENSITY : One of `  SPARSE_ANY  ` or `  DENSE  `

## Delete an index

To delete an index, complete the following steps:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list of databases, select a database.

3.  In the navigation menu, click **Indexes** .

4.  In the list of indexes, choose **Delete** from the **More** button more\_vert for the index you want to delete.

5.  Click **Delete Index** .

##### gcloud CLI

1.  To find the name of the index, use the [`  gcloud firestore indexes composite list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list) command.
    
    ``` text
    gcloud firestore indexes composite list \
    --database='DATABASE_ID'
    ```
    
    Replace DATABASE\_ID with the database ID.

2.  To delete the index, use the [`  gcloud firestore indexes composite delete  `](https://cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/delete) command.
    
    ``` text
    gcloud firestore indexes composite delete INDEX_NAME \
    --database='DATABASE_ID'
    ```
    
    Replace the following:
    
      - INDEX\_NAME : the name of an index
      - DATABASE\_ID : a database ID

## Index build time

To build an index, Firestore must create the index and then backfill the index entries with existing data. The time required to create an index is determined by the following:

  - The minimum build time for an index is a few minutes, even for an empty database.

  - The time required to backfill index entries depends on how much existing data belongs in the new index. The more field values that match the index definition, the longer it takes to backfill the index entries.

### Manage long-running operations

Index builds are *long-running operations* . The following sections describe how to work with long-running operations for indexes.

**Key Term:** Firestore supports several administrative operations that can take a long time to complete. These operations are called ***long-running operations*** . Firestore includes features to execute and manage long- running operations. Supported long-running operations include index builds and export operations.

After you start to create an index, Firestore assigns the operation a unique name. Operation names are prefixed with `  projects/ PROJECT_ID /databases/ DATABASE_ID /operations/  ` , for example:

``` text
projects/PROJECT_ID/databases/DATABASE_ID/operations/ASA1MTAwNDQxNAgadGx1YWZlZAcSeWx0aGdpbi1zYm9qLW5pbWRhEgopEg
```

You can omit the prefix when specifying an operation name for the `  describe  ` command.

### List all long-running operations

To list long-running operations, use the [`  gcloud firestore operations list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/list) command. This command lists ongoing and recently completed operations. Operations are listed for a few days after completion:

``` text
gcloud firestore operations list
```

### Check operation status

Instead of listing all long-running operations, you can list the details of a single operation:

``` text
gcloud firestore operations describe operation-name
```

### Estimating the completion time

As your operation runs, see the value of the [`  state  ` field](https://cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#state) for the overall status of the operation.

A request for the status of a long-running operation also returns the metrics `  workEstimated  ` and `  workCompleted  ` . `  workEstimated  ` shows the estimated total number of documents an operation will process. `  workCompleted  ` shows the number of documents processed so far. After the operation completes, `  workCompleted  ` reflects the total number of documents that were actually processed, which might be different than the value of `  workEstimated  ` .

To estimate an operation's progress, divide `  workCompleted  ` by `  workEstimated  ` .

**Note:** The estimate might be inaccurate because it depends on delayed statistics collection.

The following is an example of the progress of creating an index:

``` text
{
  "operations": [
    {
      "name": "projects/project-id/operations/AyAyMDBiM2U5NTgwZDAtZGIyYi0zYjc0LTIzYWEtZjg1ZGdWFmZWQHEjF0c2Flc3UtcmV4ZWRuaS1uaW1kYRUKSBI",
      "metadata": {
        "@type": "type.googleapis.com/google.firestore.admin.v1.IndexOperationMetadata",
        "common": {
          "operationType": "CREATE_INDEX",
          "startTime": "2020-06-23T16:52:25.697539Z",
          "state": "PROCESSING"
        },
        "progressDocuments": {
          "workCompleted": "219327",
          "workEstimated": "2198182"
        }
       },
    },
    ...
```

When an operation completes, the operation description will contain [`  "done": true  `](https://cloud.google.com/firestore/docs/reference/rpc/google.longrunning#operation) . See the value of the [`  state  ` field](https://cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#state) for the result of the operation. If the `  done  ` field is not set in the response, then the operation has not completed.
