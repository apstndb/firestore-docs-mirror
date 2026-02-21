# Analyze query execution with Query Explain

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to retrieve query execution information when you execute a query.

## Use Query Explain

You can use Query Explain to understand how your queries are being executed. This provides details that you can use to [optimize your queries](/firestore/docs/pipeline/enterprise-optimize-query-performance) .

You can use Query Explain through the Google Cloud console.

##### Console

Execute a query in the Query Editor and open the **Explanation** tab:

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list of databases, select a Firestore database. The Google Cloud console opens the **Firestore Explorer** for that database.

3.  Enter a query in the query editor and click **Run** .

4.  Click the **Explanation** tab to view the query analysis output.

## Analysis

The output of Query Explain contains two main components-the Summary Statistics and Execution Tree. Consider this query as an example:

``` text
db.pipeline().collection('/users').sort(field("status").ascending()).limit(100)
```

## Summary Statistics

The top of the explained output contains a summary of the execution statistics. Use these statistics to determine if a query has high latency or cost. It also contains memory statistics which let you know how close your query is to [memory limits](/firestore/mongodb-compatibility/quotas#reads_writes_and_transactions) .

``` text
Execution:
 results returned: 2
 request peak memory usage: 20.25 KiB (20,736 B)
 data bytes read: 148 B
 entity row scanned: 2

Billing:
 read units: 1
```

## Execution Tree

The execution tree describes the query execution as a series of nodes. The bottom nodes (leaf nodes) retrieve data from the storage layer which traverses up the tree to generate a query response.

For details about each execution node, refer to the [Execution reference](/firestore/docs/pipeline/enterprise-query-explain-reference) .

For details on how to use this information to optimize your queries, see [Optimize query execution](/firestore/docs/pipeline/optimize-query-performance) .

The following is an example of an execution tree:

``` text
Tree:
• Compute
|  $out_1: map_set($record_1, "__name__", $__name___1, "__key__", unset)
|  is query result: true
|
|  Execution:
|   records returned: 2
|   latency: 5.96 ms (local <1 ms)
|
└── • Compute
    |  $__name___1: map_get($record_1, "__key__")
    |
    |  Execution:
    |   records returned: 2
    |   latency: 5.88 ms (local <1 ms)
    |
    └── • MajorSort
        |  fields: [$v_1 ASC]
        |  output: [$record_1]
        |  limit: 100
        |
        |  Execution:
        |   records returned: 2
        |   latency: 5.86 ms (local <1 ms)
        |   peak memory usage: 20.25 KiB (20,736 B)
        |
        └── • Compute
            |  $v_1: map_get($record_1, "status")
            |
            |  Execution:
            |   records returned: 2
            |   latency: 5.23 ms (local <1 ms)
            |
            └── • TableScan
                   source: /users
                   order: UNDEFINED
                   properties: *
                   row range: (-∞..+∞)
                   output record: $record_1
                   variables: [$record_1]

                   Execution:
                    records returned: 2
                    latency: 4.68 ms
                    records scanned: 2
                    data bytes read: 148 B
```

## What's next

  - To learn about the execution tree nodes, see the [Query execution reference](/firestore/docs/pipeline/enterprise-query-explain-reference) .
  - To learn how to optimize your queries, see [Optimize query execution](/firestore/docs/pipeline/enterprise-optimize-query-performance) .
