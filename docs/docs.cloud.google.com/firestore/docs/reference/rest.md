---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest
uri: https://docs.cloud.google.com/firestore/docs/reference/rest
title: Cloud Firestore API
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

Accesses the NoSQL document database built for automatic scaling, high performance, and ease of application development.

## Service: firestore.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

- <https://firestore.googleapis.com/$discovery/rest?version=v1>
- <https://firestore.googleapis.com/$discovery/rest?version=v1beta2>
- <https://firestore.googleapis.com/$discovery/rest?version=v1beta1>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

- `https://firestore.googleapis.com`

### Regional service endpoint

A regional service endpoint is a base URL that specifies the network address of an API service in a single region. A service that is available in multiple regions might have multiple regional endpoints. Select a location to see its regional service endpoint for this service.

  

`https://firestore.googleapis.com`

## REST Resource: [v1beta2.projects.databases](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases)

| Methods                                                                                                                     |                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`exportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases/exportDocuments) | `POST /v1beta2/{name=projects/*/databases/*}:exportDocuments` Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. |
| [`importDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases/importDocuments) | `POST /v1beta2/{name=projects/*/databases/*}:importDocuments` Imports documents into Google Cloud Firestore.                                                                                      |

## REST Resource: [v1beta2.projects.databases.collectionGroups.fields](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.fields)

| Methods                                                                                                                         |                                                                                                                                        |
|---------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.fields/get)     | `GET /v1beta2/{name=projects/*/databases/*/collectionGroups/*/fields/*}` Gets the metadata and configuration for a Field.              |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.fields/list)   | `GET /v1beta2/{parent=projects/*/databases/*/collectionGroups/*}/fields` Lists the field configuration and metadata for this database. |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.fields/patch) | `PATCH /v1beta2/{field.name=projects/*/databases/*/collectionGroups/*/fields/*}` Updates a field configuration.                        |

## REST Resource: [v1beta2.projects.databases.collectionGroups.indexes](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes)

| Methods                                                                                                                            |                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/create) | `POST /v1beta2/{parent=projects/*/databases/*/collectionGroups/*}/indexes` Creates a composite index.   |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/delete) | `DELETE /v1beta2/{name=projects/*/databases/*/collectionGroups/*/indexes/*}` Deletes a composite index. |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/get)       | `GET /v1beta2/{name=projects/*/databases/*/collectionGroups/*/indexes/*}` Gets a composite index.       |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta2/projects.databases.collectionGroups.indexes/list)     | `GET /v1beta2/{parent=projects/*/databases/*/collectionGroups/*}/indexes` Lists composite indexes.      |

## REST Resource: [v1beta1.projects.databases](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases)

| Methods                                                                                                                     |                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`exportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases/exportDocuments) | `POST /v1beta1/{name=projects/*/databases/*}:exportDocuments` Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. |
| [`importDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases/importDocuments) | `POST /v1beta1/{name=projects/*/databases/*}:importDocuments` Imports documents into Google Cloud Firestore.                                                                                      |

## REST Resource: [v1beta1.projects.databases.documents](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents)

| Methods                                                                                                                                       |                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`batchGet`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchGet)                       | `POST /v1beta1/{database=projects/*/databases/*}/documents:batchGet` Gets multiple documents.                                                                             |
| [`batchWrite`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/batchWrite)                   | `POST /v1beta1/{database=projects/*/databases/*}/documents:batchWrite` Applies a batch of write operations.                                                               |
| [`beginTransaction`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/beginTransaction)       | `POST /v1beta1/{database=projects/*/databases/*}/documents:beginTransaction` Starts a new transaction.                                                                    |
| [`commit`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/commit)                           | `POST /v1beta1/{database=projects/*/databases/*}/documents:commit` Commits a transaction, while optionally updating documents.                                            |
| [`createDocument`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/createDocument)           | `POST /v1beta1/{parent=projects/*/databases/*/documents/**}/{collectionId}` Creates a new document.                                                                       |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/delete)                           | `DELETE /v1beta1/{name=projects/*/databases/*/documents/*/**}` Deletes a document.                                                                                        |
| [`executePipeline`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/executePipeline)         | `POST /v1beta1/{database=projects/*/databases/*}/documents:executePipeline` Executes a pipeline query.                                                                    |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/get)                                 | `GET /v1beta1/{name=projects/*/databases/*/documents/*/**}` Gets a single document.                                                                                       |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/list)                               | `GET /v1beta1/{parent=projects/*/databases/*/documents/*/**}/{collectionId}` Lists documents.                                                                             |
| [`listCollectionIds`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/listCollectionIds)     | `POST /v1beta1/{parent=projects/*/databases/*/documents}:listCollectionIds` Lists all the collection IDs underneath a document.                                           |
| [`listDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/listDocuments)             | `GET /v1beta1/{parent=projects/*/databases/*/documents}/{collectionId}` Lists documents.                                                                                  |
| [`listen`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/listen)                           | `POST /v1beta1/{database=projects/*/databases/*}/documents:listen` Listens to changes.                                                                                    |
| [`partitionQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/partitionQuery)           | `POST /v1beta1/{parent=projects/*/databases/*/documents}:partitionQuery` Partitions a query by returning partition cursors that can be used to run the query in parallel. |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/patch)                             | `PATCH /v1beta1/{document.name=projects/*/databases/*/documents/*/**}` Updates or inserts a document.                                                                     |
| [`rollback`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/rollback)                       | `POST /v1beta1/{database=projects/*/databases/*}/documents:rollback` Rolls back a transaction.                                                                            |
| [`runAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/runAggregationQuery) | `POST /v1beta1/{parent=projects/*/databases/*/documents}:runAggregationQuery` Runs an aggregation query.                                                                  |
| [`runQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/runQuery)                       | `POST /v1beta1/{parent=projects/*/databases/*/documents}:runQuery` Runs a query.                                                                                          |
| [`write`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.documents/write)                             | `POST /v1beta1/{database=projects/*/databases/*}/documents:write` Streams batches of document updates and deletes, in order.                                              |

## REST Resource: [v1beta1.projects.databases.indexes](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes)

| Methods                                                                                                           |                                                                                                            |
|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/create) | `POST /v1beta1/{parent=projects/*/databases/*}/indexes` Creates the specified index.                       |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/delete) | `DELETE /v1beta1/{name=projects/*/databases/*/indexes/*}` Deletes an index.                                |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/get)       | `GET /v1beta1/{name=projects/*/databases/*/indexes/*}` Gets an index.                                      |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1beta1/projects.databases.indexes/list)     | `GET /v1beta1/{parent=projects/*/databases/*}/indexes` Lists the indexes that match the specified filters. |

## REST Resource: [v1.projects.databases](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases)

| Methods                                                                                                                        |                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`bulkDeleteDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/bulkDeleteDocuments) | `POST /v1/{name=projects/*/databases/*}:bulkDeleteDocuments` Bulk deletes a subset of documents from Google Cloud Firestore.                                                                 |
| [`clone`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/clone)                             | `POST /v1/{parent=projects/*}/databases:clone` Creates a new database by cloning an existing one.                                                                                            |
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/create)                           | `POST /v1/{parent=projects/*}/databases` Create a database.                                                                                                                                  |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/delete)                           | `DELETE /v1/{name=projects/*/databases/*}` Deletes a database.                                                                                                                               |
| [`exportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/exportDocuments)         | `POST /v1/{name=projects/*/databases/*}:exportDocuments` Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/get)                                 | `GET /v1/{name=projects/*/databases/*}` Gets information about a database.                                                                                                                   |
| [`importDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/importDocuments)         | `POST /v1/{name=projects/*/databases/*}:importDocuments` Imports documents into Google Cloud Firestore.                                                                                      |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/list)                               | `GET /v1/{parent=projects/*}/databases` List all the databases in the project.                                                                                                               |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/patch)                             | `PATCH /v1/{database.name=projects/*/databases/*}` Updates a database.                                                                                                                       |
| [`restore`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases/restore)                         | `POST /v1/{parent=projects/*}/databases:restore` Creates a new database by restoring from an existing backup.                                                                                |

## REST Resource: [v1.projects.databases.backupSchedules](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules)

| Methods                                                                                                              |                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/create) | `POST /v1/{parent=projects/*/databases/*}/backupSchedules` Creates a backup schedule on a database.   |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/delete) | `DELETE /v1/{name=projects/*/databases/*/backupSchedules/*}` Deletes a backup schedule.               |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/get)       | `GET /v1/{name=projects/*/databases/*/backupSchedules/*}` Gets information about a backup schedule.   |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/list)     | `GET /v1/{parent=projects/*/databases/*}/backupSchedules` List backup schedules.                      |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/patch)   | `PATCH /v1/{backupSchedule.name=projects/*/databases/*/backupSchedules/*}` Updates a backup schedule. |

## REST Resource: [v1.projects.databases.collectionGroups.fields](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields)

| Methods                                                                                                                    |                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/get)     | `GET /v1/{name=projects/*/databases/*/collectionGroups/*/fields/*}` Gets the metadata and configuration for a Field.              |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/list)   | `GET /v1/{parent=projects/*/databases/*/collectionGroups/*}/fields` Lists the field configuration and metadata for this database. |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.fields/patch) | `PATCH /v1/{field.name=projects/*/databases/*/collectionGroups/*/fields/*}` Updates a field configuration.                        |

## REST Resource: [v1.projects.databases.collectionGroups.indexes](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.indexes)

| Methods                                                                                                                       |                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.indexes/delete) | `DELETE /v1/{name=projects/*/databases/*/collectionGroups/*/indexes/*}` Deletes a composite index. |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.indexes/get)       | `GET /v1/{name=projects/*/databases/*/collectionGroups/*/indexes/*}` Gets a composite index.       |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.collectionGroups.indexes/list)     | `GET /v1/{parent=projects/*/databases/*/collectionGroups/*}/indexes` Lists composite indexes.      |

## REST Resource: [v1.projects.databases.documents](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents)

| Methods                                                                                                                                  |                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`batchGet`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchGet)                       | `POST /v1/{database=projects/*/databases/*}/documents:batchGet` Gets multiple documents.                                                                             |
| [`batchWrite`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/batchWrite)                   | `POST /v1/{database=projects/*/databases/*}/documents:batchWrite` Applies a batch of write operations.                                                               |
| [`beginTransaction`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/beginTransaction)       | `POST /v1/{database=projects/*/databases/*}/documents:beginTransaction` Starts a new transaction.                                                                    |
| [`commit`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/commit)                           | `POST /v1/{database=projects/*/databases/*}/documents:commit` Commits a transaction, while optionally updating documents.                                            |
| [`createDocument`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/createDocument)           | `POST /v1/{parent=projects/*/databases/*/documents/**}/{collectionId}` Creates a new document.                                                                       |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/delete)                           | `DELETE /v1/{name=projects/*/databases/*/documents/*/**}` Deletes a document.                                                                                        |
| [`executePipeline`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/executePipeline)         | `POST /v1/{database=projects/*/databases/*}/documents:executePipeline` Executes a pipeline query.                                                                    |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/get)                                 | `GET /v1/{name=projects/*/databases/*/documents/*/**}` Gets a single document.                                                                                       |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/list)                               | `GET /v1/{parent=projects/*/databases/*/documents/*/**}/{collectionId}` Lists documents.                                                                             |
| [`listCollectionIds`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/listCollectionIds)     | `POST /v1/{parent=projects/*/databases/*/documents}:listCollectionIds` Lists all the collection IDs underneath a document.                                           |
| [`listDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/listDocuments)             | `GET /v1/{parent=projects/*/databases/*/documents}/{collectionId}` Lists documents.                                                                                  |
| [`listen`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/listen)                           | `POST /v1/{database=projects/*/databases/*}/documents:listen` Listens to changes.                                                                                    |
| [`partitionQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/partitionQuery)           | `POST /v1/{parent=projects/*/databases/*/documents}:partitionQuery` Partitions a query by returning partition cursors that can be used to run the query in parallel. |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/patch)                             | `PATCH /v1/{document.name=projects/*/databases/*/documents/*/**}` Updates or inserts a document.                                                                     |
| [`rollback`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/rollback)                       | `POST /v1/{database=projects/*/databases/*}/documents:rollback` Rolls back a transaction.                                                                            |
| [`runAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/runAggregationQuery) | `POST /v1/{parent=projects/*/databases/*/documents}:runAggregationQuery` Runs an aggregation query.                                                                  |
| [`runQuery`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/runQuery)                       | `POST /v1/{parent=projects/*/databases/*/documents}:runQuery` Runs a query.                                                                                          |
| [`write`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/write)                             | `POST /v1/{database=projects/*/databases/*}/documents:write` Streams batches of document updates and deletes, in order.                                              |

## REST Resource: [v1.projects.databases.operations](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.operations)

| Methods                                                                                                         |                                                                                                                            |
|-----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| [`cancel`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.operations/cancel) | `POST /v1/{name=projects/*/databases/*/operations/*}:cancel` Starts asynchronous cancellation on a long-running operation. |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.operations/delete) | `DELETE /v1/{name=projects/*/databases/*/operations/*}` Deletes a long-running operation.                                  |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.operations/get)       | `GET /v1/{name=projects/*/databases/*/operations/*}` Gets the latest state of a long-running operation.                    |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.operations/list)     | `GET /v1/{name=projects/*/databases/*}/operations` Lists operations that match the specified filter in the request.        |

## REST Resource: [v1.projects.databases.userCreds](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds)

| Methods                                                                                                                      |                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/create)               | `POST /v1/{parent=projects/*/databases/*}/userCreds` Create a user creds.                               |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/delete)               | `DELETE /v1/{name=projects/*/databases/*/userCreds/*}` Deletes a user creds.                            |
| [`disable`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/disable)             | `POST /v1/{name=projects/*/databases/*/userCreds/*}:disable` Disables a user creds.                     |
| [`enable`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/enable)               | `POST /v1/{name=projects/*/databases/*/userCreds/*}:enable` Enables a user creds.                       |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/get)                     | `GET /v1/{name=projects/*/databases/*/userCreds/*}` Gets a user creds resource.                         |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/list)                   | `GET /v1/{parent=projects/*/databases/*}/userCreds` List all user creds in the database.                |
| [`resetPassword`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.userCreds/resetPassword) | `POST /v1/{name=projects/*/databases/*/userCreds/*}:resetPassword` Resets the password of a user creds. |

## REST Resource: [v1.projects.locations](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations)

| Methods                                                                                          |                                                                                                         |
|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/get)   | `GET /v1/{name=projects/*/locations/*}` Gets information about a location.                              |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/list) | `GET /v1/{name=projects/*}/locations` Lists information about the supported locations for this service. |

## REST Resource: [v1.projects.locations.backups](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups)

| Methods                                                                                                      |                                                                                    |
|--------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/delete) | `DELETE /v1/{name=projects/*/locations/*/backups/*}` Deletes a backup.             |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/get)       | `GET /v1/{name=projects/*/locations/*/backups/*}` Gets information about a backup. |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations.backups/list)     | `GET /v1/{parent=projects/*/locations/*}/backups` Lists all the backups.           |
