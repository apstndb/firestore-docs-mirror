  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1beta1/projects/export#try-it)

Exports a copy of all or a subset of entities from Google Cloud Datastore to another storage system, such as Google Cloud Storage. Recent updates to entities may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

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

  
`  POST https://datastore.googleapis.com/v1beta1/projects/{projectId}:export  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Project ID against which to make the request.

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
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;entityFilter&quot;: {
    object (EntityFilter)
  },
  &quot;outputUrlPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  labels  `

`  map (key: string, value: string)  `

Client-assigned labels.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  entityFilter  `

`  object ( EntityFilter  ` )

Description of what data from the project is included in the export.

`  outputUrlPrefix  `

`  string  `

Location for the export metadata and data files.

The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So outputUrlPrefix should be of the form: `  gs://BUCKET_NAME[/NAMESPACE_PATH]  ` , where `  BUCKET_NAME  ` is the name of the Cloud Storage bucket and `  NAMESPACE_PATH  ` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace). For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) .

The resulting files will be nested deeper than the specified URL prefix. The final output URL will be provided in the `  google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url  ` field. That value should be used for subsequent projects.import operations.

By nesting the data files deeper, the same Cloud Storage bucket can be used in multiple projects.export operations without conflict.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
