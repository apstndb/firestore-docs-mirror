---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics
title: ExplainMetrics
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#SCHEMA_REPRESENTATION)
- [PlanSummary](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#PlanSummary)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#PlanSummary.SCHEMA_REPRESENTATION)
- [ExecutionStats](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#ExecutionStats)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#ExecutionStats.SCHEMA_REPRESENTATION)

Explain metrics for the query.

**JSON representation**

```
{
  "planSummary": {
    object (PlanSummary)
  },
  "executionStats": {
    object (ExecutionStats)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                  |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `planSummary`    | `object ( `[`PlanSummary`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#PlanSummary)` )` Planning phase information for the query.                                                                                                                                                                                    |
| `executionStats` | `object ( `[`ExecutionStats`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainMetrics#ExecutionStats)` )` Aggregated stats from the execution of the query. Only present when [`ExplainOptions.analyze`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1beta3/ExplainOptions#FIELDS.analyze) is set to true. |

## PlanSummary

Planning phase information for the query.

**JSON representation**

```
{
  "indexesUsed": [
    {
      object
    }
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexesUsed[]` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` The indexes selected for the query. For example: \[ {"query_scope": "Collection", "properties": "(foo ASC, **name** ASC)"}, {"query_scope": "Collection", "properties": "(bar ASC, **name** ASC)"} \] |

## ExecutionStats

Execution statistics for the query.

**JSON representation**

```
{
  "resultsReturned": string,
  "executionDuration": string,
  "readOperations": string,
  "debugStats": {
    object
  }
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resultsReturned`   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Total number of results returned, including documents, projections, aggregation results, keys.                                                                                                                                                                                                                                            |
| `executionDuration` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Total time to execute the query in the backend. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                                                           |
| `readOperations`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Total billable read operations.                                                                                                                                                                                                                                                                                                           |
| `debugStats`        | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Debugging statistics from the execution of the query. Note that the debugging stats are subject to change as Firestore evolves. It could include: { "indexes_entries_scanned": "1000", "documents_scanned": "20", "billing_details" : { "documents_billable": "20", "index_entries_billable": "1000", "min_query_cost": "0" } } |
