# Using the Firestore REST API

While the easiest way to use Firestore is to use one of the native client libraries, there are some situations when it is useful to call the REST API directly.

The REST API can be helpful for the following use cases:

  - Accessing Firestore from a resource-constrained environment, such as an internet of things (IoT) device, where running a complete client library is not possible.
  - Automating database administration or retrieving detailed database metadata.

If you are using a [gRPC-supported language](https://grpc.io/about/#osp) , consider using the [RPC API](./reference/rpc/) rather than the REST API.

## Authentication and authorization

For authentication, the Firestore REST API accepts either a [Firebase Authentication](https://firebase.google.com/docs/auth/) ID token or a [Google Identity OAuth 2.0](https://developers.google.com/identity/protocols/OAuth2) token. The token you provide affects your request's authorization:

  - Use Firebase ID tokens to authenticate requests from your application's users. For these requests, Firestore uses [Firestore Security Rules](./security/get-started) to determine if a request is authorized.

  - Use a Google Identity OAuth 2.0 token and a [service account](https://cloud.google.com/iam/docs/service-accounts) to authenticate requests from your application, such as requests for database administration. For these requests, Firestore uses [Identity and Access Management (IAM)](https://cloud.google.com/iam/docs/overview) to determine if a request is authorized.

### Working with Firebase ID tokens

You can attain a Firebase ID token in two ways:

  - [Generate a Firebase ID token using the Firebase Authentication REST API](https://firebase.google.com/docs/reference/rest/auth/) .
  - [Retrieve a user's Firebase ID token from a Firebase Authentication SDK](https://firebase.google.com/docs/auth/admin/verify-id-tokens#retrieve_id_tokens_on_clients) .

By retrieving a user's Firebase ID token, you can make requests on behalf of the user.

For requests authenticated with a Firebase ID token and for unauthenticated requests, Firestore uses your [Firestore Security Rules](./security/get-started) to determine if a request is authorized.

### Working with Google Identity OAuth 2.0 tokens

You can generate an access token by using a [service account](https://cloud.google.com/iam/docs/service-accounts) with a [Google API Client Library](https://developers.google.com/api-client-library/) or by following the steps in [Using OAuth 2.0 for Server to Server Applications](https://developers.google.com/identity/protocols/OAuth2ServiceAccount) . You can also generate a token with the [`  gcloud  `](https://cloud.google.com/sdk/gcloud/) command-line tool and the command [`  gcloud auth application-default print-access-token  `](https://cloud.google.com/sdk/gcloud/reference/auth/application-default/print-access-token) .

This token must have the following scope to send requests to the Firestore REST API:

  - `  https://www.googleapis.com/auth/datastore  `

If you authenticate your requests with a service account and a Google Identity OAuth 2.0 token, Firestore assumes that your requests act on behalf of your application instead of an individual user. Firestore allows these requests to ignore your security rules. Instead, Firestore uses [IAM](https://cloud.google.com/iam/docs/overview) to determine if a request is authorized.

You can control the access permissions of service accounts by assigning [Firestore IAM roles](https://cloud.google.com/firestore/docs/security/iam#roles) .

### Authenticating with an access token

After you obtain either a Firebase ID token or a Google Identity OAuth 2.0 token, pass it to the Firestore endpoints as an `  Authorization  ` header set to `  Bearer {YOUR_TOKEN}  ` .

## Making REST calls

All REST API endpoints exist under the base URL `  https://firestore.googleapis.com/v1/  ` .

To create a path to a document with the ID `  LA  ` in the collection `  cities  ` under the project `  YOUR_PROJECT_ID  ` you would use the following structure.

``` text
/projects/YOUR_PROJECT_ID/databases/(default)/documents/cities/LA
```

To interact with this path, combine it with the base API URL.

``` text
https://firestore.googleapis.com/v1/projects/YOUR_PROJECT_ID/databases/(default)/documents/cities/LA
```

The best way to begin experimenting with the REST API is to use the [API Explorer](https://developers.google.com/apis-explorer/#search/firestore/firestore/v1/) , which automatically generates Google Identity OAuth 2.0 tokens and allows you to examine the API.

## Methods

Below are brief descriptions of the two most important method groups. For a complete list, see the [REST API reference](./reference/rest/) or use the [API Explorer](https://developers.google.com/apis-explorer/#search/firestore/firestore/v1/) .

#### `     v1.projects.databases.documents    `

Perform CRUD operations on documents, similar to those outlined in the [add data](./manage-data/add-data) or [get data](./query-data/get-data) guides.

#### `     v1.projects.databases.collectionGroups.indexes    `

Perform actions on indexes such as creating new indexes, disabling an existing index, or listing all current indexes. Useful for automating data structure migrations or synchronizing indexes between projects.

Also enables retrieval of document metadata, such as the list of all fields and subcollections for a given document.

## Error Codes

When a Firestore request succeeds, the Firestore API returns an HTTP `  200 OK  ` status code and the requested data. When a request fails, the Firestore API returns an HTTP `  4xx  ` or `  5xx  ` status code and a response with information about the error.

The following table lists recommended actions for each error code. These codes apply to the Firestore REST and RPC APIs. The [Firestore SDKs and client libraries](/firestore/docs/reference/libraries) may not return these same error codes.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Canonical Error Code</th>
<th>Description</th>
<th>Recommended Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ABORTED      </code></td>
<td>The request conflicted with another request.</td>
<td>For a non-transactional commit:<br />
Retry the request or re-structure your data model to reduce contention.<br />
<br />
For requests in a transaction:<br />
Retry the entire transaction or re-structure your data model to reduce contention.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ALREADY_EXISTS      </code></td>
<td>The request tried to create a document that already exists.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DEADLINE_EXCEEDED      </code></td>
<td>The Firestore server handling the request exceeded a deadline.</td>
<td>Retry using exponential backoff.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FAILED_PRECONDITION      </code></td>
<td>The request did not meet one of its preconditions. For example, a query request might require an index not yet defined. See the message field in the error response for the precondition that failed.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTERNAL      </code></td>
<td>The Firestore server returned an error.</td>
<td>Do not retry this request more than once.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INVALID_ARGUMENT      </code></td>
<td>A request parameter includes an invalid value. See the message field in the error response for the invalid value.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NOT_FOUND      </code></td>
<td>The request attempted to update a document that does not exist.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PERMISSION_DENIED      </code></td>
<td>The user is not authorized to make this request.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RESOURCE_EXHAUSTED      </code></td>
<td>The project exceeded either its <a href="/firestore/quotas">quota</a> or the region/multi-region capacity.</td>
<td><a href="./monitor-usage#view-quota">Verify that you did not exceed your project quota</a> . If you exceeded a project quota, do not retry without fixing the problem.<br />
<br />
Otherwise, retry with exponential backoff.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UNAUTHENTICATED      </code></td>
<td>The request did not include valid authentication credentials.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UNAVAILABLE      </code></td>
<td>The Firestore server returned an error.</td>
<td>Retry using exponential backoff.</td>
</tr>
</tbody>
</table>
