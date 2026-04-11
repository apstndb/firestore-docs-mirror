Updates or inserts a document.

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

  
`PATCH https://firestore.googleapis.com/v1/{document.name=projects/*/databases/*/documents/*/**}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`document.name`

`string`

The resource name of the document, for example `projects/{projectId}/databases/{databaseId}/documents/{document_path}` .

### Query parameters

Parameters

`updateMask`

` object ( DocumentMask  ` )

The fields to update. None of the field paths in the mask may contain a reserved name.

If the document exists on the server and has fields not referenced in the mask, they are left unchanged. Fields referenced in the mask, but not present in the input document, are deleted from the document on the server.

`mask`

` object ( DocumentMask  ` )

The fields to return. If not set, returns all fields.

If the document has a field that is not present in this mask, that field will not be returned in the response.

`currentDocument`

` object ( Precondition  ` )

An optional precondition on the document. The request will fail if this is set and not met by the target document.

### Request body

The request body contains an instance of `  Document  ` .

### Response body

If successful, the response body contains an instance of `  Document  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
