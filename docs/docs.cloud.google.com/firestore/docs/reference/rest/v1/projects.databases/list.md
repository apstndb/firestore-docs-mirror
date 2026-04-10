List all the databases in the project.

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

  
`  GET https://firestore.googleapis.com/v1/{parent=projects/*}/databases  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
