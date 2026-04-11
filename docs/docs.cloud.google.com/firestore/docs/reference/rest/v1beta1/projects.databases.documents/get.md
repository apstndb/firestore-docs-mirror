Gets a single document.

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

  
`GET https://firestore.googleapis.com/v1beta1/{name=projects/*/databases/*/documents/*/**}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. The resource name of the Document to get. In the format: `projects/{projectId}/databases/{databaseId}/documents/{document_path}` .

### Query parameters

Parameters

`mask`

` object ( DocumentMask  ` )

The fields to return. If not set, returns all fields.

If the document has a field that is not present in this mask, that field will not be returned in the response.

Union parameter `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following:

`transaction`

`string ( bytes format)`

Reads the document in a transaction.

A base64-encoded string.

`readTime`

` string ( Timestamp  ` format)

Reads the version of the document at the given time.

This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Document  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/datastore`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
