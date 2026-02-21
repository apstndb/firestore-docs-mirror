  - [Resource](#RESOURCE_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource

There is no persistent data associated with this resource.

## Methods

### `             allocateIds           `

Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

### `             beginTransaction           `

Begins a new transaction.

### `             commit           `

Commits a transaction, optionally creating, deleting or modifying some entities.

### `             lookup           `

Looks up entities by key.

### `             reserveIds           `

Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

### `             rollback           `

Rolls back a transaction.

### `             runAggregationQuery           `

Runs an aggregation query.

### `             runQuery           `

Queries for entities.
