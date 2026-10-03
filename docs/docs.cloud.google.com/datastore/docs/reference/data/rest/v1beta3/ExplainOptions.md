---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainOptions
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainOptions
title: ExplainOptions
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainOptions#SCHEMA_REPRESENTATION)

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
