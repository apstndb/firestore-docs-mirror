Lists operations that match the specified filter in the request. If the server doesn't support this method, it returns `  UNIMPLEMENTED  ` .

### HTTP request

`  GET https://firestore.googleapis.com/v1/{name=projects/*/databases/*}/operations  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

The name of the operation's parent resource.

### Query parameters

Parameters

`  filter  `

`  string  `

The standard list filter.

`  pageSize  `

`  integer  `

The standard list page size.

`  pageToken  `

`  string  `

The standard list page token.

`  returnPartialSuccess  `

`  boolean  `

When set to `  true  ` , operations that are reachable are returned as normal, and those that are unreachable are returned in the `  ListOperationsResponse.unreachable  ` field.

This can only be `  true  ` when reading across collections. For example, when `  parent  ` is set to `  "projects/example/locations/-"  ` .

This field is not supported by default and will result in an `  UNIMPLEMENTED  ` error if set unless explicitly documented otherwise in service or product specific documentation.

### Request body

The request body must be empty.

### Response body

The response message for `  Operations.ListOperations  ` .

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
  &quot;operations&quot;: [
    {
      object (Operation)
    }
  ],
  &quot;nextPageToken&quot;: string,
  &quot;unreachable&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  operations[]  `

`  object ( Operation  ` )

A list of operations that matches the specified filter in the request.

`  nextPageToken  `

`  string  `

The standard List next-page token.

`  unreachable[]  `

`  string  `

Unordered list. Unreachable resources. Populated when the request sets `  ListOperationsRequest.return_partial_success  ` and reads across collections. For example, when attempting to list all resources across all supported locations.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
