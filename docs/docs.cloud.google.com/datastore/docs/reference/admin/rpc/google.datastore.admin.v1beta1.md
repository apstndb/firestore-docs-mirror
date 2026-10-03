---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1
title: Package google.datastore.admin.v1beta1
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

## Index

- [`DatastoreAdmin`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin) (interface)
- [`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.CommonMetadata) (message)
- [`CommonMetadata.State`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.CommonMetadata.State) (enum)
- [`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.EntityFilter) (message)
- [`ExportEntitiesMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesMetadata) (message)
- [`ExportEntitiesRequest`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesRequest) (message)
- [`ExportEntitiesResponse`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesResponse) (message)
- [`ImportEntitiesMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ImportEntitiesMetadata) (message)
- [`ImportEntitiesRequest`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ImportEntitiesRequest) (message)
- [`OperationType`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.OperationType) (enum)
- [`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.Progress) (message)

## DatastoreAdmin

Google Cloud Datastore Admin API

The Datastore Admin API provides several admin services for Cloud Datastore.

Concepts: Project, namespace, kind, and entity as defined in the Google Cloud Datastore API.

Operation: An Operation represents work being performed in the background.

EntityFilter: Allows specifying a subset of entities in a project. This is specified as a combination of kinds and namespaces (either or both of which may be all).

Export/Import Service:

- The Export/Import service provides the ability to copy all or a subset of entities to/from Google Cloud Storage.
- Exported data may be imported into Cloud Datastore for any Google Cloud Platform project. It is not restricted to the export source project. It is possible to export from one project and then import into another.
- Exported data can also be loaded into Google BigQuery for analysis.
- Exports and imports are performed asynchronously. An Operation resource is created for each export/import. The state (including any errors encountered) of the export/import may be queried via the Operation resource.

Operation Service:

- The Operations collection provides a record of actions performed for the specified project (including any operations in progress). Operations are not created directly but through calls on other collections or resources.
- An operation that is not yet done may be cancelled. The request to cancel is asynchronous and the operation may continue to run for some time after the request to cancel is made.
- An operation that is done may be deleted so that it is no longer listed as part of the Operation collection.
- ListOperations returns all pending operations, but not completed operations.
- Operations are created by service DatastoreAdmin, but are accessed via service google.longrunning.Operations.

**ExportEntities**

`rpc ExportEntities( `[`ExportEntitiesRequest`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operation)` )`

Exports a copy of all or a subset of entities from Google Cloud Datastore to another storage system, such as Google Cloud Storage. Recent updates to entities may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ImportEntities**

`rpc ImportEntities( `[`ImportEntitiesRequest`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ImportEntitiesRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operation)` )`

Imports entities into Google Cloud Datastore. Existing entities with the same key are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an ImportEntities operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Datastore.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## CommonMetadata

Metadata common to all Datastore Admin operations.

| Fields           |                                                                                                                                                                                                                                              |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time that work began on the operation.                                                                                                                 |
| `end_time`       | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the operation ended, either successfully or otherwise.                                                                                            |
| `operation_type` | [`OperationType`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.OperationType) The type of the operation. Can be used as a filter in ListOperationsRequest. |
| `labels`         | `map<string, string>` The client-assigned labels which were provided when the operation was created. May also include additional labels.                                                                                                     |
| `state`          | [`State`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.CommonMetadata.State) The current state of the Operation.                                           |

## State

The various possible states for an ongoing Operation.

| Enums               |                                                                                                                                |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                   |
| `INITIALIZING`      | Request is being prepared for processing.                                                                                      |
| `PROCESSING`        | Request is actively being processed.                                                                                           |
| `CANCELLING`        | Request is in the process of being cancelled after user called google.longrunning.Operations.CancelOperation on the operation. |
| `FINALIZING`        | Request has been processed and is in its finalization stage.                                                                   |
| `SUCCESSFUL`        | Request has completed successfully.                                                                                            |
| `FAILED`            | Request has finished being processed, but encountered an error.                                                                |
| `CANCELLED`         | Request has finished being cancelled after user called google.longrunning.Operations.CancelOperation.                          |

## EntityFilter

Identifies a subset of entities in a project. This is specified as combinations of kinds and namespaces (either or both of which may be all, as described in the following examples). Example usage:

Entire project: kinds=\[\], namespace_ids=\[\]

Kinds Foo and Bar in all namespaces: kinds=\['Foo', 'Bar'\], namespace_ids=\[\]

Kinds Foo and Bar only in the default namespace: kinds=\['Foo', 'Bar'\], namespace_ids=\[''\]

Kinds Foo and Bar in both the default and Baz namespaces: kinds=\['Foo', 'Bar'\], namespace_ids=\['', 'Baz'\]

The entire Baz namespace: kinds=\[\], namespace_ids=\['Baz'\]

| Fields            |                                                                                                                                                                                                                                                                                                                                      |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kinds[]`         | `string` If empty, then this represents all kinds.                                                                                                                                                                                                                                                                                   |
| `namespace_ids[]` | `string` An empty list represents all namespaces. This is the preferred usage for projects that don't use namespaces. An empty string element represents the default namespace. This should be used if the project has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique. |

## ExportEntitiesMetadata

Metadata for ExportEntities operations.

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `common`            | [`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.CommonMetadata) Metadata common to all Datastore Admin operations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `progress_entities` | [`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.Progress) An estimate of the number of entities processed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `progress_bytes`    | [`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.Progress) An estimate of the number of bytes processed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `entity_filter`     | [`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.EntityFilter) Description of which entities are being exported.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `output_url_prefix` | `string` Location for the export metadata and data files. This will be the same value as the [`google.datastore.admin.v1beta1.ExportEntitiesRequest.output_url_prefix`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesRequest.FIELDS.string.google.datastore.admin.v1beta1.ExportEntitiesRequest.output_url_prefix) field. The final output location is provided in [`google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesResponse.FIELDS.string.google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url) . |

## ExportEntitiesRequest

The request for [`google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities) .

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`        | `string` Project ID against which to make the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `labels`            | `map<string, string>` Client-assigned labels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `entity_filter`     | [`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.EntityFilter) Description of what data from the project is included in the export.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `output_url_prefix` | `string` Location for the export metadata and data files. The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So output_url_prefix should be of the form: `gs://BUCKET_NAME[/NAMESPACE_PATH]` , where `BUCKET_NAME` is the name of the Cloud Storage bucket and `NAMESPACE_PATH` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace). For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) . The resulting files will be nested deeper than the specified URL prefix. The final output URL will be provided in the [`google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesResponse.FIELDS.string.google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url) field. That value should be used for subsequent ImportEntities operations. By nesting the data files deeper, the same Cloud Storage bucket can be used in multiple ExportEntities operations without conflict. |

## ExportEntitiesResponse

The response for [`google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities) .

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `output_url` | `string` Location of the output metadata file. This can be used to begin an import into Cloud Datastore (this project or another project). See [`google.datastore.admin.v1beta1.ImportEntitiesRequest.input_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ImportEntitiesRequest.FIELDS.string.google.datastore.admin.v1beta1.ImportEntitiesRequest.input_url) . Only present if the operation completed successfully. |

## ImportEntitiesMetadata

Metadata for ImportEntities operations.

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `common`            | [`CommonMetadata`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.CommonMetadata) Metadata common to all Datastore Admin operations.                                                                                                                                                                                    |
| `progress_entities` | [`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.Progress) An estimate of the number of entities processed.                                                                                                                                                                                                  |
| `progress_bytes`    | [`Progress`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.Progress) An estimate of the number of bytes processed.                                                                                                                                                                                                     |
| `entity_filter`     | [`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.EntityFilter) Description of which entities are being imported.                                                                                                                                                                                         |
| `input_url`         | `string` The location of the import metadata file. This will be the same value as the [`google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesResponse.FIELDS.string.google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url) field. |

