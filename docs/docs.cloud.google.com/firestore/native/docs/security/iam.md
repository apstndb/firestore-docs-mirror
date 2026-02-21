# Security for server client libraries

When you use the server client libraries for Firestore, you can manage access to your resources with Identity and Access Management (IAM). IAM lets you give more granular access to specific Google Cloud resources and prevents unwanted access to other resources. This page describes the IAM permissions and roles for Firestore. For a detailed description of IAM, read the [IAM documentation](https://cloud.google.com/iam/docs/) .

IAM lets you adopt the [security principle of least privilege](https://wikipedia.org/wiki/Principle_of_least_privilege) , so you grant only the necessary access to your resources.

IAM lets you control **who (user)** has **what (role)** permission for **which** resources by setting IAM policies. IAM policies grant one or more roles to a user, giving the user certain permissions. For example, you can grant the `  datastore.indexAdmin  ` role to a user, which allows the user to create, modify, delete, list, or view indexes.

## Permissions and roles

This section summarizes the permissions and roles that Firestore supports.

**Note:** Some Firestore permissions differ from the standard IAM model permissions. For example, in the IAM model, the `  datastore.databases.get  ` permission lets you return a database object while, in Firestore, `  datastore.databases.get  ` lets you begin or roll back a transaction. To retrieve a database object's information, use the `  datastore.databases.getMetadata  ` permission.

### Required permissions for API methods

The following table lists the permissions that the caller must have to perform each action:

Method

Required permissions

`  projects.databases.documents  `

[`  batchGet  `](../reference/rest/latest/projects.databases.documents/batchGet)

`  datastore.entities.get  `

[`  batchWrite  `](../reference/rest/latest/projects.databases.documents/batchWrite) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  false  `

`  datastore.entities.create  `

[`  batchWrite  `](../reference/rest/latest/projects.databases.documents/batchWrite) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  true  `

`  datastore.entities.create  `

[`  batchWrite  `](../reference/rest/latest/projects.databases.documents/batchWrite) update or transform with no [precondition](../reference/rest/latest/Precondition)

`  datastore.entities.create datastore.entities.update  `

[`  beginTransaction  `](../reference/rest/latest/projects.databases.documents/beginTransaction)

`  datastore.databases.get  `

[`  commit  `](../reference/rest/latest/projects.databases.documents/commit) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  false  `

`  datastore.entities.create  `

[`  commit  `](../reference/rest/latest/projects.databases.documents/commit) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  true  `

`  datastore.entities.update  `

[`  commit  `](../reference/rest/latest/projects.databases.documents/commit) update or transform with no [precondition](../reference/rest/latest/Precondition)

`  datastore.entities.create datastore.entities.update  `

[`  commit  `](../reference/rest/latest/projects.databases.documents/commit) delete

`  datastore.entities.delete  `

[`  createDocument  `](../reference/rest/latest/projects.databases.documents/createDocument)

`  datastore.entities.create  `

[`  delete  `](../reference/rest/latest/projects.databases.documents/delete)

`  datastore.entities.delete  `

[`  get  `](../reference/rest/latest/projects.databases.documents/get)

`  datastore.entities.get  `

[`  list  `](../reference/rest/latest/projects.databases.documents/list)

`  datastore.entities.get  `  
`  datastore.entities.list  `

[`  listCollectionIds  `](../reference/rest/latest/projects.databases.documents/listCollectionIds)

`  datastore.entities.list  `

[`  partitionQuery  `](../reference/rest/latest/projects.databases.documents/partitionQuery)

`  datastore.entities.get datastore.entities.list  `

[`  patch  `](../reference/rest/latest/projects.databases.documents/patch)

`  datastore.entities.update  `

[`  rollback  `](../reference/rest/latest/projects.databases.documents/rollback)

`  datastore.databases.get  `

[`  runAggregationQuery  `](../reference/rest/latest/projects.databases.documents/runAggregationQuery)

`  datastore.entities.get datastore.entities.list  `

[`  runQuery  `](../reference/rest/latest/projects.databases.documents/runQuery)

`  datastore.entities.get datastore.entities.list  `

[`  executePipeline (RPC)  `](../reference/rest/latest/projects.databases.documents/executePipeline)  
  
with any of the following stages:  
\- `  collection(...)  `  
\- `  collection_group(...)  `  
\- `  database()  `

`  datastore.entities.get datastore.entities.list  `

[`  executePipeline (RPC)  `](../reference/rest/latest/projects.databases.documents/executePipeline)  
  
with any of the following stages:  
\- `  documents(...)  `  

`  datastore.entities.get  `

[`  write (RPC)  `](../reference/rpc/google.firestore.v1#write) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  false  `

`  datastore.entities.create  `

[`  write (RPC)  `](../reference/rpc/google.firestore.v1#write) update or transform with [exists precondition](../reference/rest/latest/Precondition) set to `  true  `

`  datastore.entities.update  `

[`  write (RPC)  `](../reference/rpc/google.firestore.v1#write) update or transform with no [precondition](../reference/rest/latest/Precondition)

`  datastore.entities.create datastore.entities.update  `

[`  write (RPC)  `](../reference/rpc/google.firestore.v1#write) delete

`  datastore.entities.delete  `

`  projects.databases.indexes  `

[`  create  `](../reference/rest/latest/projects.databases.indexes/create)

`  datastore.indexes.create  `

[`  delete  `](../reference/rest/latest/projects.databases.indexes/delete)

`  datastore.indexes.delete  `

[`  get  `](../reference/rest/latest/projects.databases.indexes/get)

`  datastore.indexes.get  `

[`  list  `](../reference/rest/latest/projects.databases.indexes/list)

`  datastore.indexes.list  `

`  projects.databases  `

[`  create  `](../reference/rest/v1/projects.databases/create)

`  datastore.databases.create  `  

If your `  create  ` request contains a `  tags  ` value, then the following additional permissions are required:

  - `  datastore.databases.createTagBinding  `

If you would like to verify whether the tag bindings are set successfully by listing the bindings, then the following additional permissions are required:

  - `  datastore.databases.listTagBindings  `
  - `  datastore.databases.listEffectiveTags  `

[`  delete  `](../reference/rest/v1/projects.databases/delete)

`  datastore.databases.delete  `

[`  get  `](../reference/rest/v1/projects.databases/get)

`  datastore.databases.getMetadata  `

[`  list  `](../reference/rest/v1/projects.databases/list)

`  datastore.databases.list  `

[`  patch  `](../reference/rest/v1/projects.databases/patch)

`  datastore.databases.update  `

restore

`  datastore.backups.restoreDatabase  `

[`  clone  `](../reference/rest/v1/projects.databases/clone)

`  datastore.databases.clone  `  

If your `  clone  ` request contains a `  tags  ` value, then the following additional permissions are required:

  - `  datastore.databases.createTagBinding  `

If you would like to verify whether the tag bindings are set successfully by listing the bindings, then the following additional permissions are required:

  - `  datastore.databases.listTagBindings  `
  - `  datastore.databases.listEffectiveTags  `

`  projects.locations  `

[`  get  `](../reference/rest/v1/projects.locations/get)

`  datastore.locations.get  `

[`  list  `](../reference/rest/v1/projects.locations/list)

`  datastore.locations.list  `

`  projects.databases.backupschedules  `

get

`  datastore.backupSchedules.get  `

list

`  datastore.backupSchedules.list  `

create

`  datastore.backupSchedules.create  `

update

`  datastore.backupSchedules.update  `

delete

`  datastore.backupSchedules.delete  `

`  projects.locations.backups  `

get

`  datastore.backups.get  `

list

`  datastore.backups.list  `

delete

`  datastore.backups.delete  `

### Predefined roles

With IAM, every API method in Firestore requires that the account making the API request has the appropriate permissions to use the resource. Permissions are granted by setting policies that grant roles to a user, group, or service account. In addition to the primitive roles, [owner, editor, and viewer](https://cloud.google.com/iam/docs/understanding-roles#primitive_roles) , you can grant Firestore roles to the users of your project.

The following table lists the Firestore IAM roles. You can grant multiple roles to a user, group, or service account.

<table style="width:65%;">
<colgroup>
<col style="width: 30%" />
<col style="width: 35%" />
<col style="width: 0%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.owner      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.*      </code><br />
<br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code><br />
</td>
<td>Full access to Firestore.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.user      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.databases.get      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.entities.*      </code><br />
<code dir="ltr" translate="no">       datastore.indexes.list      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.get      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code><br />
<br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Read/write access to data in a Firestore database. Intended for application developers and service accounts.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.viewer      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.databases.get      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.entities.get      </code><br />
<code dir="ltr" translate="no">       datastore.entities.list      </code><br />
<code dir="ltr" translate="no">       datastore.indexes.get      </code><br />
<code dir="ltr" translate="no">       datastore.indexes.list      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.get      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code><br />
<br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.insights.get      </code></td>
<td>Read access to all Firestore resources.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.importExportAdmin      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<code dir="ltr" translate="no">       datastore.databases.export      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.databases.import      </code><br />
<code dir="ltr" translate="no">       datastore.operations.cancel      </code><br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
<code dir="ltr" translate="no">       datastore.operations.list      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Full access to manage imports and exports.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.bulkAdmin      </code></td>
<td><code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.databases.bulkDelete      </code><br />
<code dir="ltr" translate="no">       datastore.operations.cancel      </code><br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
<code dir="ltr" translate="no">       datastore.operations.list      </code></td>
<td>Full access to manage bulk operations.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.indexAdmin      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.indexes.*      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.operations.list      </code><br />
<br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
<br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Full access to manage index definitions.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.keyVisualizerViewer      </code></td>
<td><code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.keyVisualizerScans.get      </code><br />
<code dir="ltr" translate="no">       datastore.keyVisualizerScans.list      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Full access to Key Visualizer scans.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.backupSchedulesViewer      </code></td>
<td><code dir="ltr" translate="no">       datastore.backupSchedules.get      </code><br />
<code dir="ltr" translate="no">       datastore.backupSchedules.list      </code></td>
<td>Read access to backup schedules in a Firestore database.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.backupSchedulesAdmin      </code></td>
<td><code dir="ltr" translate="no">       datastore.backupSchedules.get      </code><br />
<code dir="ltr" translate="no">       datastore.backupSchedules.list      </code><br />
<code dir="ltr" translate="no">       datastore.backupSchedules.create      </code><br />
<code dir="ltr" translate="no">       datastore.backupSchedules.update      </code><br />
<code dir="ltr" translate="no">       datastore.backupSchedules.delete      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code></td>
<td>Full access to backup schedules in a Firestore database.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.backupsViewer      </code></td>
<td><code dir="ltr" translate="no">       datastore.backups.get      </code><br />
<code dir="ltr" translate="no">       datastore.backups.list      </code></td>
<td>Read access to backup information in a Firestore location.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.backupsAdmin      </code></td>
<td><code dir="ltr" translate="no">       datastore.backups.get      </code><br />
<code dir="ltr" translate="no">       datastore.backups.list      </code><br />
<code dir="ltr" translate="no">       datastore.backups.delete      </code></td>
<td>Full access to backups in a Firestore location.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.restoreAdmin      </code></td>
<td><code dir="ltr" translate="no">       datastore.backups.get      </code><br />
<code dir="ltr" translate="no">       datastore.backups.list      </code><br />
<code dir="ltr" translate="no">       datastore.backups.restoreDatabase      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.databases.create      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.operations.list      </code><br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
</td>
<td>Ability to restore a Firestore backup into a new database. This role also gives the ability to create new databases, not necessarily by restoring from a backup.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.cloneAdmin      </code></td>
<td><code dir="ltr" translate="no">       datastore.databases.clone      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.databases.create      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.operations.list      </code><br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
</td>
<td>Ability to clone a Firestore database into a new database. This role also gives the ability to create new databases, not necessarily by cloning.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.statisticsViewer      </code></td>
<td><code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.insights.get      </code><br />
<code dir="ltr" translate="no">       datastore.keyVisualizerScans.get      </code><br />
<code dir="ltr" translate="no">       datastore.keyVisualizerScans.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
</td>
<td>Read access to Insights, Stats, and Key Visualizer scans.</td>
</tr>
</tbody>
</table>

### Custom roles

If the predefined roles don't address your business requirements, you can define your own custom roles with permissions that you specify:

  - [Learn about custom roles.](/iam/docs/understanding-custom-roles)
  - [Create and manage custom roles.](https://cloud.google.com/iam/docs/creating-custom-roles)

#### Required roles to create and manage tags

If any tag is represented in create or restore actions, some roles are required. See [Creating and managing tags](/resource-manager/docs/tags/tags-creating-and-managing) for more details on creating tag key-value pairs before associate them to the database resources.

The following listed permissions are required.

##### View tags

  - `  datastore.databases.listTagBindings  `
  - `  datastore.databases.listEffectiveTags  `

##### Manage tags on resources

The following permission is required for the database resource you're attaching the tag value.

  - `  datastore.databases.createTagBinding  `

### Permissions

The following table lists the permissions that Firestore supports.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Database permission name</th>
<th>Description</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.get      </code></td>
<td>Begin or rollback a transaction.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.import      </code></td>
<td>Import entities into a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.export      </code></td>
<td>Export entities from a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.bulkDelete      </code></td>
<td>Bulk delete entities from a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.getMetadata      </code></td>
<td>Read metadata from a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.list      </code></td>
<td>List databases in a project.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.create      </code></td>
<td>Create a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.update      </code></td>
<td>Update a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.delete      </code></td>
<td>Delete a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.clone      </code></td>
<td>Clone a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.createTagBinding      </code></td>
<td>Create a tag binding for a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.deleteTagBinding      </code></td>
<td>Delete a tag binding for a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.databases.listTagBindings      </code></td>
<td>List all tag bindings for a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.listEffectiveTagBindings      </code></td>
<td>List effective tag bindings for a database.</td>
<td></td>
</tr>
<tr class="odd">
<td>Entity permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.entities.create      </code></td>
<td>Create a document.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.entities.delete      </code></td>
<td>Delete a document.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.entities.get      </code></td>
<td>Read a document.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.entities.list      </code></td>
<td>List the names of documents in a project.<br />
( <code dir="ltr" translate="no">       datastore.entities.get      </code> is required to access the document data.)</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.entities.update      </code></td>
<td>Update a document.</td>
<td></td>
</tr>
<tr class="odd">
<td>Index permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.indexes.create      </code></td>
<td>Create an index.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.indexes.delete      </code></td>
<td>Delete an index.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.indexes.get      </code></td>
<td>Read metadata from an index.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.indexes.list      </code></td>
<td>List the indexes in a project.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.indexes.update      </code></td>
<td>Update an index.</td>
<td></td>
</tr>
<tr class="odd">
<td>Operation permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.operations.cancel      </code></td>
<td>Cancel a long-running operation.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.operations.delete      </code></td>
<td>Delete a long-running operation.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.operations.get      </code></td>
<td>Gets the latest state of a long-running operation.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.operations.list      </code></td>
<td>List long-running operations.</td>
<td></td>
</tr>
<tr class="even">
<td>Project permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       resourcemanager.projects.get      </code></td>
<td>Browse resources in the project.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>List owned projects.</td>
<td></td>
</tr>
<tr class="odd">
<td>Location permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.locations.get      </code></td>
<td>Get details about a database location. Required to create a new database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.locations.list      </code></td>
<td>List available database locations. Required to create a new database.</td>
<td></td>
</tr>
<tr class="even">
<td>Key Visualizer permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.keyVisualizerScans.get      </code></td>
<td>Get details about Key Visualizer scans.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.keyVisualizerScans.list      </code></td>
<td>List available Key Visualizer scans.</td>
<td></td>
</tr>
<tr class="odd">
<td>Backup Schedule permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.get      </code></td>
<td>Get details about a backup schedule.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.list      </code></td>
<td>List available backup schedules.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.create      </code></td>
<td>Create a backup schedule.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.update      </code></td>
<td>Update a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.delete      </code></td>
<td>Delete a backup schedule.</td>
<td></td>
</tr>
<tr class="odd">
<td>Backup permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backups.get      </code></td>
<td>Get details about a backup.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backups.list      </code></td>
<td>List available backups.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backups.delete      </code></td>
<td>Delete a backup.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backups.restoreDatabase      </code></td>
<td>Restore a database from a backup.</td>
<td></td>
</tr>
<tr class="even">
<td>Insights permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.insights.get      </code></td>
<td>Get insights of a resource</td>
<td></td>
</tr>
</tbody>
</table>

## Role change latency

Firestore caches IAM permissions for 5 minutes, so it takes up to 5 minutes for a role change to become effective.

## Manage Firestore IAM

You can get and set IAM policies using the Google Cloud console, the IAM API, or the `  gcloud  ` command-line tool. See [Granting, Changing, and Revoking Access to Project Members](https://cloud.google.com/iam/docs/granting-changing-revoking-access) for details.

## Configure conditional access permissions

You can use [IAM Conditions](https://cloud.google.com/iam/docs/conditions-overview) to define and enforce conditional access control.

For example, the following condition assigns a principal the `  datastore.user  ` role up until a specified date:

``` text
{
  "role": "roles/datastore.user",
  "members": [
    "user:travis@example.com"
  ],
  "condition": {
    "title": "Expires_December_1_2023",
    "description": "Expires on December 1, 2023",
    "expression":
      "request.time < timestamp('2023-12-01T00:00:00.000Z')"
  }
}
```

To learn how to define IAM Conditions for temporary access, see [Configure temporary access](https://cloud.google.com/iam/docs/configuring-temporary-access) .

To learn how to configure IAM Conditions for access to one or more databases, see [Configure database access conditions](/firestore/native/docs/manage-databases#configure_database_access_conditions) .

## Security rule dependency on IAM

[Firestore Security Rules](/firestore/docs/security/get-started) for mobile/web clients depend on the following service account and IAM binding:

<table>
<thead>
<tr class="header">
<th>Service account</th>
<th>IAM role</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       service-               project_number              @firebase-rules.iam.gserviceaccount.com      </code></td>
<td><code dir="ltr" translate="no">       roles/firebaserules.system      </code></td>
</tr>
</tbody>
</table>

Firebase automatically sets up this service account for you. If you remove the `  firebaserules.system  ` role from this service account, your security rules will deny all requests. To restore this IAM binding, use the following [gcloud CLI](https://cloud.google.com/sdk) command:

``` text
gcloud projects add-iam-policy-binding project_id \
--member=serviceAccount:service-project_number@firebase-rules.iam.gserviceaccount.com \
--role=roles/firebaserules.system
```

To determine your project\_id and project\_number , see [Identifying projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Use the Google Cloud CLI instead of the Google Cloud console, because the `  firebaserules.system  ` role is hidden in the console by default.

## What's next

  - Learn more about [IAM](https://cloud.google.com/iam/docs/) .
  - [Grant IAM roles](https://cloud.google.com/iam/docs/granting-changing-revoking-access) .
  - Learn about [authentication](https://cloud.google.com/firestore/docs/authentication) .
