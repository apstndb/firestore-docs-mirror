Deletes an index.

### HTTP request

`  DELETE https://firestore.googleapis.com/v1beta1/{name=projects/*/databases/*/indexes/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

The index name. For example: `  projects/{projectId}/databases/{databaseId}/indexes/{index_id}  `

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
