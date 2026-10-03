---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ExportDocumentsResponse
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ExportDocumentsResponse
title: ExportDocumentsResponse
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Returned in the [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Operation) response field.

**JSON representation**

```
{
  "outputUriPrefix": string
}
```

| Fields            |                                                                                                                                                                               |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputUriPrefix` | `string` Location of the output files. This can be used to begin an import into Cloud Firestore (this project or another project) after the operation completes successfully. |
