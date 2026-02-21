## Index

  - `  DatastoreAdmin  ` (interface)
  - `  CommonMetadata  ` (message)
  - `  CommonMetadata.State  ` (enum)
  - `  CreateIndexRequest  ` (message)
  - `  DatastoreFirestoreMigrationMetadata  ` (message)
  - `  DeleteIndexRequest  ` (message)
  - `  EntityFilter  ` (message)
  - `  ExportEntitiesMetadata  ` (message)
  - `  ExportEntitiesRequest  ` (message)
  - `  ExportEntitiesResponse  ` (message)
  - `  GetIndexRequest  ` (message)
  - `  ImportEntitiesMetadata  ` (message)
  - `  ImportEntitiesRequest  ` (message)
  - `  Index  ` (message)
  - `  Index.AncestorMode  ` (enum)
  - `  Index.Direction  ` (enum)
  - `  Index.IndexedProperty  ` (message)
  - `  Index.State  ` (enum)
  - `  IndexOperationMetadata  ` (message)
  - `  ListIndexesRequest  ` (message)
  - `  ListIndexesResponse  ` (message)
  - `  MigrationProgressEvent  ` (message)
  - `  MigrationProgressEvent.ConcurrencyMode  ` (enum)
  - `  MigrationProgressEvent.PrepareStepDetails  ` (message)
  - `  MigrationProgressEvent.RedirectWritesStepDetails  ` (message)
  - `  MigrationState  ` (enum)
  - `  MigrationStateEvent  ` (message)
  - `  MigrationStep  ` (enum)
  - `  OperationType  ` (enum)
  - `  Progress  ` (message)

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

Index Service:

  - The index service manages Cloud Datastore composite indexes.
  - Index creation and deletion are performed asynchronously. An Operation resource is created for each such asynchronous operation. The state of the operation (including any errors encountered) may be queried via the Operation resource.

Operation Service:

  - The Operations collection provides a record of actions performed for the specified project (including any operations in progress). Operations are not created directly but through calls on other collections or resources.
  - An operation that is not yet done may be cancelled. The request to cancel is asynchronous and the operation may continue to run for some time after the request to cancel is made.
  - An operation that is done may be deleted so that it is no longer listed as part of the Operation collection.
  - ListOperations returns all pending operations, but not completed operations.
  - Operations are created by service DatastoreAdmin, but are accessed via service google.longrunning.Operations.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateIndex</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateIndex(                         CreateIndexRequest            </code> ) returns ( <code dir="ltr" translate="no">              Operation            </code> )</p>
<p>Creates the specified index. A newly created index's initial state is <code dir="ltr" translate="no">           CREATING          </code> . On completion of the returned <code dir="ltr" translate="no">             google.longrunning.Operation           </code> , the state will be <code dir="ltr" translate="no">           READY          </code> . If the index already exists, the call will return an <code dir="ltr" translate="no">           ALREADY_EXISTS          </code> status.</p>
<p>During index creation, the process could result in an error, in which case the index will move to the <code dir="ltr" translate="no">           ERROR          </code> state. The process can be recovered by fixing the data that caused the error, removing the index with <code dir="ltr" translate="no">             delete           </code> , then re-creating the index with <code dir="ltr" translate="no">             create           </code> .</p>
<p>Indexes with a single property cannot be created.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteIndex</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteIndex(                         DeleteIndexRequest            </code> ) returns ( <code dir="ltr" translate="no">              Operation            </code> )</p>
<p>Deletes an existing index. An index can only be deleted if it is in a <code dir="ltr" translate="no">           READY          </code> or <code dir="ltr" translate="no">           ERROR          </code> state. On successful execution of the request, the index will be in a <code dir="ltr" translate="no">           DELETING          </code> <code dir="ltr" translate="no">             state           </code> . And on completion of the returned <code dir="ltr" translate="no">             google.longrunning.Operation           </code> , the index will be removed.</p>
<p>During index deletion, the process could result in an error, in which case the index will move to the <code dir="ltr" translate="no">           ERROR          </code> state. The process can be recovered by fixing the data that caused the error, followed by calling <code dir="ltr" translate="no">             delete           </code> again.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ExportEntities</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ExportEntities(                         ExportEntitiesRequest            </code> ) returns ( <code dir="ltr" translate="no">              Operation            </code> )</p>
<p>Exports a copy of all or a subset of entities from Google Cloud Datastore to another storage system, such as Google Cloud Storage. Recent updates to entities may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetIndex</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetIndex(                         GetIndexRequest            </code> ) returns ( <code dir="ltr" translate="no">              Index            </code> )</p>
<p>Gets an index.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ImportEntities</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ImportEntities(                         ImportEntitiesRequest            </code> ) returns ( <code dir="ltr" translate="no">              Operation            </code> )</p>
<p>Imports entities into Google Cloud Datastore. Existing entities with the same key are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an ImportEntities operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Datastore.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListIndexes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListIndexes(                         ListIndexesRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListIndexesResponse            </code> )</p>
<p>Lists the indexes that match the specified filters. Datastore uses an eventually consistent query to fetch the list of indexes and may occasionally return stale results.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## CommonMetadata

