Imports documents into Google Cloud Firestore. Existing documents with the same name are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an databases.importDocuments operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Firestore.

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

  
`POST https://firestore.googleapis.com/v1beta1/{name=projects/*/databases/*}:importDocuments`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Database to import into. Should be of the form: `projects/{projectId}/databases/{databaseId}` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;collectionIds&quot;: [
    string
  ],
  &quot;inputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`collectionIds[]`

`string`

Which collection ids to import. Unspecified means all collections included in the import.

`inputUriPrefix`

`string`

Location of the exported files. This must match the outputUriPrefix of an ExportDocumentsResponse from an export that has completed successfully. See: `google.firestore.admin.v1beta1.ExportDocumentsResponse.output_uri_prefix` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
