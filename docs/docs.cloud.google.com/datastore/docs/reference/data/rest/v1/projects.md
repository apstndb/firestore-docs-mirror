---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects
title: 'REST Resource: projects'
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [Resource](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects#RESOURCE_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects#METHODS_SUMMARY)

## Resource

There is no persistent data associated with this resource.

| Methods                                                                                                                   |                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| [`allocateIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/allocateIds)                 | Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted. |
| [`beginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/beginTransaction)       | Begins a new transaction.                                                                          |
| [`commit`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/commit)                           | Commits a transaction, optionally creating, deleting or modifying some entities.                   |
| [`lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/lookup)                           | Looks up entities by key.                                                                          |
| [`reserveIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/reserveIds)                   | Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.                      |
| [`rollback`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/rollback)                       | Rolls back a transaction.                                                                          |
| [`runAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runAggregationQuery) | Runs an aggregation query.                                                                         |
| [`runQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/projects/runQuery)                       | Queries for entities.                                                                              |
