---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress
title: Progress
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Describes the progress of the operation. Unit of work is generic and must be interpreted based on where [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Progress) is used.

**JSON representation**

```
{
  "estimatedWork": string,
  "completedWork": string
}
```

| Fields          |                                                                                                                      |
|-----------------|----------------------------------------------------------------------------------------------------------------------|
| `estimatedWork` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The amount of work estimated. |
| `completedWork` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The amount of work completed. |
