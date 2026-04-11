**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The following values are returned as results to operations performed with [Query Explain](https://docs.cloud.google.com/datastore/docs/query-explain-analyze) .

**Note:** The Query Explain is designed for useful ad hoc analysis; its report format will evolve to maximize ease of reading and understanding, not suitability for machine processing. The returned metrics are expected to change as Datastore mode evolves (metrics may be added, removed, or updated) and are not covered by the same deprecation policy as other Firestore APIs. See the tables below for more information about stability

## Plan records

| Key           | Type                                                                                       | Subject to change?                                              | Description                                                                                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| indexes\_used | List of [Generic Structs](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) | Yes, the contents in the Struct response are subject to change. | List of indexes selected for this query. See [below](https://docs.cloud.google.com/datastore/docs/query-explain-analyze-report-reference#query-analyze-reference-indexes-used) . |

### Indexes used

The contents of indexes used are subject to change as Datastore mode evolves.

| Key          | Type   | Description                                                                                                 |
| ------------ | ------ | ----------------------------------------------------------------------------------------------------------- |
| query\_scope | String | The scope at which a query is run. For example `Collection` , `Collection Group` and `Includes Ancestors` . |
| properties   | String | The index fields in a format, for example `(age ASC, __name__ ASC)` .                                       |

## Execution statistics

Aggregated execution statistics for the query.

| Key                 | Type           | Field subject to change?                                        | Description                                                                                                                                                                                  |
| ------------------- | -------------- | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| results\_returned   | long           | No                                                              | Total number of results returned, including entities, projections, aggregation results, keys.                                                                                                |
| execution\_duration | Duration       | No                                                              | Total time to execute the query in the backend.                                                                                                                                              |
| read\_operations    | long           | No                                                              | Total billable read operations.                                                                                                                                                              |
| debug\_stats        | Generic Struct | Yes, the contents in the Struct response are subject to change. | Debugging statistics from the execution of the query. See [below](https://docs.cloud.google.com/datastore/docs/query-explain-analyze-report-reference#query-analyze-reference-debug-stats) . |

### Debug statistics

The following results are helpful for debugging use cases and analysis of raw, optional statistics.

The contents of debug stats are subject to change as Datastore mode evolves.

| Key                     | Type           | Description                                                                                                    |
| ----------------------- | -------------- | -------------------------------------------------------------------------------------------------------------- |
| index\_entries\_scanned | String         | Total number of index entries inspected during the query.                                                      |
| documents\_scanned      | String         | Total number of documents scanned during the query.                                                            |
| billing\_details        | Generic Struct | Billing details including metrics like: "documents\_billable", "index\_entries\_billable", "min\_query\_cost". |

## What's next

  - [Learn more about running queries with explain and analyze](https://docs.cloud.google.com/datastore/docs/query-explain-analyze)
  - [Learn more about optimizing queries and indexes](https://docs.cloud.google.com/datastore/docs/concepts/optimize-indexes)
