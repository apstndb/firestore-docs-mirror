Starts a new transaction.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:beginTransaction  `

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
  &quot;options&quot;: {
    object (TransactionOptions)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  options  `

`  object ( TransactionOptions  ` )

The options for the transaction. Defaults to a read-write transaction.

### Response body

The response for `  Firestore.BeginTransaction  ` .

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
  &quot;transaction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transaction  `

`  string ( bytes format)  `

The transaction that was started.

A base64-encoded string.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
