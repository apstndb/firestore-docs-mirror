---
name: documents/docs.cloud.google.com/datastore/docs/access/iam
uri: https://docs.cloud.google.com/datastore/docs/access/iam
title: Identity and Access Management (IAM)
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

Google Cloud offers Identity and Access Management (IAM), which lets you give more granular access to specific Google Cloud resources and prevents unwanted access to other resources. This page describes the Firestore in Datastore mode IAM roles. For a detailed description of IAM, read the [IAM documentation](https://docs.cloud.google.com/iam/docs) .

> **Note:** App Engine applications [require IAM permissions to access Datastore mode databases](https://docs.cloud.google.com/datastore/docs/activate#datastore-permissions-for-app-engine) .

IAM lets you adopt the [security principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) , so you grant only the necessary access to your resources.

IAM lets you control **who (users)** has **what (roles)** permission to **which** resources by setting IAM policies. IAM policies grant specific role(s) to a user, giving the user certain permissions. For example, you can grant the `datastore.indexAdmin` role to a user and the user can create, modify, delete, list, or view indexes.

## Permissions and Roles

This section summarizes the permissions and roles Firestore in Datastore mode supports.

> **Note:** Some Datastore mode permissions differ from the standard IAM model permissions. For example, in the IAM model, the `datastore.databases.get` permission lets you return a database object while, in Datastore mode, `datastore.databases.get` lets you begin or roll back a transaction. To retrieve a database object's information, use the `datastore.databases.getMetadata` permission.
>
> The `datastore.schemas.*` permissions were previously named `datastore.indexes.*` . You can still use `datastore.indexes` as an alias for `datastore.schemas` .

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
<td><code>datastore.databases.export</code></td>
<td>Export entities from a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.bulkDelete</code></td>
<td>Bulk delete entities from a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.get</code></td>
<td>Begin or rollback a transaction.<br />
Commit with empty mutations.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.import</code></td>
<td>Import entities into a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.getMetadata</code></td>
<td>Read metadata from a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.list</code></td>
<td>List databases in a project.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.create</code></td>
<td>Create a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.update</code></td>
<td>Update a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.delete</code></td>
<td>Delete a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.clone</code></td>
<td>Clone a database.
<p>If your <code>clone</code> request contains a <code>tags</code> value, then the following additional permissions are required:</p>
<ul>
<li><code>datastore.databases.createTagBinding</code></li>
</ul>
<p>If you would like to verify whether the tag bindings are set successfully by listing the bindings, then the following additional permissions are required:</p>
<ul>
<li><code>datastore.databases.listTagBindings</code></li>
<li><code>datastore.databases.listEffectiveTags</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.createTagBinding</code></td>
<td>Create a tag binding for a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.deleteTagBinding</code></td>
<td>Delete a tag binding for a database.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.databases.listTagBindings</code></td>
<td>List all tag bindings for a database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.databases.listEffectiveTagBindings</code></td>
<td>List effective tag bindings for a database.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="odd">
<th>Entity permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.entities.allocateIds</code></td>
<td>Allocate IDs for keys with an incomplete key path.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.entities.create</code></td>
<td>Create an entity.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.entities.delete</code></td>
<td>Delete an entity.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.entities.get</code></td>
<td>Read an entity.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.entities.list</code></td>
<td>List the keys of entities in a project.<br />
( <code>datastore.entities.get</code> is required to access the entity data.)</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.entities.update</code></td>
<td>Update an entity.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Index permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.schemas.create</code></td>
<td>Create an index.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.schemas.delete</code></td>
<td>Delete an index.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.schemas.get</code></td>
<td>Read metadata from an index.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.schemas.list</code></td>
<td>List the indexes in a project.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.schemas.update</code></td>
<td>Update an index.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Namespace permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.namespaces.get</code></td>
<td>Retrieve metadata from a namespace.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.namespaces.list</code></td>
<td>List the namespaces in a project.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="odd">
<th>Operation permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.operations.cancel</code></td>
<td>Cancel a long-running operation.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.operations.delete</code></td>
<td>Delete a long-running operation.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.operations.get</code></td>
<td>Gets the latest state of a long-running operation.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.operations.list</code></td>
<td>List long-running operations.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Project permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>resourcemanager.projects.get</code></td>
<td>Browse resources in the project.</td>
<td></td>
</tr>
<tr class="even">
<td><code>resourcemanager.projects.list</code></td>
<td>List owned projects.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="odd">
<th>Statistics permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.statistics.get</code></td>
<td>Retrieve <a href="https://docs.cloud.google.com/datastore/docs/concepts/stats">statistics</a> entities.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.statistics.list</code></td>
<td>List the keys of <a href="https://docs.cloud.google.com/datastore/docs/concepts/stats">statistics</a> entities.<br />
( <code>datastore.statistics.get</code> is required to access the statistics entity data.)</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>App Engine permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>appengine.applications.get</code></td>
<td>Read-only access to all App Engine application configuration and settings.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Location permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.locations.get</code></td>
<td>Get details about a database location. Required to create a new database.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.locations.list</code></td>
<td>List available database locations. Required to create a new database.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="odd">
<th>Key Visualizer permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.keyVisualizerScans.get</code></td>
<td>Get details about Key Visualizer scans.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.keyVisualizerScans.list</code></td>
<td>List available Key Visualizer scans.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Backup Schedule permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.backupSchedules.get</code></td>
<td>Get details about a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.backupSchedules.list</code></td>
<td>List available backup schedules.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.backupSchedules.create</code></td>
<td>Create a backup schedule.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.backupSchedules.update</code></td>
<td>Update a backup schedule.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.backupSchedules.delete</code></td>
<td>Delete a backup schedule.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="header">
<th>Backup permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.backups.get</code></td>
<td>Get details about a backup.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.backups.list</code></td>
<td>List available backups.</td>
<td></td>
</tr>
<tr class="odd">
<td><code>datastore.backups.delete</code></td>
<td>Delete a backup.</td>
<td></td>
</tr>
<tr class="even">
<td><code>datastore.backups.restoreDatabase</code></td>
<td>Restore a database from a backup.</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr class="odd">
<th>Insights permission name</th>
<th>Description</th>
<th></th>
</tr>

</tbody>
<tbody>
<tr class="odd">
<td><code>datastore.insights.get</code></td>
<td>Get insights of a resource</td>
<td></td>
</tr>
</tbody>
</table>

### Predefined roles

With IAM, every Datastore API method requires that the account making the API request has the appropriate permissions to use the resource. Permissions are granted by setting policies that grant roles to a user, group, or service account. In addition to the basic roles, [Owner, Editor, and Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) , you can grant Firestore in Datastore mode roles to the users of your project.

The following table lists the Firestore in Datastore mode IAM roles. You can grant multiple roles to a user, group, or service account.

| Role                                    | Permissions                                                                                                                                                                                                                                                                                                                                                                                                                   | Description                                                                                                                                                                                             |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `roles/datastore.owner`                 | `appengine.applications.get` `datastore.*` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                                                                                                                                                                                     | Full access to the database instance. For [Datastore Admin](https://docs.cloud.google.com/datastore/docs/console/datastore-admin-console) access, grant the `appengine.appAdmin` role to the principal. |
| `roles/datastore.user`                  | `appengine.applications.get` `datastore.databases.get` `datastore.databases.getMetadata` `datastore.databases.list` `datastore.entities.*` `datastore.schemas.list` `datastore.namespaces.get` `datastore.namespaces.list` `datastore.statistics.get` `datastore.statistics.list` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                              | Read/write access to data in a Datastore mode database. Intended for application developers and service accounts.                                                                                       |
| `roles/datastore.viewer`                | `appengine.applications.get` `datastore.databases.get` `datastore.databases.getMetadata` `datastore.databases.list` `datastore.entities.get` `datastore.entities.list` `datastore.schemas.get` `datastore.schemas.list` `datastore.namespaces.get` `datastore.namespaces.list` `datastore.statistics.get` `datastore.statistics.list` `resourcemanager.projects.get` `resourcemanager.projects.list` `datastore.insights.get` | Read access to all Datastore mode database resources.                                                                                                                                                   |
| `roles/datastore.importExportAdmin`     | `appengine.applications.get` `datastore.databases.export` `datastore.databases.getMetadata` `datastore.databases.import` `datastore.operations.cancel` `datastore.operations.get` `datastore.operations.list` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                  | Full access to manage imports and exports.                                                                                                                                                              |
| `roles/datastore.bulkAdmin`             | `resourcemanager.projects.get` `resourcemanager.projects.list` `datastore.databases.getMetadata` `datastore.databases.bulkDelete` `datastore.operations.cancel` `datastore.operations.get` `datastore.operations.list`                                                                                                                                                                                                        | Full access to manage bulk operations.                                                                                                                                                                  |
| `roles/datastore.indexAdmin`            | `appengine.applications.get` `datastore.databases.getMetadata` `datastore.schemas.*` `datastore.operations.get` `datastore.operations.list` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                                                                                    | Full access to manage index definitions.                                                                                                                                                                |
| `roles/datastore.keyVisualizerViewer`   | `datastore.databases.getMetadata` `datastore.keyVisualizerScans.get` `datastore.keyVisualizerScans.list` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                                                                                                                       | Full access to Key Visualizer scans.                                                                                                                                                                    |
| `roles/datastore.backupSchedulesViewer` | `datastore.backupSchedules.get` `datastore.backupSchedules.list`                                                                                                                                                                                                                                                                                                                                                              | Read access to backup schedules in a Datastore mode database.                                                                                                                                           |
| `roles/datastore.backupSchedulesAdmin`  | `datastore.backupSchedules.get` `datastore.backupSchedules.list` `datastore.backupSchedules.create` `datastore.backupSchedules.update` `datastore.backupSchedules.delete` `datastore.databases.list` `datastore.databases.getMetadata`                                                                                                                                                                                        | Full access to backup schedules in a Datastore mode database.                                                                                                                                           |
| `roles/datastore.backupsViewer`         | `datastore.backups.get` `datastore.backups.list`                                                                                                                                                                                                                                                                                                                                                                              | Read access to backup information in a Datastore mode location.                                                                                                                                         |
| `roles/datastore.backupsAdmin`          | `datastore.backups.get` `datastore.backups.list` `datastore.backups.delete`                                                                                                                                                                                                                                                                                                                                                   | Full access to backups in a Datastore mode location.                                                                                                                                                    |
| `roles/datastore.restoreAdmin`          | `datastore.backups.get` `datastore.backups.list` `datastore.backups.restoreDatabase` `datastore.databases.list` `datastore.databases.create` `datastore.databases.getMetadata` `datastore.operations.list` `datastore.operations.get`                                                                                                                                                                                         | Ability to restore a Datastore mode backup into a new database. This role also gives the ability to create new databases, not necessarily by restoring from a backup.                                   |
| `roles/datastore.cloneAdmin`            | `datastore.databases.clone` `datastore.databases.list` `datastore.databases.create` `datastore.databases.getMetadata` `datastore.operations.list` `datastore.operations.get`                                                                                                                                                                                                                                                  | Ability to clone a Datastore mode database into a new database. This role also gives the ability to create new databases, not necessarily by cloning.                                                   |
| `roles/datastore.statisticsViewer`      | `resourcemanager.projects.get` `resourcemanager.projects.list` `datastore.databases.getMetadata` `datastore.insights.get` `datastore.keyVisualizerScans.get` `datastore.keyVisualizerScans.list` `datastore.statistics.list` `datastore.statistics.get`                                                                                                                                                                       | Read access to Insights, Stats, and Key Visualizer scans.                                                                                                                                               |

> **Warning:** The App Engine [Owner, Editor, and Viewer](https://docs.cloud.google.com/appengine/docs/standard/java/roles#basic_roles) basic roles and the [App Engine Admin](https://docs.cloud.google.com/appengine/docs/java/access-control#predefined_app_engine_roles) predefined role have access to some of the functionality on the [Datastore Admin page](https://docs.cloud.google.com/datastore/docs/console/datastore-admin-console) .

### Custom roles

If the predefined roles don't address your business requirements, you can define your own custom roles with permissions that you specify:

- [Learn about custom roles.](https://docs.cloud.google.com/iam/docs/understanding-custom-roles)
- [Create and manage custom roles.](https://docs.cloud.google.com/iam/docs/creating-custom-roles)

#### Required roles to create and manage tags

If any tag is represented in create or restore actions, some roles are required. See [Creating and managing tags](https://docs.cloud.google.com/resource-manager/docs/tags/tags-creating-and-managing) for more details on creating tag key-value pairs before associate them to the database resources.

The following listed permissions are required.

##### View tags

- `datastore.databases.listTagBindings`
- `datastore.databases.listEffectiveTags`

##### Manage tags on resources

The following permission is required for the database resource you're attaching the tag value.

- `datastore.databases.createTagBinding`

### Required Permissions for API methods

The following table lists the permissions that the caller must have to call each method:

| Method                                                                                                                                                                                            | Required Permission(s)                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`allocateIds`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/allocateIds)                                                                                                   | `datastore.entities.allocateIds`                                                                                                                                                                                                                                                                                                                                                                 |
| [`beginTransaction`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/beginTransaction)                                                                                         | `datastore.databases.get`                                                                                                                                                                                                                                                                                                                                                                        |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) with empty mutations                                                                                        | `datastore.databases.get`                                                                                                                                                                                                                                                                                                                                                                        |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for an insert                                                                                               | `datastore.entities.create`                                                                                                                                                                                                                                                                                                                                                                      |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for an upsert                                                                                               | `datastore.entities.create` `datastore.entities.update`                                                                                                                                                                                                                                                                                                                                          |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for an update                                                                                               | `datastore.entities.update`                                                                                                                                                                                                                                                                                                                                                                      |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for a delete                                                                                                | `datastore.entities.delete`                                                                                                                                                                                                                                                                                                                                                                      |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for a lookup                                                                                                | `datastore.entities.get` For a lookup related to metadata or statistics, see [Required Permissions for Metadata and Statistics](https://docs.cloud.google.com/datastore/docs/access/iam#required_permissions_for_metadata_and_statistics) .                                                                                                                                                      |
| [`commit`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/commit) for a query                                                                                                 | `datastore.entities.list` `datastore.entities.get` (if the query is not a [keys-only query](https://docs.cloud.google.com/datastore/docs/concepts/queries#keys-only_queries) ) For a query related to metadata or statistics, see [Required Permissions for Metadata and Statistics](https://docs.cloud.google.com/datastore/docs/access/iam#required_permissions_for_metadata_and_statistics) . |
| [`lookup`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/lookup)                                                                                                             | `datastore.entities.get` For a lookup related to metadata or statistics, see [Required Permissions for Metadata and Statistics](https://docs.cloud.google.com/datastore/docs/access/iam#required_permissions_for_metadata_and_statistics) .                                                                                                                                                      |
| [`rollback`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/rollback)                                                                                                         | `datastore.databases.get`                                                                                                                                                                                                                                                                                                                                                                        |
| [`runQuery`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/runQuery)                                                                                                         | `datastore.entities.list` `datastore.entities.get` (if the query is not a [keys-only query](https://docs.cloud.google.com/datastore/docs/concepts/queries#keys-only_queries) ) For a query related to metadata or statistics, see [Required Permissions for Metadata and Statistics](https://docs.cloud.google.com/datastore/docs/access/iam#required_permissions_for_metadata_and_statistics) . |
| [`runQuery`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/runQuery) with a [kindless query](https://docs.cloud.google.com/datastore/docs/concepts/queries#kindless_queries) | `datastore.entities.get` `datastore.entities.list` `datastore.statistics.get` `datastore.statistics.list`                                                                                                                                                                                                                                                                                        |

### Required Permissions for Metadata and Statistics

The following table lists permissions that the caller must have to call methods on [Metadata](https://docs.cloud.google.com/datastore/docs/concepts/metadataqueries) and [Statistics](https://docs.cloud.google.com/datastore/docs/concepts/stats) .

| Method                                                                                                                                          | Required Permission(s)                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| [`lookup`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/lookup) of entities with kind names matching **\_\_Stat\_\*\_\_** | `datastore.statistics.get`                             |
| [`runQuery`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/runQuery) using kinds with names matching **\_\_Stat\_\*\_\_**  | `datastore.statistics.get` `datastore.statistics.list` |
| [`runQuery`](https://docs.cloud.google.com/datastore/reference/rest/v1/projects/runQuery) using the kind **\_\_namespace\_\_**                  | `datastore.namespaces.get` `datastore.namespaces.list` |

### Required roles to create a Datastore mode database instance

To create a new Datastore mode database instance, you require either the [**Owner** role](https://docs.cloud.google.com/iam/docs/roles-overview#basic) or the [**Datastore Owner** role](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore) .

Datastore mode databases requires an active App Engine application. If the project doesn't have an application, Firestore in Datastore mode creates one for you. In that case, you require the `appengine.applications.create` permission from the **Owner** role or from an [IAM custom role](https://docs.cloud.google.com/iam/docs/creating-custom-roles) containing the permission.

## Role change latency

Firestore in Datastore mode caches IAM permissions for 5 minutes, so it will take up to 5 minutes for a role change to become effective.

## Managing IAM

You can get and set IAM policies using the Google Cloud console, the IAM methods, or the Google Cloud CLI.

- For the Google Cloud console, see [Access control using the Google Cloud console](https://docs.cloud.google.com/iam/docs/managing-policies#access_control_via_console) .
- For the IAM methods, see [Access control using the API](https://docs.cloud.google.com/iam/docs/managing-policies#access_control_via_api) .
- For the gcloud CLI, see [Access control using the gcloud tool](https://docs.cloud.google.com/iam/docs/managing-policies#access_control_via_the_gcloud_tool) .

## Configure conditional access permissions

You can use [IAM Conditions](https://docs.cloud.google.com/iam/docs/conditions-overview) to define and enforce conditional access control.

For example, the following condition assigns a principal the `datastore.user` role up until a specified date:

```
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

To learn how to define IAM Conditions for temporary access, see [Configure temporary access](https://docs.cloud.google.com/iam/docs/configuring-temporary-access) .

To learn how to configure IAM Conditions for access to one or more databases, see [Configure database access conditions](https://docs.cloud.google.com/datastore/docs/manage-databases#configure_per-database_access_permissions) .

## What's next

- Learn more about [IAM](https://docs.cloud.google.com/iam/docs) .
- [Grant IAM roles](https://docs.cloud.google.com/iam/docs/managing-policies) .
