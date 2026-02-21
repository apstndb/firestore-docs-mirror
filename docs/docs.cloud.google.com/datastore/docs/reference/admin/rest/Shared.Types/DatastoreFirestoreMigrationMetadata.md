  - [JSON representation](#SCHEMA_REPRESENTATION)

Metadata for Datastore to Firestore migration operations.

The DatastoreFirestoreMigration operation is not started by the end-user via an explicit "creation" method. This is an intentional deviation from the LRO design pattern.

This singleton resource can be accessed at: "projects/{projectId}/operations/datastore-firestore-migration"

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;migrationState&quot;: enum (MigrationState),
  &quot;migrationStep&quot;: enum (MigrationStep)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  migrationState  `

`  enum ( MigrationState  ` )

The current state of migration from Cloud Datastore to Cloud Firestore in Datastore mode.

`  migrationStep  `

`  enum ( MigrationStep  ` )

The current step of migration from Cloud Datastore to Cloud Firestore in Datastore mode.
