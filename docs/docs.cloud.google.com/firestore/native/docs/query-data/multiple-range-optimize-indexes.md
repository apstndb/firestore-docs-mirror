# Optimize queries with range and inequality filters on multiple fields

This page provides examples of indexing strategy that you can use for queries with range and inequality filters on multiple fields to create an efficient query experience.

Before you optimize your queries, read about [the related concepts](/firestore/native/docs/query-data/multiple-range-fields) .

## Optimize queries with Query Explain

To determine if your query and indexes are optimal, you can use [Query Explain](/firestore/native/docs/query-explain) to get the query plan summary and execution statistics of the query:

### Java

``` text
Query q = db.collection("employees").whereGreaterThan("salary",
100000).whereGreaterThan("experience", 0);

ExplainResults<QuerySnapshot> explainResults = q.explain(ExplainOptions.builder().analyze(true).build()).get();
ExplainMetrics metrics = explainResults.getMetrics();

PlanSummary planSummary = metrics.getPlanSummary();
ExecutionStats executionStats = metrics.getExecutionStats();

System.out.println(planSummary.getIndexesUsed());
System.out.println(stats.getResultsReturned());
System.out.println(stats.getExecutionDuration());
System.out.println(stats.getReadOperations());
System.out.println(stats.getDebugStats());
```

### Node.js

``` text
let q = db.collection("employees")
      .where("salary", ">", 100000)
      .where("experience", ">",0);

let options = { analyze : 'true' };
let explainResults = await q.explain(options);

let planSummary = explainResults.metrics.planSummary;
let stats = explainResults.metrics.executionStats;

console.log(planSummary);
console.log(stats);
```

The following example shows how the use of correct index ordering reduces the number of index entries that Firestore scans.

### Simple queries

With the [earlier example](/firestore/native/docs/query-data/multiple-range-fields#indexing_considerations) of a collection of employees, the simple query that runs with the `  (experience ASC, salary ASC)  ` index is as follows:

### Java

``` text
db.collection("employees")
  .whereGreaterThan("salary", 100000)
  .whereGreaterThan("experience", 0)
  .orderBy("experience")
  .orderBy("salary");
```

The query scans 95000 index entries only to return five documents. Since the query predicate isn't satisfied, a large number of index entries are read but are filtered out.

``` text
// Output query planning info
{
    "indexesUsed": [
        {
            "properties": "(experience ASC, salary ASC, __name__ ASC)",
            "query_scope": "Collection"
        }
    ],

    // Output Query Execution Stats
    "resultsReturned": "5",
    "executionDuration": "2.5s",
    "readOperations": "100",
    "debugStats": {
        "index_entries_scanned": "95000",
        "documents_scanned": "5",
        "billing_details": {
            "documents_billable": "5",
            "index_entries_billable": "95000",
            "small_ops": "0",
            "min_query_cost": "0"
        }
    }
}
```

You can infer from domain expertise that most employees will have at least some experience but few will have a salary that is more than 100000. Given this insight, you can see that the `  salary  ` constraint is more selective than the `  experience  ` constraint. To influence the index that Firestore uses to execute the query, specify an `  orderBy  ` clause that orders the `  salary  ` constraint before the `  experience  ` constraint.

### Java

``` text
db.collection("employees")
  .whereGreaterThan("salary", 100000)
  .whereGreaterThan("experience", 0)
  .orderBy("salary")
  .orderBy("experience");
```

When you explicitly use the `  orderBy()  ` clause to add the predicates, Firestore uses the `  (salary ASC, experience ASC)  ` index to run the query. Since the selectivity of the first range filter is higher in this query compared to the earlier query, the query runs faster and is more cost efficient.

``` text
// Output query planning info
{
    "indexesUsed": [
        {
            "properties": "(salary ASC, experience ASC, __name__ ASC)",
            "query_scope": "Collection"
        }
    ],

    // Output Query Execution Stats
    "resultsReturned": "5",
    "executionDuration": "0.2s",
    "readOperations": "6",
    "debugStats": {
        "index_entries_scanned": "1000",
        "documents_scanned": "5",
        "billing_details": {
            "documents_billable": "5",
            "index_entries_billable": "1000",
            "small_ops": "0",
            "min_query_cost": "0"
        }
    }
}
```

## What's next

  - Learn about [Query Explain](/firestore/native/docs/query-explain) .
  - Learn about [indexing best practices](/firestore/docs/concepts/index-overview#indexing_best_practices) .
