---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rpc
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rpc
title: Cloud Datastore API
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

Accesses the schemaless NoSQL database to provide fully managed, robust, scalable storage for your application.

## Service: datastore.googleapis.com

The Service name `datastore.googleapis.com` is needed to create RPC client stubs.

## [`google.datastore.v1.Datastore`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore)

| Methods                                                                                                                                                        |                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| [`AllocateIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.AllocateIds)                 | Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted. |
| [`BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.BeginTransaction)       | Begins a new transaction.                                                                          |
| [`Commit`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.Commit)                           | Commits a transaction, optionally creating, deleting or modifying some entities.                   |
| [`Lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.Lookup)                           | Looks up entities by key.                                                                          |
| [`ReserveIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.ReserveIds)                   | Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.                      |
| [`Rollback`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.Rollback)                       | Rolls back a transaction.                                                                          |
| [`RunAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.RunAggregationQuery) | Runs an aggregation query.                                                                         |
| [`RunQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.Datastore.RunQuery)                       | Queries for entities.                                                                              |

## [`google.datastore.v1beta3.Datastore`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore)

| Methods                                                                                                                                                                  |                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| [`AllocateIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.AllocateIds)                 | Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted. |
| [`BeginTransaction`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.BeginTransaction)       | Begins a new transaction.                                                                          |
| [`Commit`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Commit)                           | Commits a transaction, optionally creating, deleting or modifying some entities.                   |
| [`Lookup`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Lookup)                           | Looks up entities by key.                                                                          |
| [`ReserveIds`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.ReserveIds)                   | Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.                      |
| [`Rollback`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.Rollback)                       | Rolls back a transaction.                                                                          |
| [`RunAggregationQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunAggregationQuery) | Runs an aggregation query.                                                                         |
| [`RunQuery`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.datastore.v1beta3#google.datastore.v1beta3.Datastore.RunQuery)                       | Queries for entities.                                                                              |

## [`google.longrunning.Operations`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations)

| Methods                                                                                                                                               |                                                                                                                              |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| [`CancelOperation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations.CancelOperation) | Starts asynchronous cancellation on a long-running operation.                                                                |
| [`DeleteOperation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations.DeleteOperation) | Deletes a long-running operation.                                                                                            |
| [`GetOperation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations.GetOperation)       | Gets the latest state of a long-running operation.                                                                           |
| [`ListOperations`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations.ListOperations)   | Lists operations that match the specified filter in the request.                                                             |
| [`WaitOperation`](https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.longrunning#google.longrunning.Operations.WaitOperation)     | Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state. |
