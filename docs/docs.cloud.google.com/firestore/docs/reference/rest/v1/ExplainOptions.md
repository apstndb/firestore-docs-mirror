---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/ExplainOptions
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/ExplainOptions
title: ExplainOptions
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Explain options for the query.

**JSON representation**

```
{
  "analyze": boolean
}
```

| Fields    |                                                                                                                                                                                                                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `analyze` | `boolean` Optional. Whether to execute this query. When false (the default), the query will be planned, returning only metrics from the planning stages. When true, the query will be planned and executed, returning the full query results along with both planning and execution stage metrics. |
