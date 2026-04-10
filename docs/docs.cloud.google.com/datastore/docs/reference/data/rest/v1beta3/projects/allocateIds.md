  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.response_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.AllocateIdsResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/allocateIds#try-it)

Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

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

  
`  POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:allocateIds  `

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

`  keys[]  `

`  object ( Key  ` )

Required. A list of keys with incomplete key paths for which to allocate IDs. No key may be reserved/read-only.

### Response body

The response for `  Datastore.AllocateIds  ` .

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

`  keys[]  `

`  object ( Key  ` )

The keys specified in the request (in the same order), each with its key path completed with a newly allocated ID.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
