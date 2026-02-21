Metadata for the `  long-running operation  ` from the \[databases.restore\]\[google.firestore.admin.v1.RestoreDatabase\] request.

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
  &quot;backup&quot;: string,
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

The time the restore was started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

The time the restore finished, unset for ongoing restores.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  operationState  `

`  enum ( OperationState  ` )

The operation state of the restore.

`  database  `

`  string  `

The name of the database being restored to.

`  backup  `

`  string  `

The name of the backup restoring from.

`  progressPercentage  `

`  object ( Progress  ` )

How far along the restore is as an estimated percentage of remaining time.
