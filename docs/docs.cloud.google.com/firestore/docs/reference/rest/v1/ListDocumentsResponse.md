---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/ListDocumentsResponse
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/ListDocumentsResponse
title: ListDocumentsResponse
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

The response for [`Firestore.ListDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/list#google.firestore.v1.Firestore.ListDocuments) .

**JSON representation**

```
{
  "documents": [
    {
      object (Document)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]`   | `object ( `[`Document`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents#Document)` )` The Documents found. |
| `nextPageToken` | `string` A token to retrieve the next page of documents. If this field is omitted, there are no subsequent pages.                                      |
