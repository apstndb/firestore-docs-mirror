Lists all the backups.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{parent=projects/*/locations/*}/backups  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The location to list backups from.

Format is `  projects/{project}/locations/{location}  ` . Use `  {location} = '-'  ` to list backups from all locations for the given project. This allows listing backups from a single location or from all locations.

### Query parameters

Parameters

`  filter  `

`  string  `

An expression that filters the list of returned backups.

A filter expression consists of a field name, a comparison operator, and a value for filtering. The value must be a string, a number, or a boolean. The comparison operator must be one of: `  <  ` , `  >  ` , `  <=  ` , `  >=  ` , `  !=  ` , `  =  ` , or `  :  ` . Colon `  :  ` is the contains operator. Filter rules are not case sensitive.

The following fields in the `  Backup  ` are eligible for filtering:

  - `  databaseUid  ` (supports `  =  ` only)

### Request body

The request body must be empty.

### Response body

The response for `  FirestoreAdmin.ListBackups  ` .

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
  &quot;backups&quot;: [
    {
      object (Backup)
    }
  ],
  &quot;unreachable&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  backups[]  `

`  object ( Backup  ` )

List of all backups for the project.

`  unreachable[]  `

`  string  `

List of locations that existing backups were not able to be fetched from.

Instead of failing the entire requests when a single location is unreachable, this response returns a partial result set and list of locations unable to be reached here. The request can be retried against a single location to get a concrete error.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
