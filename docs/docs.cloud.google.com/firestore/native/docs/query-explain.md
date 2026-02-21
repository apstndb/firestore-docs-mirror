# Understand query performance using Query Explain

Query Explain allows you to submit Firestore in Native Mode queries to the backend and receive detailed performance statistics on backend query execution in return. It functions like the `  EXPLAIN [ANALYZE]  ` operation in many relational database systems.

Query Explain requests can be sent using the [Firestore server client libraries](/firestore/docs/reference/libraries#server_client_libraries) .

Query Explain results help you understand how your queries are executed, showing you inefficiencies and the location of likely server-side bottlenecks.

Query Explain:

  - Provides insights on the query planning phase so you can adjust your query indexes and boost efficiency.
  - Using the analyze option, helps you understand your cost and performance on a per-query basis and lets you quickly iterate through different query patterns in order to optimize their usage.

**Note:** Query Explain supports polled queries. Streaming queries are not yet supported.

## Understand Query Explain options: default and analyze

Query Explain operations can be performed using the *default* option or *analyze* option.

With the default option, Query Explain plans the query, but skips over the execution stage. This will return planner stage information. You can use this to check that a query has the necessary indexes and understand which indexes are used. This will help you to verify, for example, that a particular query is using a composite index over having to intersect over many different indexes.

With the analyze option, Query Explain both plans and executes the query. This returns all the previously mentioned planner information along with statistics from the query execution runtime. This will include the billing information of the query along with system-level insights into the query execution. You can use this tooling to test various query and index configurations to optimize their cost and latency.

## What does Query Explain cost?

When you use Query Explain with the default option, no index or read operations are performed. Regardless of query complexity, one read operation is charged.

When you use Query Explain with the analyze option, index and read operations are performed, so you are charged for the query as usual. There is no additional charge for the analysis activity, only the usual charge for the query being executed.

## Use Query Explain with the default option

You can use the client libraries to submit a default option request.

Note that requests are authenticated with IAM, using the same permissions for regular query operations. Other authentication techniques, like Firebase Authentication, are ignored. For more information, see the guide on [IAM for server client libraries](https://cloud.google.com/firestore/docs/security/iam) .

##### Java (Admin)

``` text
Query q = db.collection("col").whereGreaterThan("a", 1);
ExplainOptions options = ExplainOptions.builder().build();

ExplainResults<QuerySnapshot> explainResults = q.explain(options).get();
ExplainMetrics metrics = explainResults.getMetrics();
PlanSummary planSummary = metrics.getPlanSummary();

    
```

##### Node (Admin)

``` text
const q = db.collection('col').where('country', '=', 'USA');
const options = { analyze : 'false' };

const explainResults = await q.explain(options);

const metrics = explainResults.metrics;
const plan = metrics.planSummary;

    
```

The exact format of the response depends on the execution environment. Returned results can be converted to JSON. For example:

``` text
{
    "indexes_used": [
        {"query_scope": "Collection", "properties": "(category ASC, __name__ ASC)"},
        {"query_scope": "Collection", "properties": "(country ASC, __name__ ASC)"},
    ]
}
```

For more information, see the [Query Explain report reference](./query-explain-report-reference) .

## Use Query Explain with the analyze option

You can use the client libraries to submit an analyze option request.

Note that requests are authenticated with IAM, using the same permissions for regular query operations. Other authentication techniques, like Firebase Authentication, are ignored. For more information, see the guide on [IAM for server client libraries](https://cloud.google.com/firestore/docs/security/iam) .

**Note:** One query execution is analyzed at a time; therefore, query timing results may vary from request to request. The tool can help you spot significant structural inefficiencies, but is not intended to provide aggregate statistics on query performance.

##### Java (Admin)

``` text
Query q = db.collection("col").whereGreaterThan("a", 1);

ExplainOptions options = ExplainOptions.builder().setAnalyze(true).build();

ExplainResults<QuerySnapshot> explainResults = q.explain(options).get();

ExplainMetrics metrics = explainResults.getMetrics();
PlanSummary planSummary = metrics.getPlanSummary();
List<Map<String, Object>> indexesUsed = planSummary.getIndexesUsed();
ExecutionStats stats = metrics.getExecutionStats();

    
```

##### Node (Admin)

``` text
const q = db.collection('col').where('country', '=', 'USA');

const options = { analyze : 'true' };

const explainResults = await q.explain(options);

const metrics = explainResults.metrics;
const plan = metrics.planSummary;
const indexesUsed = plan.indexesUsed;
const stats = metrics.executionStats;

    
```

The following example shows the `  stats  ` object returned in addition to `  planInfo  ` . The exact format of the response depends on the execution environment. The example response is in JSON format.

``` text
{
    "resultsReturned": "5",
    "executionDuration": "0.100718s",
    "readOperations": "5",
    "debugStats": {
               "index_entries_scanned": "95000",
               "documents_scanned": "5"
               "billing_details": {
                     "documents_billable": "5",
                     "index_entries_billable": "0",
                     "small_ops": "0",
                     "min_query_cost": "0",
               }
    }

}
```

For more information, see the [Query Explain report reference](./query-explain-report-reference) .

## Interpret results and make adjustments

Let's look at an example scenario in which we query movies by genre and country of production.

**Note:** Query Explain is designed for useful ad hoc analysis; its report format will evolve to maximize ease of reading and understanding, not suitability for machine processing. Some metrics are expected to change as Firestore in Native Mode evolves (i.e., metrics may be added, removed, or updated) and are not covered by the same deprecation policy as other Firestore in Native Mode APIs. For more information, see the [Query Explain report reference](./query-explain-report-reference) .

For illustration, assume the equivalent of this SQL query.

``` text
SELECT *
FROM /movies
WHERE category = 'Romantic' AND country = 'USA';
```

If we use the analyze option, the returned metrics show the query runs on two single-field indexes, `  (category ASC, __name__ ASC)  ` and `  (country ASC, __name__ ASC)  ` . It scans 16500 index entries, but returns only 1200 documents.

``` text
// Output query planning info
{
    "indexes_used": [
        {"query_scope": "Collection", "properties": "(category ASC, __name__ ASC)"},
        {"query_scope": "Collection", "properties": "(country ASC, __name__ ASC)"},
    ]
}

// Output query status
{
    "resultsReturned": "1200",
    "executionDuration": "0.118882s",
    "readOperations": "1200",
    "debugStats": {
               "index_entries_scanned": "16500",
               "documents_scanned": "1200"
               "billing_details": {
                     "documents_billable": "1200",
                     "index_entries_billable": "0",
                     "small_ops": "0",
                     "min_query_cost": "0",
               }
    }
}
```

To optimize the performance of executing the query, you can create a fully-covered composite index `  (category ASC, country ASC, __name__ ASC)  ` .

Running the query with the analyze option again we can see that the newly-created index is selected for this query, and the query runs much faster and more efficiently.

``` text
// Output query planning info
{
    "indexes_used": [
        {"query_scope": "Collection", "properties": "(category ASC, country ASC,  __name__ ASC)"}
    ]
}

// Output query stats
{
    "resultsReturned": "1200",
    "executionDuration": "0.026139s",
    "readOperations": "1200",
    "debugStats": {
               "index_entries_scanned": "1200",
               "documents_scanned": "1200"
               "billing_details": {
                     "documents_billable": "1200",
                     "index_entries_billable": "0",
                     "small_ops": "0",
                     "min_query_cost": "0",
               }
    }
}
```
