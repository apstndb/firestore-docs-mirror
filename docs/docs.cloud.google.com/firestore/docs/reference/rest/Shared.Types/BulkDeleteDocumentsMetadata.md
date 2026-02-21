Metadata for `  google.longrunning.Operation  ` results from `  FirestoreAdmin.BulkDeleteDocuments  ` .

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
  &quot;progressDocuments&quot;: {
    object (Progress)
  },
  &quot;progressBytes&quot;: {
    object (Progress)
  },
  &quot;collectionIds&quot;: [
    string
  ],
  &quot;namespaceIds&quot;: [
    string
  ],
  &quot;snapshotTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

The time this operation started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

The time this operation completed. Will be unset if operation still in progress.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  operationState  `

`  enum ( OperationState  ` )

The state of the operation.

`  progressDocuments  `

`  object ( Progress  ` )

The progress, in documents, of this operation.

`  progressBytes  `

`  object ( Progress  ` )

The progress, in bytes, of this operation.

`  collectionIds[]  `

`  string  `

The IDs of the collection groups that are being deleted.

`  namespaceIds[]  `

`  string  `

Which namespace IDs are being deleted.

`  snapshotTime  `

`  string ( Timestamp  ` format)

The timestamp that corresponds to the version of the database that is being read to get the list of documents to delete. This time can also be used as the timestamp of PITR in case of disaster recovery (subject to PITR window limit).

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .
