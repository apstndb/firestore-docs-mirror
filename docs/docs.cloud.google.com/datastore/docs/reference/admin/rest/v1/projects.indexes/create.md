  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#body.request_body)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create#try-it)

Creates the specified index. A newly created index's initial state is `  CREATING  ` . On completion of the returned `  google.longrunning.Operation  ` , the state will be `  READY  ` . If the index already exists, the call will return an `  ALREADY_EXISTS  ` status.

During index creation, the process could result in an error, in which case the index will move to the `  ERROR  ` state. The process can be recovered by fixing the data that caused the error, removing the index with `  delete  ` , then re-creating the index with `  create  ` .

Indexes with a single property cannot be created.

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

  
`  POST https://datastore.googleapis.com/v1/projects/{projectId}/indexes  `

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Project ID against which to make the request.

### Request body

The request body contains an instance of `  Index  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
