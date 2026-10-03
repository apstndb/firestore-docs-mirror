---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value
title: Value
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#SCHEMA_REPRESENTATION)
- [Key](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key.SCHEMA_REPRESENTATION)
- [PartitionId](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PartitionId)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PartitionId.SCHEMA_REPRESENTATION)
- [PathElement](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PathElement)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PathElement.SCHEMA_REPRESENTATION)
- [Entity](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Entity)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Entity.SCHEMA_REPRESENTATION)

A message that can hold any of the supported value types and associated metadata.

**JSON representation**

```
{
  "meaning": integer,
  "excludeFromIndexes": boolean,

  // Union field value_type can be only one of the following:
  "nullValue": null,
  "booleanValue": boolean,
  "integerValue": string,
  "doubleValue": number,
  "timestampValue": string,
  "keyValue": {
    object (Key)
  },
  "stringValue": string,
  "blobValue": string,
  "geoPointValue": {
    object (LatLng)
  },
  "entityValue": {
    object (Entity)
  },
  "arrayValue": {
    object (ArrayValue)
  }
  // End of list of possible types for union field value_type.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>meaning</code></td>
<td><p><code>integer</code></p>
<p>The <code>meaning</code> field should only be populated for backwards compatibility.</p></td>
</tr>
<tr class="even">
<td><code>excludeFromIndexes</code></td>
<td><p><code>boolean</code></p>
<p>If the value should be excluded from all indexes including those defined explicitly.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>value_type</code> . Must have a value set. <code>value_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>nullValue</code></td>
<td><p><code>null</code></p>
<p>A null value.</p></td>
</tr>
<tr class="odd">
<td><code>booleanValue</code></td>
<td><p><code>boolean</code></p>
<p>A boolean value.</p></td>
</tr>
<tr class="even">
<td><code>integerValue</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>An integer value.</p></td>
</tr>
<tr class="odd">
<td><code>doubleValue</code></td>
<td><p><code>number</code></p>
<p>A double value.</p></td>
</tr>
<tr class="even">
<td><code>timestampValue</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>A timestamp value. When stored in the Datastore, precise only to microseconds; any additional precision is rounded down.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>keyValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key"><code>Key</code></a><code> )</code></p>
<p>A key value.</p></td>
</tr>
<tr class="even">
<td><code>stringValue</code></td>
<td><p><code>string</code></p>
<p>A UTF-8 encoded string value. When <code>excludeFromIndexes</code> is false (it is indexed) , may have at most 1500 bytes. Otherwise, may be set to at most 1,000,000 bytes.</p></td>
</tr>
<tr class="odd">
<td><code>blobValue</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p>A blob value. May have at most 1,000,000 bytes. When <code>excludeFromIndexes</code> is false, may have at most 1500 bytes. In JSON requests, must be base64-encoded.</p>
<p>A base64-encoded string.</p></td>
</tr>
<tr class="even">
<td><code>geoPointValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/LatLng"><code>LatLng</code></a><code> )</code></p>
<p>A geo point value representing a point on the surface of Earth.</p></td>
</tr>
<tr class="odd">
<td><code>entityValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Entity"><code>Entity</code></a><code> )</code></p>
<p>An entity value.</p>
<ul>
<li>May have no key.</li>
<li>May have a key with an incomplete key path.</li>
<li>May have a reserved/read-only key.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>arrayValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/ArrayValue"><code>ArrayValue</code></a><code> )</code></p>
<p>An array value. Cannot contain another array value. A <code>Value</code> instance that sets field <code>arrayValue</code> must not set fields <code>meaning</code> or <code>excludeFromIndexes</code> .</p></td>
</tr>
</tbody>
</table>

## Key

A unique identifier for an entity. If a key's partition ID or any of its path kinds or names are reserved/read-only, the key is reserved/read-only. A reserved/read-only key is forbidden in certain documented contexts.

**JSON representation**

```
{
  "partitionId": {
    object (PartitionId)
  },
  "path": [
    {
      object (PathElement)
    }
  ]
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `partitionId` | `object ( `[`PartitionId`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PartitionId)` )` Entities are partitioned into subsets, currently identified by a project ID and namespace ID. Queries are scoped to a single partition.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `path[]`      | `object ( `[`PathElement`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#PathElement)` )` The entity path. An entity path consists of one or more elements composed of a kind and a string or numerical identifier, which identify entities. The first element identifies a *root entity* , the second element identifies a *child* of the root entity, the third element identifies a child of the second entity, and so forth. The entities identified by all prefixes of the path are called the element's *ancestors* . An entity path is always fully complete: *all* of the entity's ancestors are required to be in the path along with the entity identifier itself. The only exception is that in some documented cases, the identifier in the last path element (for the entity) itself may be omitted. For example, the last path element of the key of `Mutation.insert` may have no identifier. A path can never be empty, and a path can have at most 100 elements. |

## PartitionId

A partition ID identifies a grouping of entities. The grouping is always by project and namespace, however the namespace ID may be empty.

A partition ID contains several dimensions: project ID and namespace ID.

Partition dimensions:

- May be `""` .
- Must be valid UTF-8 bytes.
- Must have values that match regex `[A-Za-z\d\.\-_]{1,100}` If the value of any dimension matches regex `__.*__` , the partition is reserved/read-only. A reserved/read-only partition ID is forbidden in certain documented contexts.

Foreign partition IDs (in which the project ID does not match the context project ID ) are discouraged. Reads and writes of foreign partition IDs may fail if the project is not in an active state.

**JSON representation**

```
{
  "projectId": string,
  "databaseId": string,
  "namespaceId": string
}
```

| Fields        |                                                                              |
|---------------|------------------------------------------------------------------------------|
| `projectId`   | `string` The ID of the project to which the entities belong.                 |
| `databaseId`  | `string` If not empty, the ID of the database to which the entities belong.  |
| `namespaceId` | `string` If not empty, the ID of the namespace to which the entities belong. |

## PathElement

A (kind, ID/name) pair used to construct a key path.

If either name or ID is set, the element is complete. If neither is set, the element is incomplete.

**JSON representation**

```
{
  "kind": string,

  // Union field id_type can be only one of the following:
  "id": string,
  "name": string
  // End of list of possible types for union field id_type.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kind`                                                                              | `string` The kind of the entity. A kind matching regex `__.*__` is reserved/read-only. A kind must not contain more than 1500 bytes when UTF-8 encoded. Cannot be `""` . Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `__bytes<X>__` where `<X>` is the base-64 encoding of the bytes. |
| Union field `id_type` . The type of ID. `id_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                            |
| `id`                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The auto-allocated ID of the entity. Never equal to zero. Values less than zero are discouraged and may not be supported in the future.                                                                                             |
| `name`                                                                              | `string` The name of the entity. A name matching regex `__.*__` is reserved/read-only. A name must not be more than 1500 bytes when UTF-8 encoded. Cannot be `""` . Must be valid UTF-8 bytes. Legacy values that are not valid UTF-8 are encoded as `__bytes<X>__` where `<X>` is the base-64 encoding of the bytes.      |

## Entity

A Datastore data object.

Must not exceed 1 MiB - 4 bytes.

**JSON representation**

```
{
  "key": {
    object (Key)
  },
  "properties": {
    string: {
      object (Value)
    },
    ...
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`        | `object ( `[`Key`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#Key)` )` The entity's key. An entity must have a key, unless otherwise documented (for example, an entity in `Value.entity_value` may have no key). An entity's kind is its key path's last element's kind, or null if it has no key.                                                                                                                                                                                              |
| `properties` | `map (key: string, value: object ( `[`Value`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value)` ))` The entity's properties. The map's keys are property names. A property name matching regex `__.*__` is reserved. A reserved property name is forbidden in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
