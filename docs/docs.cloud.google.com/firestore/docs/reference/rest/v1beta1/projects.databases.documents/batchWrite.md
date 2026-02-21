Applies a batch of write operations.

The documents.batchWrite method does not apply the write operations atomically and can apply them out of order. Method does not allow more than one write per document. Each write succeeds or fails independently. See the `  BatchWriteResponse  ` for the success status of each write.

If you require an atomically applied set of writes, use `  documents.commit  ` instead.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:batchWrite  `

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
  &quot;labels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  writes[]  `

`  object ( Write  ` )

The writes to apply.

Method does not apply writes atomically and does not guarantee ordering. Each write succeeds or fails independently. You cannot write to the same document more than once per request.

`  labels  `

`  map (key: string, value: string)  `

Labels associated with this batch write.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

### Response body

The response from `  Firestore.BatchWrite  ` .

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
  &quot;status&quot;: [
    {
      object (Status)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  writeResults[]  `

`  object ( WriteResult  ` )

The result of applying the writes.

This i-th write result corresponds to the i-th write in the request.

`  status[]  `

`  object ( Status  ` )

The status of applying the writes.

This i-th write status corresponds to the i-th write in the request.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
