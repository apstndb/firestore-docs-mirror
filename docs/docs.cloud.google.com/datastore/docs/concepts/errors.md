---
name: documents/docs.cloud.google.com/datastore/docs/concepts/errors
uri: https://docs.cloud.google.com/datastore/docs/concepts/errors
title: Errors and Error Handling
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

When a Firestore in Datastore mode request is successful, the API will return an HTTP `200 OK` status code along with the requested data in the body of the response.

> **Note:** The errors and status codes described in this page are returned by the low-level Datastore API. Note that client libraries may or may not return these same values.

When a request fails, the Datastore API will return an HTTP `4xx` or `5xx` status code that generically identifies the failure as well as a response that provides more specific information about the error(s) that caused the failure.

The rest of this page describes the structure of an error, enumerates specific error codes, and recommends how to handle them.

The following is the structure of an error response for a JSON request:

```
{
  "error": {
    "code": "integer",
    "message": "string",
    "status": "string"
  }
}
```

The response object contains a single field `error` whose value contains the following elements:

| Element   | Description                                                                                                                                                                                                                                                                                           |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`    | An [HTTP status code](https://tools.ietf.org/html/rfc7231#section-6) that generically identifies the request failure.                                                                                                                                                                                 |
| `message` | Specific information about the request failure.                                                                                                                                                                                                                                                       |
| `status`  | The [canonical error code](https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto) ( `google.rpc.Code` ) for Google APIs. Codes that may be returned by the Datastore API are listed in [Error Codes](https://docs.cloud.google.com/datastore/docs/concepts/errors#error_codes) . |

Here's an example of an error response for a JSON request:

```
{
  "error": {
    "code": 400,
    "message": "Key path is incomplete: [Person: null]",
    "status": "INVALID_ARGUMENT"
  }
}
```

If a request made with a content type of `application/x-protobuf` results in an error, it will return a serialized [`google.rpc.Status`](https://github.com/googleapis/googleapis/blob/master/google/rpc/status.proto) message as the payload.

> **Note:** The text provided in the message could change at any time so applications should not depend on the actual text.

## Error Codes

The recommended way to classify errors is inspect the value of the [canonical error code](https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto) ( `google.rpc.Code` ). In JSON errors, this code appears in the `status` field. In `application/x-protobuf` errors, it's in the `code` field.

| Canonical Error Code  | Description                                                                                                                                                                                                                               | Recommended Action                                                                                                                                                                                                                                                                                           |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ABORTED`             | Indicates that the request conflicted with another request.                                                                                                                                                                               | For a non-transactional commit: Retry the request or structure your entities to reduce contention. For requests that are part of a [transactional](https://docs.cloud.google.com/datastore/docs/concepts/transactions) commit: Retry the entire transaction or structure your entities to reduce contention. |
| `ALREADY_EXISTS`      | Indicates that the request attempted to insert an entity that already exists.                                                                                                                                                             | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `DEADLINE_EXCEEDED`   | A deadline was exceeded on the server.                                                                                                                                                                                                    | Retry using exponential backoff.                                                                                                                                                                                                                                                                             |
| `FAILED_PRECONDITION` | Indicates that a precondition for the request was not met. The message field in the error response provides information about the precondition that failed. One possible cause is running a query that requires an index not yet defined. | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `INTERNAL`            | Server returned an error.                                                                                                                                                                                                                 | Do not retry this request more than once.                                                                                                                                                                                                                                                                    |
| `INVALID_ARGUMENT`    | Indicates that a request parameter has an invalid value. The message field in the error response provides information as to which value was invalid.                                                                                      | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `NOT_FOUND`           | Indicates that the request attempted to update an entity that does not exist.                                                                                                                                                             | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `PERMISSION_DENIED`   | Indicates that the user was not authorized to make the request.                                                                                                                                                                           | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `RESOURCE_EXHAUSTED`  | Indicates that the project exceeded either its [quota](https://docs.cloud.google.com/datastore/docs/pricing) or the region/multi-region capacity.                                                                                         | [Verify that you did not exceed your project quota](https://docs.cloud.google.com/datastore/docs/pricing#locating_quota_usage_information_for_your_app) . If you exceeded a project quota, do not retry without fixing the problem. Otherwise, retry with exponential backoff.                               |
| `UNAUTHENTICATED`     | Indicates that the request did not have valid authentication credentials.                                                                                                                                                                 | Do not retry without fixing the problem.                                                                                                                                                                                                                                                                     |
| `UNAVAILABLE`         | Server returned an error.                                                                                                                                                                                                                 | Retry using exponential backoff.                                                                                                                                                                                                                                                                             |
