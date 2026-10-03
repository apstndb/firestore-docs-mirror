---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ImportDocumentsMetadata
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ImportDocumentsMetadata
title: ImportDocumentsMetadata
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation) results from [`FirestoreAdmin.ImportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/importDocuments#google.firestore.admin.v1.FirestoreAdmin.ImportDocuments) .

**JSON representation**

```
{
  "startTime": string,
  "endTime": string,
  "operationState": enum (OperationState),
  "progressDocuments": {
    object (Progress)
  },
  "progressBytes": {
    object (Progress)
  },
  "collectionIds": [
    string
  ],
  "inputUriPrefix": string,
  "namespaceIds": [
    string
  ]
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time this operation started. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                 |
| `endTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The time this operation completed. Will be unset if operation still in progress. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `operationState`    | `enum ( `[`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/OperationState)` )` The state of the import operation.                                                                                                                                                                                                                                                                                            |
| `progressDocuments` | `object ( `[`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress)` )` The progress, in documents, of this operation.                                                                                                                                                                                                                                                                                          |
| `progressBytes`     | `object ( `[`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress)` )` The progress, in bytes, of this operation.                                                                                                                                                                                                                                                                                              |
| `collectionIds[]`   | `string` Which collection IDs are being imported.                                                                                                                                                                                                                                                                                                                                                                                                      |
| `inputUriPrefix`    | `string` The location of the documents being imported.                                                                                                                                                                                                                                                                                                                                                                                                 |
| `namespaceIds[]`    | `string` Which namespace IDs are being imported.                                                                                                                                                                                                                                                                                                                                                                                                       |
