# Exporting and importing data

You can use the Firestore managed export and import service to recover from accidental deletion of data and to export data for offline processing. You can export all documents or just specific collection groups. Likewise, you can import all data from an export or only specific collection groups. Data exported from one Firestore database can be imported into another Firestore database. You can also [load Firestore exports into BigQuery](https://cloud.google.com/bigquery/docs/loading-data-cloud-firestore) .

This page describes how to export and import Firestore documents using the managed export and import service and [Cloud Storage](https://cloud.google.com/storage/) . The Firestore managed export and import service is available through the [`  gcloud  `](https://cloud.google.com/sdk/gcloud/) command-line tool and the Firestore API ( [REST](../reference/rest/v1beta1/projects.databases) , [RPC](../reference/rpc/google.firestore.admin.v1beta1) ).

**Caution:** Exporting data from Firestore will incur one read operation per document exported. However, these reads will not appear in the usage section of the console. Make sure you understand this before setting up recurring exports to avoid an unexpected bill.

## Before you begin

Before you can use the managed export and import service, you must complete the following tasks:

1.  [Enable billing for your Google Cloud project.](https://cloud.google.com/billing/docs/how-to/modify-project) Only Google Cloud projects with billing enabled can use the export and import functionality.
    
    **Note:** Firebase projects must be on the [Blaze plan](https://firebase.google.com/pricing/?authuser=0) to use the managed export and import service. Enabling billing for the Google Cloud automatically upgrades your Firebase project to the Blaze plan.

2.  [Create a Cloud Storage bucket for your project](https://cloud.google.com/storage/docs/creating-buckets) in a location near [your Firestore database location](../locations#project_location_setting) . You cannot use a Requester Pays bucket for export and import operations.

3.  Make sure your account has the necessary permissions for Firestore and Cloud Storage. **If you are the project owner, your account has the required permissions.** Otherwise, the following roles grant the necessary permissions for export and import operations and for access to Cloud Storage:
    
      - [Firestore roles:](https://cloud.google.com/firestore/docs/security/iam#roles) `  Owner  ` , `  Cloud Datastore Owner  ` , or `  Cloud Datastore Import Export Admin  `
        
        **Note:** These Datastore roles also grant permissions in Firestore.
    
      - [Cloud Storage roles:](https://cloud.google.com/storage/docs/access-control/iam-roles) `  Owner  ` or `  Storage Admin  `

### Service agent permissions

Export and import operations use a Firestore service agent to authorize Cloud Storage operations. The Firestore service agent uses the following naming convention:

  - Firestore service agent  
    `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  `

To learn more about service agents, see [Service agents](https://cloud.google.com/iam/docs/service-agents) .

**Note:** Firestore previously used the App Engine default service account instead of the Firestore service agent. If your database still uses the App Engine service account to import or export data, we recommend that you [migrate to the service specific Firestore service agent](#service_agent_migration) . You can [view which account your import and export operations use](#view_service_agent_name) in the Google Cloud console.  
  
If you use VPC Service Controls, you must use the service-specific Firestore service agent to fully protect import and export operations. VPC Service Controls are not compatible with the App Engine service account.

The Firestore service agent requires access to the Cloud Storage bucket used in an export or import operation. **If your Cloud Storage bucket is in the same project as your Firestore database, then the Firestore service agent can access the bucket by default** .

If the Cloud Storage bucket is in another project, then you must give the Firestore service agent access to the Cloud Storage bucket.

#### Assign roles to the service agent

You can use the [gsutil](https://cloud.google.com/storage/docs/gsutil) command-line tool to assign one of the roles below. For example, to assign the Storage Admin role to the Firestore service agent, run the following:

``` text
gsutil iam ch serviceAccount:service-PROJECT_NUMBER@gcp-sa-firestore.iam.gserviceaccount.com:roles/storage.admin \
    gs://[BUCKET_NAME]
```

Replace `  PROJECT_NUMBER  ` with your project number, which is used to name your Firestore service agent. To view the service agent name, see [View service agent name](#view_service_agent_name) .

Alternatively, you can [assign this role using the Google Cloud console](https://cloud.google.com/storage/docs/access-control/using-iam-permissions#bucket-add) .

### View service agent name

You can view the account that your import and export operations use to authorize requests from the **Import/Export** page in the Google Cloud console. You can also view whether your database uses the Firestore service agent or the legacy App Engine service account.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  View the authorization account next to the **Import/Export jobs run as** label.

The service agent needs the `  Storage Admin  ` role for the Cloud Storage bucket to be used for the export or import operation.

### Set up `     gcloud    ` for your project

You can initiate import and export operations through the Google Cloud console or the `  gcloud  ` command-line tool. To use `  gcloud  ` , set up the command-line tool and connect to your project in one of the following ways:

  - Access `  gcloud  ` from the Google Cloud Platform console using [Cloud Shell](https://cloud.google.com/shell/) .
    
    Make sure `  gcloud  ` is configured for the correct project:
    
    ``` text
    gcloud config set project [PROJECT_ID]
    ```

  - [Install and initialize the Google Cloud SDK.](https://cloud.google.com/sdk/docs/quickstarts)

## Export data

An export operation copies documents in your database to a set of files in a Cloud Storage bucket. Note that an export is not an exact database snapshot taken at the export start time. An export may include changes made while the operation was running.

**Note:** You must [export specific collection groups](#export_specific_collections) if you plan to:

  - [Import only specific collection groups](#import_specific_collections)
  - [Load Firestore data into BigQuery](https://cloud.google.com/bigquery/docs/loading-data-cloud-firestore)

### Export all documents

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Click **Export** .

5.  Click the **Export entire database** option.

6.  Below **Choose Destination** , enter the name of a Cloud Storage bucket or use the **Browse** button to select a bucket.

7.  Click **Export** .

The console returns to the **Import/Export** page. If the operation successfully starts, the page adds an entry to the recent imports and exports page. On failure, the page displays an error message.

### gcloud

Use the [`  firestore export  `](https://cloud.google.com/sdk/gcloud/reference/firestore/export) command to export all the documents in your database, replacing `  [BUCKET_NAME]  ` with the name of your Cloud Storage bucket. Add the `  --async  ` flag to prevent the `  gcloud  ` tool from waiting for the operation to complete.

``` text
  gcloud firestore export gs://[BUCKET_NAME] \
  --database=[DATABASE]
```

Replace the following:

  - `  BUCKET_NAME  ` : organize your exports by adding a file prefix after the bucket name, for example, `  BUCKET_NAME/my-exports-folder/export-name  ` . If you do not provide a file prefix, the managed export service creates one based on the current timestamp.

  - `  DATABASE  ` : name of the database from which you want to export the documents. For the default database, use `  --database='(default)'  ` .

Once you start an export operation, closing the terminal does not cancel the operation, see [cancel an operation](#cancel_an_operation) .

### Export specific collection groups

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Click **Export** .

5.  Click the **Export one or more collection groups** option. Use the dropdown menu to select one or more collection groups.

6.  Below **Choose Destination** , enter the name of a Cloud Storage bucket or use the **Browse** button to select a bucket.

7.  Click **Export** .

The console returns to the **Import/Export** page. If the operation successfully starts, the page adds an entry to the recent imports and exports page. On failure, the page displays an error message.

### gcloud

To export specific collection groups, use the [`  --collection-ids  `](https://cloud.google.com/sdk/gcloud/reference/firestore/export#FLAGS) flag. The operation exports only the collection groups with the given IDs. A collection group includes all collections and subcollections whose final collection ID is the collection group ID.

**Note:** Exporting a collection group won't automatically export subcollections of the collections within the group.

``` text
gcloud firestore export gs://[BUCKET_NAME] \
--collection-ids=[COLLECTION_GROUP_ID_1],[COLLECTION_GROUP_ID_2] \
--database=[DATABASE]
```

For example, you can design a `  restaurants  ` collection in the `  foo  ` database to include multiple subcollections, such as `  ratings  ` , `  reviews  ` , or `  outlets  ` . To export the `  reviews  ` collection group, it must be listed explicitly:

``` text
gcloud firestore export gs://[BUCKET_NAME] \
--collection-ids=reviews \
--database='cymbal'
```

If `  restaurants  ` is specified instead, documents in the `  reviews  ` subcollection won't be exported.

### Export from a PITR timestamp

You can export your database to Cloud Storage from [PITR data](/firestore/native/docs/pitr) . You can export PITR data where the timestamp is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, the export operation fails.

The PITR export operation supports all filters, including exporting all documents and exporting specific collection groups.

Note the following points before exporting PITR data:

  - Specify the timestamp in [RFC 3339 format](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Timestamp) . For example, `  2023-05-26T10:20:00.00Z  ` .
  - Make sure that the timestamp you specify is a whole minute timestamp within the past seven days, but not earlier than the `  earliestVersionTime  ` . If data no longer exists at the specified timestamp, an error is generated.
  - You are not charged for a failed PITR export.

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select a database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Click **Export** .

5.  Configure the export source to export either the entire database or only specific collection groups.

6.  In the **Choose the state of your database to export** section, select **Export from an earlier point in time** .
    
    Select a snapshot time to use for the export

7.  In the **Destination** section, enter the name of a Cloud Storage bucket or use the **Browse** button to select a bucket.

8.  Click **Export** .
    
    The console returns to the **Import/Export** page. If the operation successfully starts, the page adds an entry to the recent imports and exports page. On failure, the page displays an error message.

### gcloud

You can export your database to Cloud Storage from [PITR data](/firestore/native/docs/pitr) using the [`  gcloud firestore export  `](https://cloud.google.com/sdk/gcloud/reference/firestore/export) command.

Export the database, specifying the `  snapshot-time  ` parameter to a recovery timestamp. Run the following command to export the database to your bucket.

``` text
gcloud firestore export gs://[BUCKET_NAME_PATH] \
    --snapshot-time=[PITR_TIMESTAMP]
```

Where `  PITR_TIMESTAMP  ` is a PITR timestamp at the minute granularity, for example, `  2023-05-26T10:20:00.00Z  ` .

Add the [`  --collection-ids  `](https://cloud.google.com/sdk/gcloud/reference/firestore/export#--collection-ids) flag to export specific collection groups.

## Import data

Once you have export files in Cloud Storage, you can import documents in those files back into your project or to another project. Note the following points about import operations:

  - When you import data, the required indexes are updated using your database's current index definitions. An export does not contain index definitions.

  - Imports do not assign new document IDs. Imports use the IDs captured at the time of the export. As a document is being imported, its ID is reserved to prevent ID collisions. If a document with the same ID already exists, the import overwrites the existing document.

  - If a document in your database is not affected by an import, it will remain in your database after the import.

  - Import operations do not trigger Cloud Functions. [Snapshot listeners](../query-data/listen) do receive updates related to import operations.

  - The `  .overall_export_metadata  ` file name must match the name of its parent folder:
    
    `  gs://BUCKET_NAME/OPTIONAL_NAMESPACE_PATH/ PARENT_FOLDER_NAME / PARENT_FOLDER_NAME .overall_export_metadata  `
    
    If you move or copy the output files of an export, keep the PARENT\_FOLDER\_NAME and `  .overall_export_metadata  ` file name the same.

### Import all documents from an export

### Google Cloud Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Click **Import** .

5.  In the **Filename** field, enter the filename of an `  .overall_export_metadata  ` file from a completed export operation. You can use the **Browse** button to help you select the file.

6.  Click **Import** .

The console returns to the **Import/Export** page. If the operation successfully starts, the page adds an entry to the recent imports and exports page. On failure, the page displays an error message.

### gcloud

Use the [`  firestore import  `](https://cloud.google.com/sdk/gcloud/reference/firestore/import) command to import documents from a previous export operation.

``` text
gcloud firestore import gs://[BUCKET_NAME]/[EXPORT_PREFIX]/ --database=[DATABASE]
```

Replace the following:

  - `  BUCKET_NAME/EXPORT_PREFIX  ` : location of your export files.

  - `  DATABASE  ` : name of the database. For the default database, use `  --database='(default)'  ` .

For example:

``` python
gcloud firestore import gs://my-bucket/2017-05-25T23:54:39_76544/ --database='cymbal'
```

You can confirm the location of your export files in the Cloud Storage browser in the Google Cloud console:

Once you start an import operation, closing the terminal does not cancel the operation, see [cancel an operation](#cancel_an_operation) .

### Import specific collection groups

**Note:** To import specific collection groups, you must use the output of an export operation where you [exported specific collection groups](#export_specific_collections) .

### Google Cloud Console

You cannot select specific collection groups in the console. Use `  gcloud  ` instead.

### gcloud

To import specific collection groups from a set of export files, use the [`  --collection-ids  `](https://cloud.google.com/sdk/gcloud/reference/firestore/import#FLAGS) flag. The operation imports only the collection groups with the given IDs. A collection group includes all collections and subcollections whose final collection ID is the collection group ID. Specify the database name using the `  --database  ` flag. For the default database, use `  --database='(default)'  ` .

Only an export of specific collection groups supports an import of specific collection groups. You cannot import specific collection groups from an export of all documents.

``` text
  gcloud firestore import gs://[BUCKET_NAME]/[EXPORT_PREFIX]/ \
  --collection-ids=[COLLECTION_GROUP_ID_1],[COLLECTION_GROUP_ID_2] \
  --database=[DATABASE]
```

### Import a PITR export

Use the steps in [Import all documents](/firestore/native/docs/manage-data/export-import#import_all_documents_from_an_export) to import your exported database. If any document already exists in your database, it will be overwritten.

## Managing export and import operations

After you start an export or import operation, Firestore assigns the operation a unique name. You can use the operation name to delete, cancel, or status check the operation.

Operation names are prefixed with `  projects/[PROJECT_ID]/databases/(default)/operations/  ` , for example:

``` text
projects/my-project/databases/(default)/operations/ASA1MTAwNDQxNAgadGx1YWZlZAcSeWx0aGdpbi1zYm9qLW5pbWRhEgopEg
```

However, you can leave out the prefix when specifying an operation name for the `  describe  ` , `  cancel  ` , and `  delete  ` commands.

### List all export and import operations

### Google Cloud Console

You can view a list of recent export and import operations in the **Import/Export** page of the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

### gcloud

Use the [`  operations list  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/list) command to see all running and recently completed export and import operations:

``` text
gcloud firestore operations list
```

### Check operation status

### Google Cloud Console

You can view the status of a recent export or import operation in the **Import/Export** page of the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

### gcloud

Use the [`  operations describe  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/describe) command to show the status of an export or import operation.

``` text
gcloud firestore operations describe [OPERATION_NAME]
```

#### Estimate the completion time

A request for the status of a long-running operation returns the metrics `  workEstimated  ` and `  workCompleted  ` . Each of these metrics is returned in both number of bytes and number of entities:

  - `  workEstimated  ` shows the estimated total number of bytes and documents an operation will process. Firestore might omit this metric if it cannot make an estimate.

  - `  workCompleted  ` shows the number of bytes and documents processed so far. After the operation completes, the value shows the total number of bytes and documents that were actually processed, which might be larger than the value of `  workEstimated  ` .

Divide `  workCompleted  ` by `  workEstimated  ` for a rough progress estimate. This estimate might be inaccurate, because it depends on delayed statistics collection.

### Cancel an operation

### Google Cloud Console

You can cancel a running export or import operation in the **Import/Export** page of the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

In the *Recent imports and exports* table, currently running operations include a **Cancel** button in the *Completed* column. Click the **Cancel** button to stop the operation. The button changes to a *Cancelling* message and then to *Cancelled* when the operation stops completely.

### gcloud

Use the [`  operations cancel  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel) command to stop an operation in progress:

``` text
gcloud firestore operations cancel [OPERATION_NAME]
```

Cancelling a running operation does not undo the operation. A cancelled export operation will leave documents already exported in Cloud Storage, and a cancelled import operation will leave in place updates already made to your database. You cannot import a partially completed export.

### Delete an operation

Use the [`  gcloud firestore operations delete  `](https://cloud.google.com/sdk/gcloud/reference/firestore/operations/delete) command to remove an operation from the list of recent operations. This command will not delete export files from Cloud Storage.

``` text
gcloud firestore operations delete [OPERATION_NAME]
```

## Billing and pricing for export and import operations

You are required to enable billing for your Google Cloud project before you use the managed export and import service.

Export and import operations are charged for document reads and writes at the rates listed in [Firestore pricing](/firestore/native/pricing) . Export operations incur one read operation per document exported. Import operations incur one write operation per document imported.

Output files stored in Cloud Storage count towards your [Cloud Storage data storage costs](https://cloud.google.com/storage/pricing) .

Export or import operations will not trigger your [Google Cloud budget](https://cloud.google.com/billing/docs/how-to/budgets) alerts until after completion. Export and import operations will not affect the usage shown in the usage section of the console.

### Viewing export and import costs

Export and import operations apply the `  goog-firestoremanaged:exportimport  ` label to billed operations. In the [Cloud Billing reports page](https://cloud.google.com/billing/docs/how-to/reports#getting_started) , you can use this label to view costs related to import and export operations:

**Note:** Export and import operations executed before September 8th, 2020 did not apply the `  goog-firestoremanaged  ` label.

## Export to BigQuery

You can load data from a Firestore export into BigQuery, but only if you specified a `  collection-ids  ` filter. See [Loading data from Firestore exports](https://cloud.google.com/bigquery/docs/loading-data-cloud-firestore) .

### BigQuery column limit

BigQuery imposes a limit of 10,000 columns per table. Firestore export operations generate a BigQuery table schema for each collection group. In this schema, each unique field name within a collection group becomes a schema column.

If a collection group's BigQuery schema surpasses 10,000 columns, the Firestore export operation attempts to stay under the column limit by treating map fields as bytes. If this conversion brings the number of columns below 10,000, you can load the data into BigQuery, but you cannot query the subfields within the map fields. If the number of columns still exceeds 10,000, the export operation does not generate a BigQuery schema for the collection group and you cannot load its data into BigQuery.

## Export format and metadata files

The output of a managed export uses the [LevelDB log format](https://github.com/google/leveldb/blob/master/doc/log_format.md) .

### Metadata files

An export operation creates a metadata file for each collection group you specify. Metadata files are typically named `  ALL_NAMESPACES_KIND_[COLLECTION_GROUP_ID].export_metadata  ` .

The metadata files are protocol buffers and you can decode them with the [`  protoc  ` protocol compiler](https://github.com/protocolbuffers/protobuf#readme) . For example, you can decode a metadata file to determine the collection groups the export files contain:

``` text
protoc --decode_raw < export0.export_metadata
```

## Service agent migration

Firestore uses a Firestore service agent to authorize import and export operations instead of using the App Engine service account. The service agent and service account use the following naming conventions:

  - Firestore service agent  
    `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  `

Firestore previously used the App Engine default service account instead of the Firestore service agent. If your database still uses the App Engine service account to import or export data, we recommend that you follow the instructions in this section to migrate to using the Firestore service agent.

  - App Engine service account  
    `  PROJECT_ID @appspot.gserviceaccount.com  `

The Firestore service agent is preferable because it is specific to Firestore. The App Engine service account is shared by more than one service.

**Note:** If you use VPC Service Controls, you must use the Firestore service agent to fully protect import and export operations. VPC Service Controls is not compatible with the App Engine service account.

### View authorization account

You can view which account your import and export operations use to authorize requests from the **Import/Export** page in the Google Cloud console. You can also view if your database already uses the Firestore service agent.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  View the authorization account next to the **Import/Export jobs run as** label.

If your project does not use the Firestore service agent, you can migrate to the Firestore service agent using either of these techniques:

  - [Migrate a project by checking and updating Cloud Storage bucket permissions (recommended)](#migrate-by-project) .
  - [Add an organization-wide policy constraint](#migrate-by-org-policy) that affects all projects within the organization.

The first of these techniques is preferable because it localizes the scope of effect to a single Firestore project. The second technique is not preferred because it doesn't migrate existing Cloud Storage bucket permissions. It does, however, offer security compliance at the organization level.

### Migrate by checking and updating Cloud Storage bucket permissions

The migration process has two steps:

1.  Update Cloud Storage bucket permissions. See the following section for details.
2.  Confirm migration to the Firestore service agent.

#### Service agent bucket permissions

For any export or import operations that use a Cloud Storage bucket in *another* project, you must grant the Firestore service agent permissions for that bucket. For example, operations that move data to another project need to access a bucket in that other project. Otherwise, these operations fail after migrating to the Firestore service agent.

Import and export workflows that stay within the same project do not require changes to permissions. The Firestore service agent can access buckets in the same project by default.

Update the permissions for Cloud Storage buckets from other projects to give access to the `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  ` service agent. Grant the service agent the `  Firestore Service Agent  ` role.

The `  Firestore Service Agent  ` role grants read and write permissions for a Cloud Storage bucket. If you need to grant only read or only write permissions, use a [custom role](https://cloud.google.com/iam/docs/creating-custom-roles) .

The migration process described in the following section helps you identify Cloud Storage buckets that might require permission updates.

#### Migrate a project to the Firestore Service Agent

Complete the following steps to migrate from the App Engine service account to the Firestore service agent. Once completed, the migration can't be undone.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  If your project has not yet migrated to the Firestore service agent, you see a banner describing the migration and a **Check Bucket Status** button. The next step helps you identify and fix potential permission errors.
    
    Click **Check Bucket Status** .
    
    A menu appears with the option to complete your migration and a list of Cloud Storage buckets. It may take a few minutes for the list to finish loading.
    
    This list includes buckets which were recently used in import and export operations, but do not currently give read and write permissions to the Firestore service agent.

5.  Take note of the principal name of your project's Firestore service agent. The service agent name appears under the **Service agent to give access to** label.

6.  For any bucket in the list that you will use for future import or export operations, complete the following steps:
    
    1.  In this bucket's table row, click **Fix** . This opens that bucket's permissions page in a new tab.
    
    2.  Click **Add** .
    
    3.  In the **New principals** field, enter the name of your Firestore service agent.
    
    4.  In the **Select a role** field, select **Service Agents \> Firestore Service Agent** .
    
    5.  Click **Save** .
    
    6.  Return to the tab with the Firestore Import/Export page.
    
    7.  Repeat these steps for other buckets in the list. Make sure to view all the pages of the list.

7.  Click **Migrate to Firestore Service Agent** . If you still have buckets with failed permission checks, you need to confirm your migration by clicking **Migrate** .
    
    An alert informs you when your migration completes. Migration can't be undone.

#### View migration status

To verify your project's migration status:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Look for the principal next to the **Import/Export jobs run as** label.
    
    If the principal is `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  ` , then your project has already migrated to the Firestore service agent. The migration can't be undone.
    
    If the project has not been migrated, a banner appears at the top of the page with a **Check Bucket Status** button. See [Migrate to the Firestore service agent](#migrate_to_the_firestore_service_agent) to complete the migration.

### Add an organization-wide policy constraint

  - Set the following constraint in your organization's policy:
    
    **Require Firestore Service Agent for import/export** ( `  firestore.requireP4SAforImportExport  ` ).
    
    This constraint requires import and export operations to use the Firestore service agent to authorize requests. To set this constraint, see [Creating and managing organization policies](/resource-manager/docs/organization-policy/creating-managing-policies#creating_and_editing_policies) .

Applying this organizational policy constraint does not automatically grant the appropriate Cloud Storage bucket permissions for the Firestore service agent.

If the constraint creates permission errors for any import or export workflows, you can disable it to go back to using default service account. After you [check and update Cloud Storage bucket permissions](#migrate-by-project) , you can enable the constraint again.
