Creates a new document.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{parent=projects/*/databases/*/documents/**}/{collectionId}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The parent resource. For example: `  projects/{projectId}/databases/{databaseId}/documents  ` or `  projects/{projectId}/databases/{databaseId}/documents/chatrooms/{chatroom_id}  `

`  collectionId  `

`  string  `

Required. The collection ID, relative to `  parent  ` , to list. For example: `  chatrooms  ` .

### Query parameters

Parameters

`  documentId  `

`  string  `

The client-assigned document ID to use for this document.

Optional. If not specified, an ID will be assigned by the service.

`  mask  `

`  object ( DocumentMask  ` )

The fields to return. If not set, returns all fields.

If the document has a field that is not present in this mask, that field will not be returned in the response.

### Request body

The request body contains an instance of `  Document  ` .

### Response body

If successful, the response body contains an instance of `  Document  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
