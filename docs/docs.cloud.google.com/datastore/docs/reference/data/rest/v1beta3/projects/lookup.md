  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.LookupResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

Looks up entities by key.

### HTTP request

`  POST https://datastore.googleapis.com/v1beta3/projects/{projectId}:lookup  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;readOptions&quot;: {
    object (ReadOptions)
  },
  &quot;keys&quot;: [
    {
      object (Key)
    }
  ],
  &quot;propertyMask&quot;: {
    object (PropertyMask)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  readOptions  `

`  object ( ReadOptions  ` )

The options for this lookup request.

`  keys[]  `

`  object ( Key  ` )

Required. Keys of entities to look up.

`  propertyMask  `

`  object ( PropertyMask  ` )

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;found&quot;: [
    {
      object (EntityResult)
    }
  ],
  &quot;missing&quot;: [
    {
      object (EntityResult)
    }
  ],
  &quot;deferred&quot;: [
    {
      object (Key)
    }
  ],
  &quot;readTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  found[]  `

`  object ( EntityResult  ` )

Entities found as `  ResultType.FULL  ` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`  missing[]  `

`  object ( EntityResult  ` )

Entities not found as `  ResultType.KEY_ONLY  ` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`  deferred[]  `

`  object ( Key  ` )

A list of keys that were not looked up due to resource constraints. The order of results in this field is undefined and has no relation to the order of the keys in the input.

`  readTime  `

`  string ( Timestamp  ` format)

The time at which these entities were read or found missing.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
