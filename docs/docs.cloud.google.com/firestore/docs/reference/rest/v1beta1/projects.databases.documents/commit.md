Commits a transaction, while optionally updating documents.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:commit  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  database  `

`  string  `

Required. The database name. In the format: `  projects/{projectId}/databases/{databaseId}  ` .

### Request body

The request body contains data with the following structure:

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
  &quot;writes&quot;: [
    {
      object (Write)
    }
  ],
  &quot;transaction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  writes[]  `

`  object ( Write  ` )

The writes to apply.

Always executed atomically and in order.

`  transaction  `

`  string ( bytes format)  `

If set, applies all writes in this transaction, and commits it.

A base64-encoded string.

### Response body

The response for `  Firestore.Commit  ` .

If successful, the response body contains data with the following structure:

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
  &quot;writeResults&quot;: [
    {
      object (WriteResult)
    }
  ],
  &quot;commitTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  writeResults[]  `

`  object ( WriteResult  ` )

The result of applying the writes.

This i-th write result corresponds to the i-th write in the request.

`  commitTime  `

`  string ( Timestamp  ` format)

The time at which the commit occurred. Any read with an equal or greater `  readTime  ` is guaranteed to see the effects of the commit.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
