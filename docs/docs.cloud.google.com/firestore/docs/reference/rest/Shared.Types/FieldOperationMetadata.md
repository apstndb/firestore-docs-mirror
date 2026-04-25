Metadata for `  google.longrunning.Operation  ` results from `  FirestoreAdmin.UpdateField  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;field&quot;: string,&quot;indexConfigDeltas&quot;: [{object (IndexConfigDelta)}],&quot;state&quot;: enum (OperationState),&quot;progressDocuments&quot;: {object (Progress)},&quot;progressBytes&quot;: {object (Progress)},&quot;ttlConfigDelta&quot;: {object (TtlConfigDelta)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`startTime`

` string ( Timestamp  ` format)

The time this operation started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime`

` string ( Timestamp  ` format)

The time this operation completed. Will be unset if operation still in progress.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`field`

`string`

The field resource that this operation is acting on. For example: `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/fields/{fieldPath}`

`indexConfigDeltas[]`

` object ( IndexConfigDelta  ` )

A list of `  IndexConfigDelta  ` , which describe the intent of this operation.

`state`

` enum ( OperationState  ` )

The state of the operation.

`progressDocuments`

` object ( Progress  ` )

The progress, in documents, of this operation.

`progressBytes`

` object ( Progress  ` )

The progress, in bytes, of this operation.

`ttlConfigDelta`

` object ( TtlConfigDelta  ` )

Describes the deltas of TTL configuration.

## IndexConfigDelta

Information about an index configuration change.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;changeType&quot;: enum (ChangeType),&quot;index&quot;: {object (Index)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`changeType`

` enum ( ChangeType  ` )

Specifies how the index is changing.

`index`

` object ( Index  ` )

The index being changed.

## TtlConfigDelta

Information about a TTL configuration change.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;changeType&quot;: enum (ChangeType),&quot;expirationOffset&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`changeType`

`enum ( ChangeType` )

Specifies how the TTL configuration is changing.

`expirationOffset`

` string ( Duration  ` format)

The offset, relative to the timestamp value in the TTL-enabled field, used determine the document's expiration time.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .
