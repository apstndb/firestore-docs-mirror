## Resource: Backup

A Backup of a Cloud Firestore Database.

The backup contains all documents and index configurations for the given database at a specific point in time.

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
  &quot;name&quot;: string,
  &quot;database&quot;: string,
  &quot;databaseUid&quot;: string,
  &quot;snapshotTime&quot;: string,
  &quot;expireTime&quot;: string,
  &quot;state&quot;: enum (State)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The unique resource name of the Backup.

Format is `  projects/{project}/locations/{location}/backups/{backup}  ` .

`  database  `

`  string  `

Output only. Name of the Firestore database that the backup is from.

Format is `  projects/{project}/databases/{database}  ` .

`  databaseUid  `

`  string  `

Output only. The system-generated UUID4 for the Firestore database that the backup is from.

`  snapshotTime  `

`  string ( Timestamp  ` format)

Output only. The backup contains an externally consistent copy of the database at this time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  expireTime  `

`  string ( Timestamp  ` format)

Output only. The timestamp at which this backup expires.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  state  `

`  enum ( State  ` )

Output only. The current state of the backup.

## State

Indicate the current state of the backup.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  CREATING  `

The pending backup is still being created. Operations on the backup will be rejected in this state.

`  READY  `

The backup is complete and ready to use.

`  NOT_AVAILABLE  `

The backup is not available at this moment.

## Methods

### `             delete           `

Deletes a backup.

### `             get           `

Gets information about a backup.

### `             list           `

Lists all the backups.
