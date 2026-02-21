Metadata for the `  long-running operation  ` from the \[databases.clone\]\[google.firestore.admin.v1.CloneDatabase\] request.

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
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string,
  &quot;operationState&quot;: enum (OperationState),
  &quot;database&quot;: string,
  &quot;pitrSnapshot&quot;: {
    object (PitrSnapshot)
  },
  &quot;progressPercentage&quot;: {
    object (Progress)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

The time the clone was started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

The time the clone finished, unset for ongoing clones.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  operationState  `

`  enum ( OperationState  ` )

The operation state of the clone.

`  database  `

`  string  `

The name of the database being cloned to.

`  pitrSnapshot  `

`  object ( PitrSnapshot  ` )

The snapshot from which this database was cloned.

`  progressPercentage  `

`  object ( Progress  ` )

How far along the clone is as an estimated percentage of remaining time.

## PitrSnapshot

A consistent snapshot of a database at a specific point in time. A PITR (Point-in-time recovery) snapshot with previous versions of a database's data is available for every minute up to the associated database's data retention period. If the PITR feature is enabled, the retention period is 7 days; otherwise, it is one hour.

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
  &quot;database&quot;: string,
  &quot;databaseUid&quot;: string,
  &quot;snapshotTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  database  `

`  string  `

Required. The name of the database that this was a snapshot of. Format: `  projects/{project}/databases/{database}  ` .

`  databaseUid  `

`  string ( bytes format)  `

Output only. Public UUID of the database the snapshot was associated with.

A base64-encoded string.

`  snapshotTime  `

`  string ( Timestamp  ` format)

Required. Snapshot time of the database.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .
