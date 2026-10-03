---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes
title: 'REST Resource: projects.databases.indexes'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Resource: Index

An index definition.

**JSON representation**

```
{
  "name": string,
  "collectionId": string,
  "fields": [
    {
      object (IndexField)
    }
  ],
  "state": enum (State)
}
```

| Fields         |                                                                                                                                                                   |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` The resource name of the index. Output only.                                                                                                             |
| `collectionId` | `string` The collection ID to which this index applies. Required.                                                                                                 |
| `fields[]`     | `object ( `[`IndexField`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes#IndexField)` )` The fields to index.     |
| `state`        | `enum ( `[`State`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes#State)` )` The state of the index. Output only. |

## IndexField

A field of an index.

**JSON representation**

```
{
  "fieldPath": string,
  "mode": enum (Mode)
}
```

| Fields      |                                                                                                                                                                                                                                                                           |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fieldPath` | `string` The path of the field. Must match the field path specification described by \[google.firestore.v1beta1.Document.fields\]\[fields\]. Special field path `__name__` may be used by itself or at the end of a path. `__type__` may be used only at the end of path. |
| `mode`      | `enum ( `[`Mode`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes#Mode)` )` The field's mode.                                                                                                                              |

## Mode

The mode determines how a field is indexed.

| Enums              |                                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------|
| `MODE_UNSPECIFIED` | The mode is unspecified.                                                                                                  |
| `ASCENDING`        | The field's values are indexed so as to support sequencing in ascending order and also query by \<, \>, \<=, \>=, and =.  |
| `DESCENDING`       | The field's values are indexed so as to support sequencing in descending order and also query by \<, \>, \<=, \>=, and =. |
| `ARRAY_CONTAINS`   | The field's array values are indexed so as to support membership using ARRAY_CONTAINS queries.                            |

## State

The state of an index. During index creation, an index will be in the `CREATING` state. If the index is created successfully, it will transition to the `READY` state. If the index is not able to be created, it will transition to the `ERROR` state.

| Enums               |                                                                                                                                                                                                                                                            |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                                                                                                                                                                                  |
| `CREATING`          | The index is being created. There is an active long-running operation for the index. The index is updated when writing a document. Some index data may exist.                                                                                              |
| `READY`             | The index is ready to be used. The index is updated when writing a document. The index is fully populated from all stored documents it applies to.                                                                                                         |
| `ERROR`             | The index was being created, but something went wrong. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing a document. Some index data may exist. |

| Methods                                                                                                           |                                                     |
|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/create) | Creates the specified index.                        |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/delete) | Deletes an index.                                   |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/get)       | Gets an index.                                      |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/list)     | Lists the indexes that match the specified filters. |
