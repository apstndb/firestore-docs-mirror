Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. Recent updates to documents may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

For more details on export behavior and output format, refer to: <https://cloud.google.com/firestore/docs/manage-data/export-import>

### HTTP request

`  POST https://firestore.googleapis.com/v1/{name=projects/*/databases/*}:exportDocuments  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. Database to export. Should be of the form: `  projects/{projectId}/databases/{databaseId}  ` .

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
  &quot;collectionIds&quot;: [
    string
  ],
  &quot;outputUriPrefix&quot;: string,
  &quot;namespaceIds&quot;: [
    string
  ],
  &quot;snapshotTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  collectionIds[]  `

`  string  `

IDs of the collection groups to export. Unspecified means all collection groups. Each collection group in this list must be unique.

`  outputUriPrefix  `

`  string  `

The output URI. Currently only supports Google Cloud Storage URIs of the form: `  gs://BUCKET_NAME[/NAMESPACE_PATH]  ` , where `  BUCKET_NAME  ` is the name of the Google Cloud Storage bucket and `  NAMESPACE_PATH  ` is an optional Google Cloud Storage namespace path. When choosing a name, be sure to consider Google Cloud Storage naming guidelines: <https://cloud.google.com/storage/docs/naming> . If the URI is a bucket (without a namespace path), a prefix will be generated based on the start time.

`  namespaceIds[]  `

`  string  `

An empty list represents all namespaces. This is the preferred usage for databases that don't use namespaces.

An empty string element represents the default namespace. This should be used if the database has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique.

`  snapshotTime  `

`  string ( Timestamp  ` format)

The timestamp that corresponds to the version of the database to be exported. The timestamp must be in the past, rounded to the minute and not older than `  earliestVersionTime  ` . If specified, then the exported documents will represent a consistent view of the database at the provided time. Otherwise, there are no guarantees about the consistency of the exported documents.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
