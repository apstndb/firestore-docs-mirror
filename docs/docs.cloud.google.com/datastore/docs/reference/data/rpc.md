Accesses the schemaless NoSQL database to provide fully managed, robust, scalable storage for your application.

## Service: datastore.googleapis.com

The Service name `  datastore.googleapis.com  ` is needed to create RPC client stubs.

## `         google.datastore.v1.Datastore       `

Methods

`  AllocateIds  `

Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

`  BeginTransaction  `

Begins a new transaction.

`  Commit  `

Commits a transaction, optionally creating, deleting or modifying some entities.

`  Lookup  `

Looks up entities by key.

`  ReserveIds  `

Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

`  Rollback  `

Rolls back a transaction.

`  RunAggregationQuery  `

Runs an aggregation query.

`  RunQuery  `

Queries for entities.

## `         google.datastore.v1beta3.Datastore       `

Methods

`  AllocateIds  `

Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

`  BeginTransaction  `

Begins a new transaction.

`  Commit  `

Commits a transaction, optionally creating, deleting or modifying some entities.

`  Lookup  `

Looks up entities by key.

`  ReserveIds  `

Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

`  Rollback  `

Rolls back a transaction.

`  RunAggregationQuery  `

Runs an aggregation query.

`  RunQuery  `

Queries for entities.

## `         google.longrunning.Operations       `

Methods

`  CancelOperation  `

Starts asynchronous cancellation on a long-running operation.

`  DeleteOperation  `

Deletes a long-running operation.

`  GetOperation  `

Gets the latest state of a long-running operation.

`  ListOperations  `

Lists operations that match the specified filter in the request.

`  WaitOperation  `

Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.
