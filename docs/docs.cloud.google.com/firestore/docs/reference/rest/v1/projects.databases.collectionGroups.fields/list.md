Lists the field configuration and metadata for this database.

Currently, `  FirestoreAdmin.ListFields  ` only supports listing fields that have been explicitly overridden. To issue this query, call `  FirestoreAdmin.ListFields  ` with the filter set to `  indexConfig.usesAncestorConfig:false  ` or `  ttlConfig:*  ` .

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

  
`  GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*/collectionGroups/*}/fields  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}  `

### Query parameters

Parameters

`  filter  `

`  string  `

The filter to apply to list results. Currently, `  FirestoreAdmin.ListFields  ` only supports listing fields that have been explicitly overridden. To issue this query, call `  FirestoreAdmin.ListFields  ` with a filter that includes `  indexConfig.usesAncestorConfig:false  ` or `  ttlConfig:*  ` .

`  pageSize  `

`  integer  `

The number of results to return.

`  pageToken  `

`  string  `

A page token, returned from a previous call to `  FirestoreAdmin.ListFields  ` , that may be used to get the next page of results.

### Request body

The request body must be empty.

### Response body

The response for `  FirestoreAdmin.ListFields  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: [
    {
      object (Field)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fields[]  `

`  object ( Field  ` )

The requested fields.

`  nextPageToken  `

`  string  `

A page token that may be used to request another page of results. If blank, this is the last page.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