## ImportEntitiesRequest

The request for [`google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities) .

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `project_id`    | `string` Project ID against which to make the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `labels`        | `map<string, string>` Client-assigned labels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `input_url`     | `string` The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So input_url should be of the form: `gs://BUCKET_NAME[/NAMESPACE_PATH]/OVERALL_EXPORT_METADATA_FILE` , where `BUCKET_NAME` is the name of the Cloud Storage bucket, `NAMESPACE_PATH` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace), and `OVERALL_EXPORT_METADATA_FILE` is the metadata file written by the ExportEntities operation. For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) . For more information, see [`google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.ExportEntitiesResponse.FIELDS.string.google.datastore.admin.v1beta1.ExportEntitiesResponse.output_url) . |
| `entity_filter` | [`EntityFilter`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.EntityFilter) Optionally specify which kinds/namespaces are to be imported. If provided, the list must be a subset of the EntityFilter used in creating the export, otherwise a FAILED_PRECONDITION error will be returned. If no filter is specified then all entities from the export are imported.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## OperationType

Operation types.

| Enums                        |                 |
|------------------------------|-----------------|
| `OPERATION_TYPE_UNSPECIFIED` | Unspecified.    |
| `EXPORT_ENTITIES`            | ExportEntities. |
| `IMPORT_ENTITIES`            | ImportEntities. |

## Progress

Measures the progress of a particular metric.

| Fields           |                                                                                                              |
|------------------|--------------------------------------------------------------------------------------------------------------|
| `work_completed` | `int64` The amount of work that has been completed. Note that this may be greater than work_estimated.       |
| `work_estimated` | `int64` An estimate of how much work needs to be performed. May be zero if the work estimate is unavailable. |
