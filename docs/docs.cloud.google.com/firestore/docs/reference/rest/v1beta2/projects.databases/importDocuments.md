Imports documents into Google Cloud Firestore. Existing documents with the same name are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an databases.importDocuments operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Firestore.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta2/{name=projects/*/databases/*}:importDocuments  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Database to import into. Should be of the form: `  projects/{projectId}/databases/{databaseId}  ` .

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
  &quot;inputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  collectionIds[]  `

`  string  `

Which collection ids to import. Unspecified means all collections included in the import.

`  inputUriPrefix  `

`  string  `

Location of the exported files. This must match the outputUriPrefix of an ExportDocumentsResponse from an export that has completed successfully. See: `  google.firestore.admin.v1beta2.ExportDocumentsResponse.output_uri_prefix  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
