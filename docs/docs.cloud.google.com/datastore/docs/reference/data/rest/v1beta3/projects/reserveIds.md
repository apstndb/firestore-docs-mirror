  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/reserveIds#try-it)

Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

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

  
`  POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:reserveIds  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. The ID of the project against which to make the request.

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
  &quot;databaseId&quot;: string,
  &quot;keys&quot;: [
    {
      object (Key)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  databaseId  `

`  string  `

The ID of the database against which to make the request.

'(default)' is not allowed; please use empty string '' to refer the default database.

`  keys[]  `

`  object ( Key  ` )

Required. A list of keys with complete key paths whose numeric IDs should not be auto-allocated.

### Response body

If successful, the response body is empty.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
