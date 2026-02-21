When a Firestore in Datastore mode request is successful, the API will return an HTTP `  200 OK  ` status code along with the requested data in the body of the response.

**Note:** The errors and status codes described in this page are returned by the low-level Datastore API. Note that client libraries may or may not return these same values.

When a request fails, the Datastore API will return an HTTP `  4xx  ` or `  5xx  ` status code that generically identifies the failure as well as a response that provides more specific information about the error(s) that caused the failure.

The rest of this page describes the structure of an error, enumerates specific error codes, and recommends how to handle them.

The following is the structure of an error response for a JSON request:

``` text
{
  "error": {
    "code": "integer",
    "message": "string",
    "status": "string"
  }
}
```

The response object contains a single field `  error  ` whose value contains the following elements:

<table>
<thead>
<tr class="header">
<th>Element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       code      </code></td>
<td>An <a href="https://tools.ietf.org/html/rfc7231#section-6">HTTP status code</a> that generically identifies the request failure.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       message      </code></td>
<td>Specific information about the request failure.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       status      </code></td>
<td>The <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">canonical error code</a> ( <code dir="ltr" translate="no">       google.rpc.Code      </code> ) for Google APIs. Codes that may be returned by the Datastore API are listed in <a href="#error_codes">Error Codes</a> .</td>
</tr>
</tbody>
</table>

Here's an example of an error response for a JSON request:

``` text
{
  "error": {
    "code": 400,
    "message": "Key path is incomplete: [Person: null]",
    "status": "INVALID_ARGUMENT"
  }
}
```

If a request made with a content type of `  application/x-protobuf  ` results in an error, it will return a serialized [`  google.rpc.Status  `](https://github.com/googleapis/googleapis/blob/master/google/rpc/status.proto) message as the payload.

**Note:** The text provided in the message could change at any time so applications should not depend on the actual text.

## Error Codes

The recommended way to classify errors is inspect the value of the [canonical error code](https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto) ( `  google.rpc.Code  ` ). In JSON errors, this code appears in the `  status  ` field. In `  application/x-protobuf  ` errors, it's in the `  code  ` field.

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
<td>Indicates that the request conflicted with another request.</td>
<td>For a non-transactional commit:<br />
Retry the request or structure your entities to reduce contention.<br />
<br />
For requests that are part of a <a href="/datastore/docs/concepts/transactions">transactional</a> commit:<br />
Retry the entire transaction or structure your entities to reduce contention.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ALREADY_EXISTS      </code></td>
<td>Indicates that the request attempted to insert an entity that already exists.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DEADLINE_EXCEEDED      </code></td>
<td>A deadline was exceeded on the server.</td>
<td>Retry using exponential backoff.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FAILED_PRECONDITION      </code></td>
<td>Indicates that a precondition for the request was not met. The message field in the error response provides information about the precondition that failed. One possible cause is running a query that requires an index not yet defined.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTERNAL      </code></td>
<td>Server returned an error.</td>
<td>Do not retry this request more than once.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INVALID_ARGUMENT      </code></td>
<td>Indicates that a request parameter has an invalid value. The message field in the error response provides information as to which value was invalid.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       NOT_FOUND      </code></td>
<td>Indicates that the request attempted to update an entity that does not exist.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       PERMISSION_DENIED      </code></td>
<td>Indicates that the user was not authorized to make the request.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       RESOURCE_EXHAUSTED      </code></td>
<td>Indicates that the project exceeded either its <a href="/datastore/docs/pricing">quota</a> or the region/multi-region capacity.</td>
<td><a href="/datastore/docs/pricing#locating_quota_usage_information_for_your_app">Verify that you did not exceed your project quota</a> . If you exceeded a project quota, do not retry without fixing the problem.<br />
<br />
Otherwise, retry with exponential backoff.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UNAUTHENTICATED      </code></td>
<td>Indicates that the request did not have valid authentication credentials.</td>
<td>Do not retry without fixing the problem.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UNAVAILABLE      </code></td>
<td>Server returned an error.</td>
<td>Retry using exponential backoff.</td>
</tr>
</tbody>
</table>
