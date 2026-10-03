---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes
title: 'REST Resource: projects.indexes'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [Resource: Index](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#Index)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#Index.SCHEMA_REPRESENTATION)
- [AncestorMode](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#AncestorMode)
- [IndexedProperty](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#IndexedProperty)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#IndexedProperty.SCHEMA_REPRESENTATION)
- [Direction](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#Direction)
- [State](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#State)
- [Methods](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#METHODS_SUMMARY)

## Resource: Index

Datastore composite index definition.

**JSON representation**

```
{
  "projectId": string,
  "indexId": string,
  "kind": string,
  "ancestor": enum (AncestorMode),
  "properties": [
    {
      object (IndexedProperty)
    }
  ],
  "state": enum (State)
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
<td><code>projectId</code></td>
<td><p><code>string</code></p>
<p>Output only. Project ID.</p></td>
</tr>
<tr class="even">
<td><code>indexId</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource ID of the index.</p></td>
</tr>
<tr class="odd">
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>Required. The entity kind to which this index applies.</p></td>
</tr>
<tr class="even">
<td><code>ancestor</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#AncestorMode"><code>AncestorMode</code></a><code> )</code></p>
<p>Required. The index's ancestor mode. Must not be ANCESTOR_MODE_UNSPECIFIED.</p></td>
</tr>
<tr class="odd">
<td><code>properties[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#IndexedProperty"><code>IndexedProperty</code></a><code> )</code></p>
<p>Required. An ordered sequence of property names and their index attributes.</p>
<p>Requires:</p>
<ul>
<li>A maximum of 100 properties.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#State"><code>State</code></a><code> )</code></p>
<p>Output only. The state of the index.</p></td>
</tr>
</tbody>
</table>

## AncestorMode

For an ordered index, specifies whether each of the entity's ancestors will be included.

| Enums                       |                                                     |
|-----------------------------|-----------------------------------------------------|
| `ANCESTOR_MODE_UNSPECIFIED` | The ancestor mode is unspecified.                   |
| `NONE`                      | Do not include the entity's ancestors in the index. |
| `ALL_ANCESTORS`             | Include all the entity's ancestors in the index.    |

## IndexedProperty

A property of an index.

**JSON representation**

```
{
  "name": string,
  "direction": enum (Direction)
}
```

| Fields      |                                                                                                                                                                                                            |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`      | `string` Required. The property name to index.                                                                                                                                                             |
| `direction` | `enum ( `[`Direction`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes#Direction)` )` Required. The indexed property's direction. Must not be DIRECTION_UNSPECIFIED. |

## Direction

The direction determines how a property is indexed.

| Enums                   |                                                                                                                              |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------|
| `DIRECTION_UNSPECIFIED` | The direction is unspecified.                                                                                                |
| `ASCENDING`             | The property's values are indexed so as to support sequencing in ascending order and also query by \<, \>, \<=, \>=, and =.  |
| `DESCENDING`            | The property's values are indexed so as to support sequencing in descending order and also query by \<, \>, \<=, \>=, and =. |

## State

The possible set of states of an index.

| Enums               |                                                                                                                                                                                                                                                                                                           |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                                                                                                                                                                                                                                 |
| `CREATING`          | The index is being created, and cannot be used by queries. There is an active long-running operation for the index. The index is updated when writing an entity. Some index data may exist.                                                                                                               |
| `READY`             | The index is ready to be used. The index is updated when writing an entity. The index is fully populated from all stored entities it applies to.                                                                                                                                                          |
| `DELETING`          | The index is being deleted, and cannot be used by queries. There is an active long-running operation for the index. The index is not updated when writing an entity. Some index data may exist.                                                                                                           |
| `ERROR`             | The index was being created or deleted, but something went wrong. The index cannot by used by queries. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing an entity. Some index data may exist. |

| Methods                                                                                                  |                                                     |
|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| [`create`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/create) | Creates the specified index.                        |
| [`delete`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/delete) | Deletes an existing index.                          |
| [`get`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/get)       | Gets an index.                                      |
| [`list`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/v1/projects.indexes/list)     | Lists the indexes that match the specified filters. |
