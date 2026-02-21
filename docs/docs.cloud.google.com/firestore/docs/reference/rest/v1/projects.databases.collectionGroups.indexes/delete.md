Deletes a composite index.

### HTTP request

`  DELETE https://firestore.googleapis.com/v1/{name=projects/*/databases/*/collectionGroups/*/indexes/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. A name of the form `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/indexes/{index_id}  `

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
