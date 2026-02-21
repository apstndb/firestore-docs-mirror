  - [JSON representation](#SCHEMA_REPRESENTATION)

An event signifying a change in state of a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

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
  &quot;state&quot;: enum (MigrationState)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  state  `

`  enum ( MigrationState  ` )

The new state of the migration.
