Rolls back a transaction.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:rollback  `

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
  &quot;transaction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transaction  `

`  string ( bytes format)  `

Required. The transaction to roll back.

A base64-encoded string.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
