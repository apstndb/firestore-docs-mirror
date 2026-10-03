---
name: documents/docs.cloud.google.com/firestore/mongodb-compatibility/docs/security/iam
uri: https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/security/iam
title: Identity and Access Management (IAM)
description: How to use Identity and Access Management to manage access to Firestore with MongoDB compatibility databases.
data_source: docs.cloud.google.com
---

# Identity and Access Management (IAM)

Manage access to your resources with Identity and Access Management (IAM). IAM lets you give more granular access to specific Google Cloud resources and prevents unwanted access to other resources. This page describes the IAM permissions and roles for Firestore. For a detailed description of IAM, read the [IAM documentation](https://cloud.google.com/iam/docs/) .

IAM lets you adopt the [security principle of least privilege](https://wikipedia.org/wiki/Principle_of_least_privilege) , so you grant only the necessary access to your resources.

IAM lets you control **who (user)** has **what (role)** permission for **which** resources by setting IAM policies. IAM policies grant one or more roles to a user, giving the user certain permissions. For example, you can grant the `datastore.indexAdmin` role to a user, which allows the user to create, modify, delete, list, or view indexes.

## Permissions and roles

This section summarizes the permissions and roles that Firestore supports.

> **Note:** Some Firestore with MongoDB compatibility permissions differ from the standard IAM model permissions. For example, in the IAM model, the `datastore.databases.get` permission lets you return a database object while, in Firestore with MongoDB compatibility, `datastore.databases.get` lets you begin or roll back a transaction. To retrieve a database object's information, use the `datastore.databases.getMetadata` permission.
>
> The `datastore.schemas.*` permissions were previously named `datastore.indexes.*` . You can still use `datastore.indexes` as an alias for `datastore.schemas` .

### Required permissions for API methods

The following table lists the permissions that the caller must have to perform each action:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Required permissions</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>projects.databases.MongoDBCompatible</code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code>ListDatabases</code></td>
<td><code>datastore.databases.getMetadata</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>ListIndexes</code></td>
<td><code>datastore.schemas.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>Find</code></td>
<td><code>datastore.entities.get</code><br />
<code>datastore.entities.list</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>Aggregate</code></td>
<td><code>datastore.entities.get</code><br />
<code>datastore.entities.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>GetMore</code></td>
<td><p>The same permissions that were required by the call that created the cursor.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>ListCollections</code></td>
<td><code>datastore.entities.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>Count</code></td>
<td><code>datastore.entities.list</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>Distinct</code></td>
<td><code>datastore.entities.get</code><br />
<code>datastore.entities.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>CommitTransaction</code></td>
<td><code>datastore.databases.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>AbortTransaction</code></td>
<td><code>datastore.databases.get</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>EndSessions</code></td>
<td><code>datastore.databases.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>KillCursors</code></td>
<td><code>datastore.databases.get</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>Insert</code></td>
<td><code>datastore.entities.create</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>Update</code></td>
<td><code>datastore.entities.get</code><br />
<code>datastore.entities.list</code><br />
<code>datastore.entities.update</code><br />
<code>datastore.entities.create</code> (for upsert only)</td>
<td></td>
</tr>
<tr class="even">
<td><code>FindAndModify</code></td>
<td><code>datastore.entities.get</code><br />
<code>datastore.entities.list</code><br />
<code>datastore.entities.update</code> (for replace or update only)<br />
<code>datastore.entities.create</code> (for upsert only)<br />
<code>datastore.entities.delete</code> (for delete only)<br />
</td>
<td></td>
</tr>
<tr class="odd">
<td><code>CreateCollection</code></td>
<td><code>datastore.entities.create</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>DropCollection</code></td>
<td><code>datastore.schemas.delete</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>projects.databases.indexes</code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/latest/projects.databases.indexes/create"><code>create</code></a></td>
<td><code>datastore.schemas.create</code></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/latest/projects.databases.indexes/delete"><code>delete</code></a></td>
<td><code>datastore.schemas.delete</code></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/latest/projects.databases.indexes/get"><code>get</code></a></td>
<td><code>datastore.schemas.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/latest/projects.databases.indexes/list"><code>list</code></a></td>
<td><code>datastore.schemas.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>projects.databases</code></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/create"><code>create</code></a></td>
<td><code>datastore.databases.create</code></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/delete"><code>delete</code></a></td>
<td><code>datastore.databases.delete</code></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/get"><code>get</code></a></td>
<td><code>datastore.databases.getMetadata</code></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/list"><code>list</code></a></td>
<td><code>datastore.databases.list</code></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/patch"><code>patch</code></a></td>
<td><code>datastore.databases.update</code></td>
<td></td>
</tr>
<tr class="even">
<td>restore</td>
<td><code>datastore.backups.restoreDatabase</code></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/clone"><code>clone</code></a></td>
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
</tr>
<tr class="even">
<td><code>projects.locations</code></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/get"><code>get</code></a></td>
<td><code>datastore.locations.get</code></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/list"><code>list</code></a></td>
<td><code>datastore.locations.list</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>projects.databases.backupschedules</code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code>get</code></td>
<td><code>datastore.backupSchedules.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>list</code></td>
<td><code>datastore.backupSchedules.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>create</code></td>
<td><code>datastore.backupSchedules.create</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>update</code></td>
<td><code>datastore.backupSchedules.update</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>delete</code></td>
<td><code>datastore.backupSchedules.delete</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>projects.locations.backups</code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code>get</code></td>
<td><code>datastore.backups.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>list</code></td>
<td><code>datastore.backups.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>delete</code></td>
<td><code>datastore.backups.delete</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>projects.databases.usercreds</code></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><code>get</code></td>
<td><code>datastore.userCreds.get</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>list</code></td>
<td><code>datastore.userCreds.list</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>create</code></td>
<td><code>datastore.userCreds.create</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>enable</code></td>
<td><code>datastore.userCreds.update</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>disable</code></td>
<td><code>datastore.userCreds.update</code></td>
<td></td>
</tr>
<tr class="odd">
<td><code>resetPassword</code></td>
<td><code>datastore.userCreds.update</code></td>
<td></td>
</tr>
<tr class="even">
<td><code>delete</code></td>
<td><code>datastore.userCreds.delete</code></td>
<td></td>
</tr>
</tbody>
</table>

### Predefined roles

With IAM, every API method in Firestore requires that the account making the API request has the appropriate permissions to use the resource. Permissions are granted by setting policies that grant roles to a user, group, or service account. In addition to the primitive roles, [owner, editor, and viewer](https://cloud.google.com/iam/docs/understanding-roles#primitive_roles) , you can grant Firestore roles to the users of your project.

The following table lists the Firestore IAM roles. You can grant multiple roles to a user, group, or service account.

| Role                                    | Permissions                                                                                                                                                                                                                                                                                                                                                                                          | Description                                                                                                                                                      |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `roles/datastore.owner`                 | `appengine.applications.get` `datastore.*` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                                                                                                                                                            | Full access to Firestore.                                                                                                                                        |
| `roles/datastore.user`                  | `appengine.applications.get` `datastore.databases.get` `datastore.databases.getMetadata` `datastore.databases.list` `datastore.entities.*` `datastore.schemas.list` `datastore.namespaces.get` `datastore.namespaces.list` `datastore.statistics.get` `datastore.statistics.list` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                     | Read/write access to data in a Firestore database. Intended for application developers and service accounts.                                                     |
| `roles/datastore.viewer`                | `appengine.applications.get` `datastore.databases.get` `datastore.databases.getMetadata` `datastore.databases.list` `datastore.entities.get` `datastore.entities.list` `datastore.schemas.get` `datastore.schemas.list` `datastore.namespaces.get` `datastore.namespaces.list` `datastore.statistics.get` `datastore.statistics.list` `resourcemanager.projects.get` `resourcemanager.projects.list` | Read access to all Firestore resources.                                                                                                                          |
| `roles/datastore.indexAdmin`            | `appengine.applications.get` `datastore.databases.getMetadata` `datastore.schemas.*` `datastore.operations.list` `datastore.operations.get` `resourcemanager.projects.get` `resourcemanager.projects.list`                                                                                                                                                                                           | Full access to manage index definitions.                                                                                                                         |
| `roles/datastore.backupSchedulesViewer` | `datastore.backupSchedules.get` `datastore.backupSchedules.list`                                                                                                                                                                                                                                                                                                                                     | Read access to backup schedules in a Firestore database.                                                                                                         |
| `roles/datastore.backupSchedulesAdmin`  | `datastore.backupSchedules.get` `datastore.backupSchedules.list` `datastore.backupSchedules.create` `datastore.backupSchedules.update` `datastore.backupSchedules.delete` `datastore.databases.list` `datastore.databases.getMetadata`                                                                                                                                                               | Full access to backup schedules in a Firestore database.                                                                                                         |
| `roles/datastore.backupsViewer`         | `datastore.backups.get` `datastore.backups.list`                                                                                                                                                                                                                                                                                                                                                     | Read access to backup information in a Firestore location.                                                                                                       |
| `roles/datastore.backupsAdmin`          | `datastore.backups.get` `datastore.backups.list` `datastore.backups.delete`                                                                                                                                                                                                                                                                                                                          | Full access to backups in a Firestore location.                                                                                                                  |
| `roles/datastore.restoreAdmin`          | `datastore.backups.get` `datastore.backups.list` `datastore.backups.restoreDatabase` `datastore.databases.list` `datastore.databases.create` `datastore.databases.getMetadata` `datastore.operations.list` `datastore.operations.get`                                                                                                                                                                | Ability to restore a Firestore backup into a new database. This role also gives the ability to create new databases, not necessarily by restoring from a backup. |
| `roles/datastore.cloneAdmin`            | `datastore.databases.clone` `datastore.databases.list` `datastore.databases.create` `datastore.databases.getMetadata` `datastore.operations.list` `datastore.operations.get`                                                                                                                                                                                                                         | Ability to clone a Firestore database into a new database. This role also gives the ability to create new databases, not necessarily by cloning.                 |
| `roles/datastore.statisticsViewer`      | `resourcemanager.projects.get` `resourcemanager.projects.list` `datastore.databases.getMetadata` `datastore.insights.get` `datastore.keyVisualizerScans.get` `datastore.keyVisualizerScans.list` `datastore.statistics.list` `datastore.statistics.get`                                                                                                                                              | Read access to Insights, Stats, and Key Visualizer scans.                                                                                                        |
| `roles/datastore.userCredsViewer`       | `datastore.userCreds.get` `datastore.userCreds.list`                                                                                                                                                                                                                                                                                                                                                 | Read access to user credentials in a Firestore database.                                                                                                         |
| `roles/datastore.userCredsAdmin`        | `datastore.userCreds.get` `datastore.userCreds.list` `datastore.userCreds.create` `datastore.userCreds.update` `datastore.userCreds.delete` `datastore.databases.list` `datastore.databases.getMetadata`                                                                                                                                                                                             | Full access to user credentials in a Firestore database.                                                                                                         |

### Custom roles

If the predefined roles do not address your business requirements, you can define your own custom roles with permissions that you specify:

- [Learn about custom roles.](https://cloud.google.com/iam/docs/understanding-custom-roles)
- [Create and manage custom roles.](https://cloud.google.com/iam/docs/creating-custom-roles)

#### Required roles to create and manage tags

If any tag is represented in create or restore actions, some roles are required. See [Creating and managing tags](https://cloud.google.com/resource-manager/docs/tags/tags-creating-and-managing) for more details on creating tag key-value pairs before associate them to the database resources.

The following listed permissions are required.

##### View tags

- `datastore.databases.listTagBindings`
- `datastore.databases.listEffectiveTags`

##### Manage tags on resources

The following permission is required for the database resource you're attaching the tag value.

- `datastore.databases.createTagBinding`

### Permissions

The following table lists the permissions that Firestore supports.

| Database permission name                       | Description                                                                                                    |     |
|------------------------------------------------|----------------------------------------------------------------------------------------------------------------|-----|
| `datastore.databases.get`                      | Begin or rollback a transaction.                                                                               |     |
| `datastore.databases.getMetadata`              | Read metadata from a database.                                                                                 |     |
| `datastore.databases.list`                     | List databases in a project.                                                                                   |     |
| `datastore.databases.create`                   | Create a database.                                                                                             |     |
| `datastore.databases.update`                   | Update a database.                                                                                             |     |
| `datastore.databases.delete`                   | Delete a database.                                                                                             |     |
| `datastore.databases.clone`                    | Clone a database.                                                                                              |     |
| `datastore.databases.createTagBinding`         | Create a tag binding for a database.                                                                           |     |
| `datastore.databases.deleteTagBinding`         | Delete a tag binding for a database.                                                                           |     |
| `datastore.databases.listTagBindings`          | List all tag bindings for a database.                                                                          |     |
| `datastore.databases.listEffectiveTagBindings` | List effective tag bindings for a database.                                                                    |     |
| Entity permission name                         | Description                                                                                                    |     |
| `datastore.entities.create`                    | Create a document.                                                                                             |     |
| `datastore.entities.delete`                    | Delete a document.                                                                                             |     |
| `datastore.entities.get`                       | Read a document.                                                                                               |     |
| `datastore.entities.list`                      | List the names of documents in a project. ( `datastore.entities.get` is required to access the document data.) |     |
| `datastore.entities.update`                    | Update a document.                                                                                             |     |
| Index permission name                          | Description                                                                                                    |     |
| `datastore.schemas.create`                     | Create an index.                                                                                               |     |
| `datastore.schemas.delete`                     | Delete an index.                                                                                               |     |
| `datastore.schemas.get`                        | Read metadata from an index.                                                                                   |     |
| `datastore.schemas.list`                       | List the indexes in a project.                                                                                 |     |
| `datastore.schemas.update`                     | Update an index.                                                                                               |     |
| Operation permission name                      | Description                                                                                                    |     |
| `datastore.operations.cancel`                  | Cancel a long-running operation.                                                                               |     |
| `datastore.operations.delete`                  | Delete a long-running operation.                                                                               |     |
| `datastore.operations.get`                     | Gets the latest state of a long-running operation.                                                             |     |
| `datastore.operations.list`                    | List long-running operations.                                                                                  |     |
| Project permission name                        | Description                                                                                                    |     |
| `resourcemanager.projects.get`                 | Browse resources in the project.                                                                               |     |
| `resourcemanager.projects.list`                | List owned projects.                                                                                           |     |
| Location permission name                       | Description                                                                                                    |     |
| `datastore.locations.get`                      | Get details about a database location. Required to create a new database.                                      |     |
| `datastore.locations.list`                     | List available database locations. Required to create a new database.                                          |     |
| Key Visualizer permission name                 | Description                                                                                                    |     |
| `datastore.keyVisualizerScans.get`             | Get details about Key Visualizer scans.                                                                        |     |
| `datastore.keyVisualizerScans.list`            | List available Key Visualizer scans.                                                                           |     |
| Backup Schedule permission name                | Description                                                                                                    |     |
| `datastore.backupSchedules.get`                | Get details about a backup schedule.                                                                           |     |
| `datastore.backupSchedules.list`               | List available backup schedules.                                                                               |     |
| `datastore.backupSchedules.create`             | Create a backup schedule.                                                                                      |     |
| `datastore.backupSchedules.update`             | Update a backup schedule.                                                                                      |     |
| `datastore.backupSchedules.delete`             | Delete a backup schedule.                                                                                      |     |
| Backup permission name                         | Description                                                                                                    |     |
| `datastore.backups.get`                        | Get details about a backup.                                                                                    |     |
| `datastore.backups.list`                       | List available backups.                                                                                        |     |
| `datastore.backups.delete`                     | Delete a backup.                                                                                               |     |
| `datastore.backups.restoreDatabase`            | Restore a database from a backup.                                                                              |     |
| Insights permission name                       | Description                                                                                                    |     |
| `datastore.insights.get`                       | Get insights of a resource                                                                                     |     |
| User credentials permission name               | Description                                                                                                    |     |
| `datastore.userCreds.get`                      | Get details about user credentials.                                                                            |     |
| `datastore.userCreds.list`                     | List available user credentials.                                                                               |     |
| `datastore.userCreds.create`                   | Create user credentials.                                                                                       |     |
| `datastore.userCreds.update`                   | Enable or disable user credentials, or reset a user password.                                                  |     |
| `datastore.userCreds.delete`                   | Delete user credentials.                                                                                       |     |

## Role change latency

Firestore caches IAM permissions for 5 minutes, so it takes up to 5 minutes for a role change to become effective.

## Managing Firestore IAM

You can get and set IAM policies using the Google Cloud console, the IAM API, or the `gcloud` command-line tool. See [Granting, Changing, and Revoking Access to Project Members](https://cloud.google.com/iam/docs/granting-changing-revoking-access) for details.

## Configure conditional access permissions

You can use [IAM Conditions](https://cloud.google.com/iam/docs/conditions-overview) to define and enforce conditional access control.

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

To learn how to define IAM Conditions for temporary access, see [Configure temporary access](https://cloud.google.com/iam/docs/configuring-temporary-access) .

To learn how to configure IAM Conditions for access to one or more databases, see [Configure database access conditions](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/create-databases#configure_per-database_access_permissions) .

## What's next

- Learn more about [IAM](https://cloud.google.com/iam/docs/) .
- [Grant IAM roles](https://cloud.google.com/iam/docs/granting-changing-revoking-access) .
- Learn about [authentication](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/connect) .
