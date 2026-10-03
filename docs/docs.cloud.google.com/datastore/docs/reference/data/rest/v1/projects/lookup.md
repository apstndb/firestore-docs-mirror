---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup
title: 'Method: projects.lookup'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [HTTP request](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.HTTP_TEMPLATE)
- [Path parameters](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.PATH_PARAMETERS)
- [Request body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.request_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.request_body.SCHEMA_REPRESENTATION)
- [Response body](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.response_body)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.LookupResponse.SCHEMA_REPRESENTATION)
- [Authorization scopes](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.aspect)
- [Try it!](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#try-it)

Looks up entities by key.

### HTTP request

Choose a location:

  
`POST https://datastore.googleapis.com/v1/projects/{projectId}:lookup`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

| Parameters  |                                                                             |
|-------------|-----------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project against which to make the request. |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "databaseId": string,
  "readOptions": {
    object (ReadOptions)
  },
  "keys": [
    {
      object (Key)
    }
  ],
  "propertyMask": {
    object (PropertyMask)
  }
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                             |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `databaseId`   | `string` The ID of the database against which to make the request. '(default)' is not allowed; please use empty string '' to refer the default database.                                                                                                                                                                                                                    |
| `readOptions`  | `object ( `[`ReadOptions`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ReadOptions)` )` The options for this lookup request.                                                                                                                                                                                                                        |
| `keys[]`       | `object ( `[`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key)` )` Required. Keys of entities to look up.                                                                                                                                                                                                                      |
| `propertyMask` | `object ( `[`PropertyMask`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyMask)` )` The properties to return. Defaults to returning all properties. If this field is set and an entity has a property not referenced in the mask, it will be absent from \[LookupResponse.found.entity.properties\]\[\]. The entity's key is always returned. |

### Response body

The response for [`Datastore.Lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#google.datastore.v1.Datastore.Lookup) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "found": [
    {
      object (EntityResult)
    }
  ],
  "missing": [
    {
      object (EntityResult)
    }
  ],
  "deferred": [
    {
      object (Key)
    }
  ],
  "transaction": string,
  "readTime": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `found[]`     | `object ( `[`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult)` )` Entities found as `ResultType.FULL` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.                                                                                                                                                                                                                                                               |
| `missing[]`   | `object ( `[`EntityResult`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/EntityResult)` )` Entities not found as `ResultType.KEY_ONLY` entities. The order of results in this field is undefined and has no relation to the order of the keys in the input.                                                                                                                                                                                                                                                       |
| `deferred[]`  | `object ( `[`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key)` )` A list of keys that were not looked up due to resource constraints. The order of results in this field is undefined and has no relation to the order of the keys in the input.                                                                                                                                                                                                                                           |
| `transaction` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The identifier of the transaction that was started as part of this projects.lookup request. Set only when [`ReadOptions.new_transaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/ReadOptions#FIELDS.new_transaction) was set in [`LookupRequest.read_options`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup#body.request_body.FIELDS.read_options) . A base64-encoded string. |
| `readTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time at which these entities were read or found missing. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                       |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
