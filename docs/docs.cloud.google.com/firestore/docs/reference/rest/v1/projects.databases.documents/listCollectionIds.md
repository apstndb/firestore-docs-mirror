Lists all the collection IDs underneath a document.

### HTTP request

`  POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*/documents}:listCollectionIds  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent document. In the format: `  projects/{projectId}/databases/{databaseId}/documents/{document_path}  ` . For example: `  projects/my-project/databases/my-database/documents/chatrooms/my-chatroom  `

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
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string,

  // Union field consistency_selector can be only one of the following:
  &quot;readTime&quot;: string
  // End of list of possible types for union field consistency_selector.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  pageSize  `

`  integer  `

The maximum number of results to return.

`  pageToken  `

`  string  `

A page token. Must be a value from `  ListCollectionIdsResponse  ` .

Union field `  consistency_selector  ` . The consistency mode for this request. If not set, defaults to strong consistency. `  consistency_selector  ` can be only one of the following:

`  readTime  `

`  string ( Timestamp  ` format)

Reads documents as they were at the given time.

This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Response body

The response from `  Firestore.ListCollectionIds  ` .

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
  &quot;collectionIds&quot;: [
    string
  ],
  &quot;nextPageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  collectionIds[]  `

`  string  `

The collection ids.

`  nextPageToken  `

`  string  `

A page token that may be used to continue the list.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
