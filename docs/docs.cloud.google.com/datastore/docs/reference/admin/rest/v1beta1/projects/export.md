  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Exports a copy of all or a subset of entities from Google Cloud Datastore to another storage system, such as Google Cloud Storage. Recent updates to entities may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

### HTTP request

`  POST https://datastore.googleapis.com/v1beta1/projects/{projectId}:export  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
