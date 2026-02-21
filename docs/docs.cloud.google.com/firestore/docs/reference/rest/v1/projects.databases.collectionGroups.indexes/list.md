Lists composite indexes.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*/collectionGroups/*}/indexes  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}  `

### Query parameters

Parameters

`  filter  `

`  string  `

The filter to apply to list results.

`  pageSize  `

`  integer  `

The number of results to return.

`  pageToken  `

`  string  `

A page token, returned from a previous call to `  FirestoreAdmin.ListIndexes  ` , that may be used to get the next page of results.

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

The requested indexes.

`  nextPageToken  `

`  string  `

A page token that may be used to request another page of results. If blank, this is the last page.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
