Create a user creds.

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

  
`POST https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/userCreds`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`parent`

`string`

Required. A parent name of the form `projects/{projectId}/databases/{databaseId}`

### Query parameters

Parameters

`userCredsId`

`string`

Required. The ID to use for the user creds, which will become the final component of the user creds's resource name.

This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/.

### Request body

The request body contains an instance of `  UserCreds  ` .

### Response body

If successful, the response body contains a newly created instance of `  UserCreds  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
