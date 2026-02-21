List all the databases in the project.

### HTTP request

`  GET https://firestore.googleapis.com/v1/{parent=projects/*}/databases  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}  `

### Query parameters

Parameters

`  showDeleted  `

`  boolean  `

If true, also returns deleted resources.

### Request body

The request body must be empty.

### Response body

The list of databases for a project.

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
  &quot;databases&quot;: [
    {
      object (Database)
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

`  databases[]  `

`  object ( Database  ` )

The databases in the project.

`  unreachable[]  `

`  string  `

In the event that data about individual databases cannot be listed they will be recorded here.

An example entry might be: projects/some\_project/locations/some\_location This can happen if the Cloud Region that the Database resides in is currently unavailable. In this case we can't fetch all the details about the database. You may be able to get a more detailed error message (or possibly fetch the resource) by sending a 'Get' request for the resource or a 'List' request for the specific location.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
