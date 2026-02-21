Google Cloud offers Identity and Access Management (IAM), which lets you give more granular access to specific Google Cloud resources and prevents unwanted access to other resources. This page describes the Firestore in Datastore mode IAM roles. For a detailed description of IAM, read the [IAM documentation](/iam/docs) .

**Note:** App Engine applications [require IAM permissions to access Datastore mode databases](/datastore/docs/activate#datastore-permissions-for-app-engine) .

IAM lets you adopt the [security principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) , so you grant only the necessary access to your resources.

IAM lets you control **who (users)** has **what (roles)** permission to **which** resources by setting IAM policies. IAM policies grant specific role(s) to a user, giving the user certain permissions. For example, you can grant the `  datastore.indexAdmin  ` role to a user and the user can create, modify, delete, list, or view indexes.

## Permissions and Roles

This section summarizes the permissions and roles Firestore in Datastore mode supports.

### Permissions

The following table lists the permissions that Firestore in Datastore mode supports.

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
<td><code dir="ltr" translate="no">       datastore.databases.get      </code></td>
<td>Begin or rollback a transaction.<br />
Commit with empty mutations.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.databases.import      </code></td>
<td>Import entities into a database.</td>
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
<td>Clone a database.
<p>If your <code dir="ltr" translate="no">        clone       </code> request contains a <code dir="ltr" translate="no">        tags       </code> value, then the following additional permissions are required:</p>
<ul>
<li><code dir="ltr" translate="no">         datastore.databases.createTagBinding        </code></li>
</ul>
<p>If you would like to verify whether the tag bindings are set successfully by listing the bindings, then the following additional permissions are required:</p>
<ul>
<li><code dir="ltr" translate="no">         datastore.databases.listTagBindings        </code></li>
<li><code dir="ltr" translate="no">         datastore.databases.listEffectiveTags        </code></li>
</ul></td>
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
<td><code dir="ltr" translate="no">       datastore.entities.allocateIds      </code></td>
<td>Allocate IDs for keys with an incomplete key path.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.entities.create      </code></td>
<td>Create an entity.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.entities.delete      </code></td>
<td>Delete an entity.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.entities.get      </code></td>
<td>Read an entity.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.entities.list      </code></td>
<td>List the keys of entities in a project.<br />
( <code dir="ltr" translate="no">       datastore.entities.get      </code> is required to access the entity data.)</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.entities.update      </code></td>
<td>Update an entity.</td>
<td></td>
</tr>
<tr class="even">
<td>Index permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.indexes.create      </code></td>
<td>Create an index.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.indexes.delete      </code></td>
<td>Delete an index.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.indexes.get      </code></td>
<td>Read metadata from an index.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.indexes.list      </code></td>
<td>List the indexes in a project.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.indexes.update      </code></td>
<td>Update an index.</td>
<td></td>
</tr>
<tr class="even">
<td>Namespace permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.namespaces.get      </code></td>
<td>Retrieve metadata from a namespace.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.namespaces.list      </code></td>
<td>List the namespaces in a project.</td>
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
<td>Statistics permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.statistics.get      </code></td>
<td>Retrieve <a href="/datastore/docs/concepts/stats">statistics</a> entities.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.statistics.list      </code></td>
<td>List the keys of <a href="/datastore/docs/concepts/stats">statistics</a> entities.<br />
( <code dir="ltr" translate="no">       datastore.statistics.get      </code> is required to access the statistics entity data.)</td>
<td></td>
</tr>
<tr class="even">
<td>App Engine permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       appengine.applications.get      </code></td>
<td>Read-only access to all App Engine application configuration and settings.</td>
<td></td>
</tr>
<tr class="even">
<td>Location permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.locations.get      </code></td>
<td>Get details about a database location. Required to create a new database.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.locations.list      </code></td>
<td>List available database locations. Required to create a new database.</td>
<td></td>
</tr>
<tr class="odd">
<td>Key Visualizer permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.keyVisualizerScans.get      </code></td>
<td>Get details about Key Visualizer scans.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.keyVisualizerScans.list      </code></td>
<td>List available Key Visualizer scans.</td>
<td></td>
</tr>
<tr class="even">
<td>Backup Schedule permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.get      </code></td>
<td>Get details about a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.list      </code></td>
<td>List available backup schedules.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.create      </code></td>
<td>Create a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.update      </code></td>
<td>Update a backup schedule.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backupSchedules.delete      </code></td>
<td>Delete a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td>Backup permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backups.get      </code></td>
<td>Get details about a backup.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backups.list      </code></td>
<td>List available backups.</td>
<td></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastore.backups.delete      </code></td>
<td>Delete a backup.</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.backups.restoreDatabase      </code></td>
<td>Restore a database from a backup.</td>
<td></td>
</tr>
<tr class="odd">
<td>Insights permission name</td>
<td>Description</td>
<td></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datastore.insights.get      </code></td>
<td>Get insights of a resource</td>
<td></td>
</tr>
</tbody>
</table>

### Predefined roles

With IAM, every Datastore API method requires that the account making the API request has the appropriate permissions to use the resource. Permissions are granted by setting policies that grant roles to a user, group, or service account. In addition to the basic roles, [Owner, Editor, and Viewer](/iam/docs/roles-overview#basic) , you can grant Firestore in Datastore mode roles to the users of your project.

The following table lists the Firestore in Datastore mode IAM roles. You can grant multiple roles to a user, group, or service account.

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
<code dir="ltr" translate="no">       datastore.*      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Full access to the database instance.<br />
For <a href="/datastore/docs/console/datastore-admin-console">Datastore Admin</a> access, grant the <code dir="ltr" translate="no">       appengine.appAdmin      </code> role to the principal.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.user      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
<code dir="ltr" translate="no">       datastore.databases.get      </code><br />
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.databases.list      </code><br />
<code dir="ltr" translate="no">       datastore.entities.*      </code><br />
<code dir="ltr" translate="no">       datastore.indexes.list      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.get      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code></td>
<td>Read/write access to data in a Datastore mode database. Intended for application developers and service accounts.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.viewer      </code></td>
<td><code dir="ltr" translate="no">       appengine.applications.get      </code><br />
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
<code dir="ltr" translate="no">       resourcemanager.projects.get      </code><br />
<code dir="ltr" translate="no">       resourcemanager.projects.list      </code><br />
<code dir="ltr" translate="no">       datastore.insights.get      </code></td>
<td>Read access to all Datastore mode database resources.</td>
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
<code dir="ltr" translate="no">       datastore.databases.getMetadata      </code><br />
<code dir="ltr" translate="no">       datastore.indexes.*      </code><br />
<code dir="ltr" translate="no">       datastore.operations.get      </code><br />
<code dir="ltr" translate="no">       datastore.operations.list      </code><br />
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
<td>Read access to backup schedules in a Datastore mode database.</td>
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
<td>Full access to backup schedules in a Datastore mode database.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       roles/datastore.backupsViewer      </code></td>
<td><code dir="ltr" translate="no">       datastore.backups.get      </code><br />
<code dir="ltr" translate="no">       datastore.backups.list      </code></td>
<td>Read access to backup information in a Datastore mode location.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       roles/datastore.backupsAdmin      </code></td>
<td><code dir="ltr" translate="no">       datastore.backups.get      </code><br />
<code dir="ltr" translate="no">       datastore.backups.list      </code><br />
<code dir="ltr" translate="no">       datastore.backups.delete      </code></td>
<td>Full access to backups in a Datastore mode location.</td>
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
<td>Ability to restore a Datastore mode backup into a new database. This role also gives the ability to create new databases, not necessarily by restoring from a backup.</td>
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
<td>Ability to clone a Datastore mode database into a new database. This role also gives the ability to create new databases, not necessarily by cloning.</td>
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

**Warning:** The App Engine [Owner, Editor, and Viewer](/appengine/docs/standard/java/roles#basic_roles) basic roles and the [App Engine Admin](/appengine/docs/java/access-control#predefined_app_engine_roles) predefined role have access to some of the functionality on the [Datastore Admin page](/datastore/docs/console/datastore-admin-console) .

### Custom roles

If the predefined roles don't address your business requirements, you can define your own custom roles with permissions that you specify:

  - [Learn about custom roles.](/iam/docs/understanding-custom-roles)
  - [Create and manage custom roles.](/iam/docs/creating-custom-roles)

#### Required roles to create and manage tags

If any tag is represented in create or restore actions, some roles are required. See [Creating and managing tags](/resource-manager/docs/tags/tags-creating-and-managing) for more details on creating tag key-value pairs before associate them to the database resources.

The following listed permissions are required.

##### View tags

  - `  datastore.databases.listTagBindings  `
  - `  datastore.databases.listEffectiveTags  `

##### Manage tags on resources

The following permission is required for the database resource you're attaching the tag value.

  - `  datastore.databases.createTagBinding  `

### Required Permissions for API methods

The following table lists the permissions that the caller must have to call each method:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Required Permission(s)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         allocateIds       </code></td>
<td><code dir="ltr" translate="no">       datastore.entities.allocateIds      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         beginTransaction       </code></td>
<td><code dir="ltr" translate="no">       datastore.databases.get      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         commit       </code> with empty mutations</td>
<td><code dir="ltr" translate="no">       datastore.databases.get      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         commit       </code> for an insert</td>
<td><code dir="ltr" translate="no">       datastore.entities.create      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         commit       </code> for an upsert</td>
<td><code dir="ltr" translate="no">       datastore.entities.create      </code><br />
<code dir="ltr" translate="no">       datastore.entities.update      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         commit       </code> for an update</td>
<td><code dir="ltr" translate="no">       datastore.entities.update      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         commit       </code> for a delete</td>
<td><code dir="ltr" translate="no">       datastore.entities.delete      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         commit       </code> for a lookup</td>
<td><code dir="ltr" translate="no">       datastore.entities.get      </code><br />
<br />
For a lookup related to metadata or statistics, see <a href="#required_permissions_for_metadata_and_statistics">Required Permissions for Metadata and Statistics</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         commit       </code> for a query</td>
<td><code dir="ltr" translate="no">       datastore.entities.list      </code><br />
<code dir="ltr" translate="no">       datastore.entities.get      </code> (if the query is not a <a href="/datastore/docs/concepts/queries#keys-only_queries">keys-only query</a> )<br />
<br />
For a query related to metadata or statistics, see <a href="#required_permissions_for_metadata_and_statistics">Required Permissions for Metadata and Statistics</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         lookup       </code></td>
<td><code dir="ltr" translate="no">       datastore.entities.get      </code><br />
<br />
For a lookup related to metadata or statistics, see <a href="#required_permissions_for_metadata_and_statistics">Required Permissions for Metadata and Statistics</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         rollback       </code></td>
<td><code dir="ltr" translate="no">       datastore.databases.get      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         runQuery       </code></td>
<td><code dir="ltr" translate="no">       datastore.entities.list      </code><br />
<code dir="ltr" translate="no">       datastore.entities.get      </code> (if the query is not a <a href="/datastore/docs/concepts/queries#keys-only_queries">keys-only query</a> )<br />
<br />
For a query related to metadata or statistics, see <a href="#required_permissions_for_metadata_and_statistics">Required Permissions for Metadata and Statistics</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         runQuery       </code> with a <a href="/datastore/docs/concepts/queries#kindless_queries">kindless query</a></td>
<td><code dir="ltr" translate="no">       datastore.entities.get      </code><br />
<code dir="ltr" translate="no">       datastore.entities.list      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code></td>
</tr>
</tbody>
</table>

### Required Permissions for Metadata and Statistics

The following table lists permissions that the caller must have to call methods on [Metadata](/datastore/docs/concepts/metadataqueries) and [Statistics](/datastore/docs/concepts/stats) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Required Permission(s)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         lookup       </code> of entities with kind names matching <strong>__Stat_*__</strong></td>
<td><code dir="ltr" translate="no">       datastore.statistics.get      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         runQuery       </code> using kinds with names matching <strong>__Stat_*__</strong></td>
<td><code dir="ltr" translate="no">       datastore.statistics.get      </code><br />
<code dir="ltr" translate="no">       datastore.statistics.list      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         runQuery       </code> using the kind <strong>__namespace__</strong></td>
<td><code dir="ltr" translate="no">       datastore.namespaces.get      </code><br />
<code dir="ltr" translate="no">       datastore.namespaces.list      </code></td>
</tr>
</tbody>
</table>

### Required roles to create a Datastore mode database instance

To create a new Datastore mode database instance, you require either the [**Owner** role](/iam/docs/roles-overview#basic) or the [**Datastore Owner** role](/iam/docs/roles-permissions/firestore) .

Datastore mode databases requires an active App Engine application. If the project doesn't have an application, Firestore in Datastore mode creates one for you. In that case, you require the `  appengine.applications.create  ` permission from the **Owner** role or from an [IAM custom role](/iam/docs/creating-custom-roles) containing the permission.

## Role change latency

Firestore in Datastore mode caches IAM permissions for 5 minutes, so it will take up to 5 minutes for a role change to become effective.

## Managing IAM

You can get and set IAM policies using the Google Cloud console, the IAM methods, or the Google Cloud CLI.

  - For the Google Cloud console, see [Access control using the Google Cloud console](/iam/docs/managing-policies#access_control_via_console) .
  - For the IAM methods, see [Access control using the API](/iam/docs/managing-policies#access_control_via_api) .
  - For the gcloud CLI, see [Access control using the gcloud tool](/iam/docs/managing-policies#access_control_via_the_gcloud_tool) .

## Configure conditional access permissions

You can use [IAM Conditions](/iam/docs/conditions-overview) to define and enforce conditional access control.

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

To learn how to define IAM Conditions for temporary access, see [Configure temporary access](/iam/docs/configuring-temporary-access) .

To learn how to configure IAM Conditions for access to one or more databases, see [Configure database access conditions](/datastore/docs/manage-databases#configure_per-database_access_permissions) .

## What's next

  - Learn more about [IAM](/iam/docs) .
  - [Grant IAM roles](/iam/docs/managing-policies) .
