---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/list
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/list
title: 'Method: projects.databases.userCreds.list'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

List all user creds in the database. Note that the returned resource does not contain the secret value itself.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1/{parent=projects/*/databases/*}/userCreds`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                     |
|------------|-----------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. A parent database name of the form `projects/{projectId}/databases/{databaseId}` |

### Request body

The request body must be empty.

### Response body

The response for [`FirestoreAdmin.ListUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/list#google.firestore.admin.v1.FirestoreAdmin.ListUserCreds) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "userCreds": [
    {
      object (UserCreds)
    }
  ]
}
```

| Fields        |                                                                                                                                                                      |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `userCreds[]` | `object ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds#UserCreds)` )` The user creds for the database. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
