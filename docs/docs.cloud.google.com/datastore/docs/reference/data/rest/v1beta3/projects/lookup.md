  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.request_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.response_body)
      - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.LookupResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/projects/lookup#try-it)

Looks up entities by key.

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

  
`POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:lookup`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`projectId`

`string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;readOptions&quot;: {object (ReadOptions)},&quot;keys&quot;: [{object (Key)}],&quot;propertyMask&quot;: {object (PropertyMask)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`readOptions`

` object ( ReadOptions  ` )

The options for this lookup request.

`keys[]`

`object ( Key` )

Required. Keys of entities to look up.

`propertyMask`

` object ( PropertyMask  ` )

The properties to return. Defaults to returning all properties.

If this field is set and an entity has a property not referenced in the mask, it will be absent from \[LookupResponse.found.entity.properties\]\[\].

The entity's key is always returned.

### Response body

The response for `  Datastore.Lookup  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;found&quot;: [{object (EntityResult)}],&quot;missing&quot;: [{object (EntityResult)}],&quot;deferred&quot;: [{object (Key)}],&quot;readTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`found[]`

` object ( EntityResult  ` )

Entities found as `ResultType.FULL` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`missing[]`

` object ( EntityResult  ` )

Entities not found as `ResultType.KEY_ONLY` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`deferred[]`

`object ( Key` )

A list of keys that were not looked up due to resource constraints. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`readTime`

` string ( Timestamp  ` format)

The time at which these entities were read or found missing.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
