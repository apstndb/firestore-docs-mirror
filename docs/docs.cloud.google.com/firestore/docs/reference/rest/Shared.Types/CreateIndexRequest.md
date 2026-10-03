---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/CreateIndexRequest
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/CreateIndexRequest
title: CreateIndexRequest
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

The request for `FirestoreAdmin.CreateIndex` .

**JSON representation**

```
{
  "parent": string,
  "index": {
    object (Index)
  }
}
```

| Fields   |                                                                                                                                                   |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent` | `string` Required. A parent name of the form `projects/{projectId}/databases/{databaseId}/collectionGroups/{collectionId}`                        |
| `index`  | `object ( `[`Index`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Index)` )` Required. The composite index to create. |
