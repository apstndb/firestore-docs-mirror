# Analyze query performance statistics

This page describes how to use the Query insights dashboard to detect and analyze query performance.

## Query insights overview

Use the Query insights dashboard to monitor metrics-related queries. Based on the metrics, you can identify the most frequently used queries and queries with high latencies that might require optimization. Use the Query insights dashboard to help you with:

  - **Query performance optimization** : identify queries with high latencies and that might need optimization.
  - **Query cost management** : discover high-cost queries and optimize them to reduce costs.
  - **Query stats monitoring** : track query stats over time.

### Query insights data

Query insights includes data from the following API methods:

  - [`  listDocuments  `](/firestore/docs/reference/rest/v1/projects.databases.documents/listDocuments)
  - [`  listCollectionIds  `](/firestore/docs/reference/rest/v1/projects.databases.documents/listCollectionIds)
  - [`  runQuery  `](/firestore/docs/reference/rest/v1/projects.databases.documents/runQuery)
  - [`  runAggregationQuery  `](/firestore/docs/reference/rest/v1/projects.databases.documents/runAggregationQuery)
  - [`  partitionQuery  `](/firestore/docs/reference/rest/v1/projects.databases.documents/partitionQuery)

You can view data about the queries that use these methods for a given project, database, and time duration ranging from 10 minutes to 30 days. Data for queries with equivalent structures is captured under a single normalized query.

Query insights returns the following information about a query:

<table>
<tbody>
<tr class="odd">
<td>Normalized query text</td>
<td>The query structure represented in text.</td>
</tr>
<tr class="even">
<td>Execution count</td>
<td>Number of executions in the selected time window.</td>
</tr>
<tr class="odd">
<td>Error count</td>
<td>Number of errors in the selected time window.</td>
</tr>
<tr class="even">
<td>Average execution duration(ms)</td>
<td>The average time in milliseconds it took the database to process the query.</td>
</tr>
<tr class="odd">
<td>Average number of results returned</td>
<td>The number of results returned by the query. Results include documents, collection IDs, and aggregated buckets.</td>
</tr>
<tr class="even">
<td>Average number of documents scanned</td>
<td>The number of documents scanned in a query.</td>
</tr>
<tr class="odd">
<td>Average number of index entries scanned</td>
<td>The number of index entries examined to execute the query.</td>
</tr>
<tr class="even">
<td>Load by average time</td>
<td>Data to help filter for the top queries based on average latency.</td>
</tr>
<tr class="odd">
<td>Load by total (billable) read operations</td>
<td>Data to help filter for the top queries based on total billable read operations.</td>
</tr>
</tbody>
</table>

### Data granularity and retention

Data granularity depends on the duration specified:

  - 10 minute granularity for intervals up to 4 days ago
  - 1 hour granularity for intervals up to 30 days ago

The maximum data retention for Query insights is 30 days. 10-minute data is stored for 4 days, and hourly data is stored for 30 days.

### Limitations

  - [Real-time listeners](/firestore/docs/query-data/listen) are not included in Query insights statistics.
  - Query insights data is delayed by one to two hours.

## Pricing

There's no additional cost for Query insights.

## Required roles

To get the permission that you need to view the Query insights dashboard, ask your administrator to grant you the [Datastore Viewer](/iam/docs/roles-permissions/firestore#datastore.viewer) ( `  roles/datastore.viewer  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  datastore.insights.get  ` permission, which is required to view the Query insights dashboard.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## View Query insights

To view query insights for a Firestore database, open the database **Query insights** pane in the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list of databases, select a database.

3.  In the navigation menu, click **Query insights** .
    
    Use the **Load type** drop-down to find the top queries by either latency or number of read operations.

## What's next

  - Use [query explain](/firestore/docs/query-explain) to improve query performance
  - [Monitor usage](/firestore/docs/monitor-usage)
