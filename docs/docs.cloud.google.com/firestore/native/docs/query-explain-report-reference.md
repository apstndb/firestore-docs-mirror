---
name: documents/docs.cloud.google.com/firestore/native/docs/query-explain-report-reference
uri: https://docs.cloud.google.com/firestore/native/docs/query-explain-report-reference
title: Query Explain report reference
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Query Explain report reference

The following values are returned as results to operations performed with [Firestore Query Explain](https://docs.cloud.google.com/firestore/native/docs/query-explain) .

> **Note:** Query Explain is designed for useful ad hoc analysis; its report format will evolve to maximize ease of reading and understanding, not suitability for machine processing. Some metrics are expected to change as Firestore in Native Mode evolves (i.e., metrics may be added, removed, or updated) and are not covered by the same deprecation policy as other Firestore in Native Mode APIs. The following tables indicate which portions of the data are subject to change.

## Plan records

| Key           | Type                                                                                       | Field subject to change?                                        | Description                                                                                                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| indexes\_used | List of [Generic Structs](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) | Yes, the contents in the Struct response are subject to change. | List of indexes selected for this query. See [below](https://docs.cloud.google.com/firestore/native/docs/query-explain-report-reference#query-analyze-reference-indexes-used) . |

### Indexes used

The contents of indexes used are subject to change as Firestore in Native Mode evolves.

| Key          | Type   | Description                                                                                                  |
| ------------ | ------ | ------------------------------------------------------------------------------------------------------------ |
| query\_scope | String | The scope at which a query is run. For example: `Collection` , `Collection Group` and `Includes Ancestors` . |
| properties   | String | The index fields in a format. For example: `(age ASC, __name__ ASC)` .                                       |

## Execution statistics

Aggregated execution statistics for the query.

| Key                 | Type                                                                              | Field subject to change?                                        | Description                                                                                                                                                                                 |
| ------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| results\_returned   | long                                                                              | No                                                              | Total number of results returned, including documents, projections, aggregation results, keys.                                                                                              |
| execution\_duration | [Duration](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)     | No                                                              | Total time to execute the query in the backend.                                                                                                                                             |
| read\_operations    | long                                                                              | No                                                              | Total billable read operations.                                                                                                                                                             |
| debug\_stats        | [Generic Struct](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) | Yes, the contents in the Struct response are subject to change. | Debugging statistics from the execution of the query. See [below](https://docs.cloud.google.com/firestore/native/docs/query-explain-report-reference#query-analyze-reference-debug-stats) . |

### Debug statistics

The following results are helpful for debugging use cases and analysis of raw, optional statistics.

The contents of debug statistics are subject to change as Firestore in Native Mode evolves.

| Key                     | Type                                                                              | Description                                                                                                                                             |
| ----------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| index\_entries\_scanned | String                                                                            | Total number of index entries inspected during the query.                                                                                               |
| documents\_scanned      | String                                                                            | Total number of documents scanned during the query.                                                                                                     |
| billing\_details        | [Generic Struct](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) | Billing details including metrics like: "documents\_billable", "index\_entries\_billable", "knn\_vector\_index\_entries\_billable", "min\_query\_cost". |
