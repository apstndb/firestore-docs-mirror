Accesses the schemaless NoSQL database to provide fully managed, robust, scalable storage for your application.

  - [REST Resource: v1beta3.projects](#v1beta3.projects)
  - [REST Resource: v1.projects](#v1.projects)
  - [REST Resource: v1.projects.operations](#v1.projects.operations)

## Service: datastore.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

  - <https://datastore.googleapis.com/$discovery/rest?version=v1>
  - <https://datastore.googleapis.com/$discovery/rest?version=v1beta3>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

  - `  https://datastore.googleapis.com  `

## REST Resource: [v1beta3.projects](/datastore/docs/reference/data/rest/v1beta3/projects)

Methods

`  allocateIds  `

`  POST /v1beta3/projects/{projectId}:allocateIds  `  
Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

`  beginTransaction  `

`  POST /v1beta3/projects/{projectId}:beginTransaction  `  
Begins a new transaction.

`  commit  `

`  POST /v1beta3/projects/{projectId}:commit  `  
Commits a transaction, optionally creating, deleting or modifying some entities.

`  lookup  `

`  POST /v1beta3/projects/{projectId}:lookup  `  
Looks up entities by key.

`  reserveIds  `

`  POST /v1beta3/projects/{projectId}:reserveIds  `  
Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

`  rollback  `

`  POST /v1beta3/projects/{projectId}:rollback  `  
Rolls back a transaction.

`  runAggregationQuery  `

`  POST /v1beta3/projects/{projectId}:runAggregationQuery  `  
Runs an aggregation query.

`  runQuery  `

`  POST /v1beta3/projects/{projectId}:runQuery  `  
Queries for entities.

## REST Resource: [v1.projects](/datastore/docs/reference/data/rest/v1/projects)

Methods

`  allocateIds  `

`  POST /v1/projects/{projectId}:allocateIds  `  
Allocates IDs for the given keys, which is useful for referencing an entity before it is inserted.

`  beginTransaction  `

`  POST /v1/projects/{projectId}:beginTransaction  `  
Begins a new transaction.

`  commit  `

`  POST /v1/projects/{projectId}:commit  `  
Commits a transaction, optionally creating, deleting or modifying some entities.

`  lookup  `

`  POST /v1/projects/{projectId}:lookup  `  
Looks up entities by key.

`  reserveIds  `

`  POST /v1/projects/{projectId}:reserveIds  `  
Prevents the supplied keys' IDs from being auto-allocated by Cloud Datastore.

`  rollback  `

`  POST /v1/projects/{projectId}:rollback  `  
Rolls back a transaction.

`  runAggregationQuery  `

`  POST /v1/projects/{projectId}:runAggregationQuery  `  
Runs an aggregation query.

`  runQuery  `

`  POST /v1/projects/{projectId}:runQuery  `  
Queries for entities.

## REST Resource: [v1.projects.operations](/datastore/docs/reference/data/rest/v1/projects.operations)

Methods

`  cancel  `

`  POST /v1/{name=projects/*/operations/*}:cancel  `  
Starts asynchronous cancellation on a long-running operation.

`  delete  `

`  DELETE /v1/{name=projects/*/operations/*}  `  
Deletes a long-running operation.

`  get  `

`  GET /v1/{name=projects/*/operations/*}  `  
Gets the latest state of a long-running operation.

`  list  `

`  GET /v1/{name=projects/*}/operations  `  
Lists operations that match the specified filter in the request.
