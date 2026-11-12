---
name: documents/docs.cloud.google.com/datastore/docs/query-insights
uri: https://docs.cloud.google.com/datastore/docs/query-insights
title: Analyze query performance statistics
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

This page describes how to use the Query insights dashboard to detect and analyze query performance.

## Query insights overview

Use the Query insights dashboard to monitor metrics-related queries. Based on the metrics, you can identify the most frequently used queries and queries with high latencies that might require optimization. Use the Query insights dashboard to help you with:

- **Query performance optimization** : identify queries with high latencies and that might need optimization.
- **Query cost management** : discover high-cost queries and optimize them to reduce costs.
- **Query stats monitoring** : track query stats over time.
- **Index recommendations** : present in the dashboard, but always empty.

### Query insights data

Query insights includes data from the following API methods:

- [`runQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery)
- [`runAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runAggregationQuery)

You can view data about the queries that use these methods for a given project, database, and time duration ranging from 10 minutes to 30 days. Data for queries with equivalent structures is captured under a single normalized query.

Query insights returns the following information about a query:

|                                          |                                                                                                                       |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Normalized query text                    | The query structure represented in text.                                                                              |
| Execution count                          | Number of executions in the selected time window.                                                                     |
| Error count                              | Number of errors in the selected time window.                                                                         |
| Average execution duration(ms)           | The average time in milliseconds it took the database to process the query.                                           |
| Average number of results returned       | The number of results returned by the query. Results include entities, kind IDs, projections, and aggregated buckets. |
| Average number of entities scanned       | The number of entities scanned in a query.                                                                            |
| Average number of index entries scanned  | The number of index entries examined to execute the query.                                                            |
| Load by average time                     | Data to help filter for the top queries based on average latency.                                                     |
| Load by total (billable) read operations | Data to help filter for the top queries based on total billable read operations.                                      |
| Index recommendations                    | In Firestore in Datastore mode, this field is present in Query insights but is always empty.                          |

### Data granularity and retention

Data granularity depends on the duration specified:

- 10 minute granularity for intervals up to 4 days ago
- 1 hour granularity for intervals up to 30 days ago

The maximum data retention for Query insights is 30 days. 10-minute data is stored for 4 days, and hourly data is stored for 30 days.

## View Query insights

To view query insights for a Firestore in Datastore mode database, open the database **Query insights** pane in the Google Cloud console.

1.  In the Google Cloud console, go to the **Databases** page.

2.  From the list of databases, select a database.

3.  In the navigation menu, click **Query insights** .

    ![The database usage dashboard in the console.](https://docs.cloud.google.com/static/firestore/native/docs/images/datastore-query-insights.png)

    Use the **Load type** drop-down to find the top queries by either latency or number of read operations.

## Index recommendations

In Firestore in Datastore mode, the **Index recommendations** field is visible in the Query insights dashboard, but recommendations aren't generated for Datastore mode databases. Index recommendations are available only for Firestore Enterprise edition databases in Native mode and MongoDB compatibility.

### Limitations

- In Firestore in Datastore mode, the index recommendations field is present in the Query insights dashboard, but is always empty.
- Query insights data is delayed by one to two hours.
- Index recommendations are generated periodically based on historical query data, not in real time.
- Index recommendations suggest new composite indexes; they don't suggest modifying or deleting existing indexes.
- Automatic index creation isn't supported; recommended indexes must be created manually.
- Query normalization replaces literal values with placeholders. Index recommendations are based on normalized query templates rather than specific runtime values.
- Cost evaluation uses heuristics rather than live data sampling. Recommended indexes might not improve performance in every scenario, and creating an index adds write and storage overhead.

## Pricing

There's no additional cost for Query insights or index recommendations.

## Required roles

To get the permissions that you need to view the Query insights dashboard and create recommended indexes, ask your administrator to grant you the following IAM roles on your project:

- View Query insights: [Datastore Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore#datastore.viewer) ( `roles/datastore.viewer` )
- Create recommended indexes:
  - [Datastore Index Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore#datastore.indexAdmin) ( `roles/datastore.indexAdmin` )
  - [Cloud Datastore Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore#datastore.owner) ( `roles/datastore.owner` )
  - [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/editor` )
  - [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/owner` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to view the Query insights dashboard and create recommended indexes. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to view the Query insights dashboard and create recommended indexes:

- View Query insights: `datastore.insights.get`
- Create recommended indexes:
  - `datastore.indexes.create`
  - `datastore.indexes.update`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## What's next

- Use [query explain](https://docs.cloud.google.com/datastore/docs/query-explain-analyze) to improve query performance
- [Monitor usage](https://docs.cloud.google.com/datastore/docs/understand-performance-monitoring)
