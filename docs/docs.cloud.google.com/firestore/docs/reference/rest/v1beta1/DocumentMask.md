---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/DocumentMask
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/DocumentMask
title: DocumentMask
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

A set of field paths on a document. Used to restrict a get or update operation on a document to a subset of its fields. This is different from standard field masks, as this is always scoped to a [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents#Document) , and takes in account the dynamic nature of `Value` .

**JSON representation**

```
{
  "fieldPaths": [
    string
  ]
}
```

| Fields         |                                                                                                                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fieldPaths[]` | `string` The list of field paths in the mask. See [`Document.fields`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents#Document.FIELDS.fields) for a field path syntax reference. |
