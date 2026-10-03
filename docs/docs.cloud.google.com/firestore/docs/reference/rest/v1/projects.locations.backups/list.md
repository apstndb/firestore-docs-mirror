---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/list
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/list
title: 'Method: projects.locations.backups.list'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Lists all the backups.

### HTTP request

Choose a location:

  
`GET https://firestore.googleapis.com/v1/{parent=projects/*/locations/*}/backups`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters |                                                                                                                                                                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The location to list backups from. Format is `projects/{project}/locations/{location}` . Use `{location} = '-'` to list backups from all locations for the given project. This allows listing backups from a single location or from all locations. |

### Query parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>An expression that filters the list of returned backups.</p>
<p>A filter expression consists of a field name, a comparison operator, and a value for filtering. The value must be a string, a number, or a boolean. The comparison operator must be one of: <code>&lt;</code> , <code>&gt;</code> , <code>&lt;=</code> , <code>&gt;=</code> , <code>!=</code> , <code>=</code> , or <code>:</code> . Colon <code>:</code> is the contains operator. Filter rules are not case sensitive.</p>
<p>The following fields in the <a href="https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups#Backup"><code>Backup</code></a> are eligible for filtering:</p>
<ul>
<li><code>databaseUid</code> (supports <code>=</code> only)</li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body must be empty.

### Response body

The response for [`FirestoreAdmin.ListBackups`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/list#google.firestore.admin.v1.FirestoreAdmin.ListBackups) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "backups": [
    {
      object (Backup)
    }
  ],
  "unreachable": [
    string
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                            |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backups[]`     | `object ( `[`Backup`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups#Backup)` )` List of all backups for the project.                                                                                                                                                                           |
| `unreachable[]` | `string` List of locations that existing backups were not able to be fetched from. Instead of failing the entire requests when a single location is unreachable, this response returns a partial result set and list of locations unable to be reached here. The request can be retried against a single location to get a concrete error. |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
