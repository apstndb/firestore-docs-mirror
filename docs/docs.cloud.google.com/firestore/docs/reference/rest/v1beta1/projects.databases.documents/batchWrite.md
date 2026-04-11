Applies a batch of write operations.

The documents.batchWrite method does not apply the write operations atomically and can apply them out of order. Method does not allow more than one write per document. Each write succeeds or fails independently. See the `  BatchWriteResponse  ` for the success status of each write.

If you require an atomically applied set of writes, use `  documents.commit  ` instead.

### HTTP request

Choose a location:

global

africa-south1

asia-east1

asia-east2

asia-northeast1

asia-northeast2

asia-northeast3

asia-south1

asia-south2

asia-southeast1

asia-southeast2

asia-southeast3

australia-southeast1

australia-southeast2

europe-central2

europe-north1

europe-north2

europe-southwest1

europe-west1

europe-west10

europe-west12

europe-west2

europe-west3

europe-west4

europe-west6

europe-west8

europe-west9

me-central1

me-central2

me-west1

northamerica-northeast1

northamerica-northeast2

northamerica-south1

southamerica-east1

southamerica-west1

us-central1

us-east1

us-east4

us-east5

us-south1

us-west1

us-west2

us-west3

us-west4

eu

us

  
`POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:batchWrite`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`database`

`string`

Required. The database name. In the format: `projects/{projectId}/databases/{databaseId}` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;writes&quot;: [{object (Write)}],&quot;labels&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`writes[]`

` object ( Write  ` )

The writes to apply.

Method does not apply writes atomically and does not guarantee ordering. Each write succeeds or fails independently. You cannot write to the same document more than once per request.

`labels`

`map (key: string, value: string)`

Labels associated with this batch write.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;writeResults&quot;: [{object (WriteResult)}],&quot;status&quot;: [{object (Status)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`writeResults[]`

` object ( WriteResult  ` )

The result of applying the writes.

This i-th write result corresponds to the i-th write in the request.

`status[]`

` object ( Status  ` )

The status of applying the writes.

This i-th write status corresponds to the i-th write in the request.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
