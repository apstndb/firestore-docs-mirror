Lists the indexes that match the specified filters.

### HTTP request

`  GET https://firestore.googleapis.com/v1beta1/{parent=projects/*/databases/*}/indexes  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

The database name. For example: `  projects/{projectId}/databases/{databaseId}  `

### Query parameters

Parameters

`  filter  `

`  string  `

`  pageSize  `

`  integer  `

The standard List page size.

`  pageToken  `

`  string  `

The standard List page token.

### Request body

The request body must be empty.

### Response body

The response for `  FirestoreAdmin.ListIndexes  ` .

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
  &quot;indexes&quot;: [
    {
      object (Index)
    }
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  indexes[]  `

`  object ( Index  ` )

The indexes.

`  nextPageToken  `

`  string  `

The standard List next-page token.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