Metadata common to all Datastore Admin operations.

Fields

`  start_time  `

`  Timestamp  `

The time that work began on the operation.

`  end_time  `

`  Timestamp  `

The time the operation ended, either successfully or otherwise.

`  operation_type  `

`  OperationType  `

The type of the operation. Can be used as a filter in ListOperationsRequest.

`  labels  `

`  map<string, string>  `

The client-assigned labels which were provided when the operation was created. May also include additional labels.

`  state  `

`  State  `

The current state of the Operation.

## State

The various possible states for an ongoing Operation.

Enums

`  STATE_UNSPECIFIED  `

Unspecified.

`  INITIALIZING  `

Request is being prepared for processing.

`  PROCESSING  `

Request is actively being processed.

`  CANCELLING  `

Request is in the process of being cancelled after user called google.longrunning.Operations.CancelOperation on the operation.

`  FINALIZING  `

Request has been processed and is in its finalization stage.

`  SUCCESSFUL  `

Request has completed successfully.

`  FAILED  `

Request has finished being processed, but encountered an error.

`  CANCELLED  `

Request has finished being cancelled after user called google.longrunning.Operations.CancelOperation.

## CreateIndexRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.CreateIndex  ` .

Fields

`  project_id  `

`  string  `

Project ID against which to make the request.

`  index  `

`  Index  `

The index to create. The name and state fields are output only and will be ignored. Single property indexes cannot be created or deleted.

## DatastoreFirestoreMigrationMetadata

Metadata for Datastore to Firestore migration operations.

The DatastoreFirestoreMigration operation is not started by the end-user via an explicit "creation" method. This is an intentional deviation from the LRO design pattern.

This singleton resource can be accessed at: "projects/{project\_id}/operations/datastore-firestore-migration"

Fields

`  migration_state  `

`  MigrationState  `

The current state of migration from Cloud Datastore to Cloud Firestore in Datastore mode.

`  migration_step  `

`  MigrationStep  `

The current step of migration from Cloud Datastore to Cloud Firestore in Datastore mode.

## DeleteIndexRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.DeleteIndex  ` .

Fields

`  project_id  `

`  string  `

Project ID against which to make the request.

`  index_id  `

`  string  `

The resource ID of the index to delete.

## EntityFilter

Identifies a subset of entities in a project. This is specified as combinations of kinds and namespaces (either or both of which may be all, as described in the following examples). Example usage:

Entire project: kinds=\[\], namespace\_ids=\[\]

Kinds Foo and Bar in all namespaces: kinds=\['Foo', 'Bar'\], namespace\_ids=\[\]

Kinds Foo and Bar only in the default namespace: kinds=\['Foo', 'Bar'\], namespace\_ids=\[''\]

Kinds Foo and Bar in both the default and Baz namespaces: kinds=\['Foo', 'Bar'\], namespace\_ids=\['', 'Baz'\]

The entire Baz namespace: kinds=\[\], namespace\_ids=\['Baz'\]

Fields

`  kinds[]  `

`  string  `

If empty, then this represents all kinds.

`  namespace_ids[]  `

`  string  `

An empty list represents all namespaces. This is the preferred usage for projects that don't use namespaces.

An empty string element represents the default namespace. This should be used if the project has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique.

## ExportEntitiesMetadata

Metadata for ExportEntities operations.

Fields

`  common  `

`  CommonMetadata  `

Metadata common to all Datastore Admin operations.

`  progress_entities  `

`  Progress  `

An estimate of the number of entities processed.

`  progress_bytes  `

`  Progress  `

An estimate of the number of bytes processed.

`  entity_filter  `

`  EntityFilter  `

Description of which entities are being exported.

`  output_url_prefix  `

`  string  `

Location for the export metadata and data files. This will be the same value as the `  google.datastore.admin.v1.ExportEntitiesRequest.output_url_prefix  ` field. The final output location is provided in `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` .

## ExportEntitiesRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.ExportEntities  ` .

Fields

`  project_id  `

`  string  `

Required. Project ID against which to make the request.

`  labels  `

`  map<string, string>  `

Client-assigned labels.

`  entity_filter  `

`  EntityFilter  `

Description of what data from the project is included in the export.

`  output_url_prefix  `

