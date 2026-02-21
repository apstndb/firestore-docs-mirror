Creates the specified index. A newly created index's initial state is `  CREATING  ` . On completion of the returned `  google.longrunning.Operation  ` , the state will be `  READY  ` . If the index already exists, the call will return an `  ALREADY_EXISTS  ` status.

During creation, the process could result in an error, in which case the index will move to the `  ERROR  ` state. The process can be recovered by fixing the data that caused the error, removing the index with `  delete  ` , then re-creating the index with `  create  ` .

Indexes with a single field cannot be created.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{parent=projects/*/databases/*}/indexes  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

The name of the database this index will apply to. For example: `  projects/{projectId}/databases/{databaseId}  `

### Request body

The request body contains an instance of `  Index  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
