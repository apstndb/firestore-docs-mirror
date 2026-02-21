Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. Recent updates to documents may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta2/{name=projects/*/databases/*}:exportDocuments  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Database to export. Should be of the form: `  projects/{projectId}/databases/{databaseId}  ` .

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
  &quot;collectionIds&quot;: [
    string
  ],
  &quot;outputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  collectionIds[]  `

`  string  `

Which collection ids to export. Unspecified means all collections.

`  outputUriPrefix  `

`  string  `

The output URI. Currently only supports Google Cloud Storage URIs of the form: `  gs://BUCKET_NAME[/NAMESPACE_PATH]  ` , where `  BUCKET_NAME  ` is the name of the Google Cloud Storage bucket and `  NAMESPACE_PATH  ` is an optional Google Cloud Storage namespace path. When choosing a name, be sure to consider Google Cloud Storage naming guidelines: <https://cloud.google.com/storage/docs/naming> . If the URI is a bucket (without a namespace path), a prefix will be generated based on the start time.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
