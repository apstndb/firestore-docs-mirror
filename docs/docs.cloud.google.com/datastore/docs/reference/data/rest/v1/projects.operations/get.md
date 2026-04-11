  - [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects.operations/get#try-it)

Gets the latest state of a long-running operation. Clients can use this method to poll the operation result at intervals as recommended by the API service.

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

  
`GET https://datastore.googleapis.com/v1/{name=projects/*/operations/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

The name of the operation resource.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