`  string  `

Required. Location for the export metadata and data files.

The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So output\_url\_prefix should be of the form: `  gs://BUCKET_NAME[/NAMESPACE_PATH]  ` , where `  BUCKET_NAME  ` is the name of the Cloud Storage bucket and `  NAMESPACE_PATH  ` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace). For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) .

The resulting files will be nested deeper than the specified URL prefix. The final output URL will be provided in the `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` field. That value should be used for subsequent ImportEntities operations.

By nesting the data files deeper, the same Cloud Storage bucket can be used in multiple ExportEntities operations without conflict.

## ExportEntitiesResponse

The response for `  google.datastore.admin.v1.DatastoreAdmin.ExportEntities  ` .

Fields

`  output_url  `

`  string  `

Location of the output metadata file. This can be used to begin an import into Cloud Datastore (this project or another project). See `  google.datastore.admin.v1.ImportEntitiesRequest.input_url  ` . Only present if the operation completed successfully.

## GetIndexRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.GetIndex  ` .

Fields

`  project_id  `

`  string  `

Project ID against which to make the request.

`  index_id  `

`  string  `

The resource ID of the index to get.

## ImportEntitiesMetadata

Metadata for ImportEntities operations.

Fields

`  common  `

`  CommonMetadata  `

Metadata common to all Datastore Admin operations.

`  progress_entities  `

`  Progress  `

An estimate of the number of entities processed.

`  progress_bytes  `

`  Progress  `

An estimate of the number of bytes processed.

`  entity_filter  `

`  EntityFilter  `

Description of which entities are being imported.

`  input_url  `

`  string  `

The location of the import metadata file. This will be the same value as the `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` field.

## ImportEntitiesRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.ImportEntities  ` .

Fields

`  project_id  `

`  string  `

Required. Project ID against which to make the request.

`  labels  `

`  map<string, string>  `

Client-assigned labels.

`  input_url  `

`  string  `

