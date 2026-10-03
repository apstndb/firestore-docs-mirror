---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/FieldOperationMetadata
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/FieldOperationMetadata
title: FieldOperationMetadata
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation) results from [`FirestoreAdmin.UpdateField`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/patch#google.firestore.admin.v1.FirestoreAdmin.UpdateField) .

**JSON representation**

```
{
  "startTime": string,
  "endTime": string,
  "field": string,
  "indexConfigDeltas": [
    {
      object (IndexConfigDelta)
    }
  ],
  "state": enum (OperationState),
  "progressDocuments": {
    object (Progress)
  },
  "progressBytes": {
    object (Progress)
  },
  "ttlConfigDelta": {
    object (TtlConfigDelta)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time this operation started. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                 |
| `endTime`             | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time this operation completed. Will be unset if operation still in progress. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `field`               | `string` The field resource that this operation is acting on. For example: `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}/fields/{fieldPath}`                                                                                                                                                                                                                                                                            |
| `indexConfigDeltas[]` | `object ( `[`IndexConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/FieldOperationMetadata#IndexConfigDelta)` )` A list of [`IndexConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/FieldOperationMetadata#IndexConfigDelta) , which describe the intent of this operation.                                                                                                  |
| `state`               | `enum ( `[`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/OperationState)` )` The state of the operation.                                                                                                                                                                                                                                                                                                   |
| `progressDocuments`   | `object ( `[`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress)` )` The progress, in documents, of this operation.                                                                                                                                                                                                                                                                                          |
| `progressBytes`       | `object ( `[`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress)` )` The progress, in bytes, of this operation.                                                                                                                                                                                                                                                                                              |
| `ttlConfigDelta`      | `object ( `[`TtlConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/FieldOperationMetadata#TtlConfigDelta)` )` Describes the deltas of TTL configuration.                                                                                                                                                                                                                                                           |

## IndexConfigDelta

Information about an index configuration change.

**JSON representation**

```
{
  "changeType": enum (ChangeType),
  "index": {
    object (Index)
  }
}
```

| Fields       |                                                                                                                                                       |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `changeType` | `enum ( `[`ChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ChangeType)` )` Specifies how the index is changing. |
| `index`      | `object ( `[`Index`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index)` )` The index being changed.                     |

## TtlConfigDelta

Information about a TTL configuration change.

**JSON representation**

```
{
  "changeType": enum (ChangeType),
  "expirationOffset": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                             |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `changeType`       | `enum ( ``ChangeType`` )` Specifies how the TTL configuration is changing.                                                                                                                                                                                                                                                  |
| `expirationOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` The offset, relative to the timestamp value in the TTL-enabled field, used determine the document's expiration time. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
