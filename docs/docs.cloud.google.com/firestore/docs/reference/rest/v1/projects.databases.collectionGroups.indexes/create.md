Creates a composite index. This returns a `  google.longrunning.Operation  ` which may be used to track the status of the creation. The metadata for the operation will be the type `  IndexOperationMetadata  ` .

### HTTP request

`  POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*/collectionGroups/*}/indexes  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. A parent name of the form `  projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}  `

### Request body

The request body contains an instance of `  Index  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
