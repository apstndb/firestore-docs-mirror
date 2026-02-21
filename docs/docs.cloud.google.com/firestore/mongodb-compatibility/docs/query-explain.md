# Analyze query execution with Query Explain

This page describes how to retrieve query execution information when you execute a query.

## Use Query Explain

You can use Query Explain to understand how your queries are being executed. This provides details that you can use to [optimize your queries](/firestore/mongodb-compatibility/docs/optimize-query-performance) .

You can use Query Explain through the Google Cloud console or the `  explain  ` command.

##### Console

Execute a query in the Query Editor and open the **Explanation** tab:

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list of databases, select a Firestore with MongoDB compatibility database. The Google Cloud console opens the **Firestore Explorer** for that database.

3.  Enter a query in the query editor and click **Run** .

4.  Click the **Explanation** tab to view the query analysis output.

##### MongoDB API

Query Explain in the MongoDB API is supported through the [`  explain  `](https://www.mongodb.com/docs/manual/reference/command/explain/) command which you can use in tools such as Mongo Shell and Compass.

The `  explain  ` command is supported with the `  aggregate  ` , `  find  ` , `  distinct  ` , and `  count  ` commands, for example:

``` text
db.collection.explain('executionStats').find(...)
```

You can also use the `  explain()  ` method, for example:

``` text
db.collection.find({QUERY}).explain('executionStats')
```

###### Limitations

Note the following limitations and differences:

  - Query Explain does not support commands which return a cursor. For example, invoking explain by calling the following command directly is not supported:
    
    ``` text
    db.collection.aggregate(..., explain: true)
    ```

  - Query Explain is only supported on the `  find  ` , `  aggregate  ` , `  count  ` , and `  distinct  ` commands.

  - The `  Verbosity  ` and `  Comment  ` options of Query Explain are not supported through the MongoDB API. The behaviour matches the `  executionStats  ` option. The `  allPlansExecution  ` and `  queryPlanner  ` options are ignored if provided.
    
    If no verbosity is provided, the shell uses the `  queryPlanner  ` verbosity and filters out execution stats. You must use the `  executionStats  ` or `  allPlansExecution  ` verbosity to see the full output.

## Analysis

The output of Query Explain contains two main components-the Summary Statistics and Execution Tree. Consider this query as an example:

``` text
db.order.aggregate(
 [
   { "$match": { "user_id": 1234 } },
   { "$sort": { "date_placed": 1 } }
 ]
)
```

## Summary Statistics

The top of the explained output contains a summary of the execution statistics. Use these statistics to determine if a query has high latency or cost. It also contains memory statistics which let you know how close your query is to [memory limits](/firestore/mongodb-compatibility/quotas) .

``` text
Billing Metrics:
read units: 1

Execution Metrics:
request peak memory usage: 4.00 KiB (4,096 B)
results returned: 1
```

## Execution Tree

The execution tree describes the query execution as a series of nodes. The bottom nodes (leaf nodes) retrieve data from the storage layer which traverses up the tree to generate a query response.

For details about each execution node, refer to the [Execution reference](/firestore/mongodb-compatibility/docs/query-explain-reference) .

For details on how to use this information to optimize your queries, see [Optimize query execution](/firestore/mongodb-compatibility/docs/optimize-query-performance) .

The following is an example of an execution tree:

``` text
• Compute
|  $out_1: map_set($record_1, "__id__", $__id___1, "__key__", $__key___1, "__row_id__", $__row_id___1, "__$0__", $__$0___2)
|  is query result: true
|
|  Execution:
|   records returned: 1
|
└── • Compute
    |  $__$0___2: UNSET
    |
    |  Execution:
    |   records returned: 1
    |
    └── • Compute
        |  $__key___1: UNSET
        |  $__row_id___1: UNSET
        |
        |  Execution:
        |   records returned: 1
        |
        └── • Compute
            |  $__id___1: _id($record_1.__key__)
            |
            |  Execution:
            |   records returned: 1
            |
            └── • MajorSort
                |  fields: [$v_5 ASC]
                |  output: [$record_1]
                |
                |  Execution:
                |   records returned: 1
                |   peak memory usage: 4.00 KiB (4,096 B)
                |
                └── • Compute
                    |  $v_5: array_get($v_4, 0L)
                    |
                    |  Execution:
                    |   records returned: 1
                    |
                    └── • Compute
                        |  $v_4: sortPaths(array($record_1.date_placed), [date_placed ASC])
                        |
                        |  Execution:
                        |   records returned: 1
                        |
                        └── • Filter
                            |  expression: $eq($user_id_1, 1,234)
                            |
                            |  Execution:
                            |   records returned: 1
                            |
                            └── • TableScan
                                   source: **/my_collection
                                   order: STABLE
                                   properties: * - { __create_time__, __update_time__ }
                                   output record: $record_1
                                   output bindings: {$user_id_1=user_id}
                                   variables: [$record_1, $user_id_1]

                                   Execution:
                                    records returned: 1
                                    records scanned: 1
```

## What's next

  - To learn about the execution tree nodes, see the [Query execution reference](/firestore/mongodb-compatibility/docs/query-explain-reference) .
  - To learn how to optimize your queries, see [Optimize query execution](/firestore/mongodb-compatibility/docs/optimize-query-performance) .