Required. The full resource URL of the external storage location. Currently, only Google Cloud Storage is supported. So input\_url should be of the form: `  gs://BUCKET_NAME[/NAMESPACE_PATH]/OVERALL_EXPORT_METADATA_FILE  ` , where `  BUCKET_NAME  ` is the name of the Cloud Storage bucket, `  NAMESPACE_PATH  ` is an optional Cloud Storage namespace path (this is not a Cloud Datastore namespace), and `  OVERALL_EXPORT_METADATA_FILE  ` is the metadata file written by the ExportEntities operation. For more information about Cloud Storage namespace paths, see [Object name considerations](https://cloud.google.com/storage/docs/naming#object-considerations) .

For more information, see `  google.datastore.admin.v1.ExportEntitiesResponse.output_url  ` .

`  entity_filter  `

`  EntityFilter  `

Optionally specify which kinds/namespaces are to be imported. If provided, the list must be a subset of the EntityFilter used in creating the export, otherwise a FAILED\_PRECONDITION error will be returned. If no filter is specified then all entities from the export are imported.

## Index

Datastore composite index definition.

Fields

`  project_id  `

`  string  `

Output only. Project ID.

`  index_id  `

`  string  `

Output only. The resource ID of the index.

`  kind  `

`  string  `

Required. The entity kind to which this index applies.

`  ancestor  `

`  AncestorMode  `

Required. The index's ancestor mode. Must not be ANCESTOR\_MODE\_UNSPECIFIED.

`  properties[]  `

`  IndexedProperty  `

Required. An ordered sequence of property names and their index attributes.

Requires:

  - A maximum of 100 properties.

`  state  `

`  State  `

Output only. The state of the index.

## AncestorMode

For an ordered index, specifies whether each of the entity's ancestors will be included.

Enums

`  ANCESTOR_MODE_UNSPECIFIED  `

The ancestor mode is unspecified.

`  NONE  `

Do not include the entity's ancestors in the index.

`  ALL_ANCESTORS  `

Include all the entity's ancestors in the index.

## Direction

The direction determines how a property is indexed.

Enums

`  DIRECTION_UNSPECIFIED  `

The direction is unspecified.

`  ASCENDING  `

The property's values are indexed so as to support sequencing in ascending order and also query by \<, \>, \<=, \>=, and =.

`  DESCENDING  `

The property's values are indexed so as to support sequencing in descending order and also query by \<, \>, \<=, \>=, and =.

## IndexedProperty

A property of an index.

Fields

`  name  `

`  string  `

Required. The property name to index.

`  direction  `

`  Direction  `

Required. The indexed property's direction. Must not be DIRECTION\_UNSPECIFIED.

## State

The possible set of states of an index.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  CREATING  `

The index is being created, and cannot be used by queries. There is an active long-running operation for the index. The index is updated when writing an entity. Some index data may exist.

`  READY  `

The index is ready to be used. The index is updated when writing an entity. The index is fully populated from all stored entities it applies to.

`  DELETING  `

The index is being deleted, and cannot be used by queries. There is an active long-running operation for the index. The index is not updated when writing an entity. Some index data may exist.

`  ERROR  `

The index was being created or deleted, but something went wrong. The index cannot by used by queries. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing an entity. Some index data may exist.

## IndexOperationMetadata

Metadata for Index operations.

Fields

`  common  `

`  CommonMetadata  `

Metadata common to all Datastore Admin operations.

`  progress_entities  `

`  Progress  `

An estimate of the number of entities processed.

`  index_id  `

`  string  `

The index resource ID that this operation is acting on.

## ListIndexesRequest

The request for `  google.datastore.admin.v1.DatastoreAdmin.ListIndexes  ` .

Fields

`  project_id  `

`  string  `

Project ID against which to make the request.

`  filter  `

`  string  `

`  page_size  `

`  int32  `

The maximum number of items to return. If zero, then all results will be returned.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## ListIndexesResponse

The response for `  google.datastore.admin.v1.DatastoreAdmin.ListIndexes  ` .

Fields

`  indexes[]  `

`  Index  `

The indexes.

`  next_page_token  `

`  string  `

The standard List next-page token.

## MigrationProgressEvent

An event signifying the start of a new step in a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

Fields

`  step  `

`  MigrationStep  `

The step that is starting.

An event with step set to `  START  ` indicates that the migration has been reverted back to the initial pre-migration state.

Union field `  step_details  ` . Details about this step. `  step_details  ` can be only one of the following:

`  prepare_step_details  `

`  PrepareStepDetails  `

Details for the `  PREPARE  ` step.

`  redirect_writes_step_details  `

`  RedirectWritesStepDetails  `

Details for the `  REDIRECT_WRITES  ` step.

## ConcurrencyMode

Concurrency modes for transactions in Cloud Firestore.

Enums

`  CONCURRENCY_MODE_UNSPECIFIED  `

Unspecified.

`  PESSIMISTIC  `

Pessimistic concurrency.

`  OPTIMISTIC  `

Optimistic concurrency.

`  OPTIMISTIC_WITH_ENTITY_GROUPS  `

Optimistic concurrency with entity groups.

## PrepareStepDetails

Details for the `  PREPARE  ` step.

Fields

`  concurrency_mode  `

`  ConcurrencyMode  `

The concurrency mode this database will use when it reaches the `  REDIRECT_WRITES  ` step.

## RedirectWritesStepDetails

Details for the `  REDIRECT_WRITES  ` step.

Fields

`  concurrency_mode  `

`  ConcurrencyMode  `

The concurrency mode for this database.

## MigrationState

States for a migration.

Enums

`  MIGRATION_STATE_UNSPECIFIED  `

Unspecified.

`  RUNNING  `

The migration is running.

`  PAUSED  `

The migration is paused.

`  COMPLETE  `

The migration is complete.

## MigrationStateEvent

An event signifying a change in state of a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

Fields

`  state  `

`  MigrationState  `

The new state of the migration.

## MigrationStep

Steps in a migration.

Enums

`  MIGRATION_STEP_UNSPECIFIED  `

Unspecified.

`  PREPARE  `

Pre-migration: the database is prepared for migration.

`  START  `

Start of migration.

`  APPLY_WRITES_SYNCHRONOUSLY  `

Writes are applied synchronously to at least one replica.

`  COPY_AND_VERIFY  `

Data is copied to Cloud Firestore and then verified to match the data in Cloud Datastore.

`  REDIRECT_EVENTUALLY_CONSISTENT_READS  `

Eventually-consistent reads are redirected to Cloud Firestore.

`  REDIRECT_STRONGLY_CONSISTENT_READS  `

Strongly-consistent reads are redirected to Cloud Firestore.

`  REDIRECT_WRITES  `

Writes are redirected to Cloud Firestore.

## OperationType

Operation types.

Enums

`  OPERATION_TYPE_UNSPECIFIED  `

Unspecified.

`  EXPORT_ENTITIES  `

ExportEntities.

`  IMPORT_ENTITIES  `

ImportEntities.

`  CREATE_INDEX  `

CreateIndex.

`  DELETE_INDEX  `

DeleteIndex.

## Progress

Measures the progress of a particular metric.

Fields

`  work_completed  `

`  int64  `

The amount of work that has been completed. Note that this may be greater than work\_estimated.

`  work_estimated  `

`  int64  `

An estimate of how much work needs to be performed. May be zero if the work estimate is unavailable.
