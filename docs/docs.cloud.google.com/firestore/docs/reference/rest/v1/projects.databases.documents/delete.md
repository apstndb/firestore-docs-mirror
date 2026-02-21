Deletes a document.

### HTTP request

`  DELETE https://firestore.googleapis.com/v1/{name=projects/*/databases/*/documents/*/**}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The resource name of the Document to delete. In the format: `  projects/{projectId}/databases/{databaseId}/documents/{document_path}  ` .

### Query parameters

Parameters

`  currentDocument  `

`  object ( Precondition  ` )

An optional precondition on the document. The request will fail if this is set and not met by the target document.

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
