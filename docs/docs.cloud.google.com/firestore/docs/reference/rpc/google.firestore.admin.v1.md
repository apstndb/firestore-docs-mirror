---
name: documents/docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1
uri: https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1
title: Package google.firestore.admin.v1
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Index

- [`FirestoreAdmin`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin) (interface)
- [`Backup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup) (message)
- [`Backup.State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup.State) (enum)
- [`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule) (message)
- [`BulkDeleteDocumentsMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BulkDeleteDocumentsMetadata) (message)
- [`BulkDeleteDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BulkDeleteDocumentsRequest) (message)
- [`BulkDeleteDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BulkDeleteDocumentsResponse) (message)
- [`CloneDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CloneDatabaseMetadata) (message)
- [`CloneDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CloneDatabaseRequest) (message)
- [`CreateBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateBackupScheduleRequest) (message)
- [`CreateDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateDatabaseMetadata) (message)
- [`CreateDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateDatabaseRequest) (message)
- [`CreateIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateIndexRequest) (message)
- [`CreateUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateUserCredsRequest) (message)
- [`DailyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DailyRecurrence) (message)
- [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) (message)
- [`Database.AppEngineIntegrationMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.AppEngineIntegrationMode) (enum)
- [`Database.CmekConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.CmekConfig) (message)
- [`Database.ConcurrencyMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.ConcurrencyMode) (enum)
- [`Database.DataAccessMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DataAccessMode) (enum)
- [`Database.DatabaseEdition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DatabaseEdition) (enum)
- [`Database.DatabaseType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DatabaseType) (enum)
- [`Database.DeleteProtectionState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DeleteProtectionState) (enum)
- [`Database.EncryptionConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig) (message)
- [`Database.EncryptionConfig.CustomerManagedEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.CustomerManagedEncryptionOptions) (message)
- [`Database.EncryptionConfig.GoogleDefaultEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.GoogleDefaultEncryptionOptions) (message)
- [`Database.EncryptionConfig.SourceEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.SourceEncryptionOptions) (message)
- [`Database.PointInTimeRecoveryEnablement`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.PointInTimeRecoveryEnablement) (enum)
- [`Database.SourceInfo`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.SourceInfo) (message)
- [`Database.SourceInfo.BackupSource`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.SourceInfo.BackupSource) (message)
- [`DeleteBackupRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteBackupRequest) (message)
- [`DeleteBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteBackupScheduleRequest) (message)
- [`DeleteDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteDatabaseMetadata) (message)
- [`DeleteDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteDatabaseRequest) (message)
- [`DeleteIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteIndexRequest) (message)
- [`DeleteUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteUserCredsRequest) (message)
- [`DisableUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DisableUserCredsRequest) (message)
- [`EnableUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.EnableUserCredsRequest) (message)
- [`ExportDocumentsMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ExportDocumentsMetadata) (message)
- [`ExportDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ExportDocumentsRequest) (message)
- [`ExportDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ExportDocumentsResponse) (message)
- [`Field`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field) (message)
- [`Field.IndexConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.IndexConfig) (message)
- [`Field.TtlConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.TtlConfig) (message)
- [`Field.TtlConfig.State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.TtlConfig.State) (enum)
- [`FieldOperationMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata) (message)
- [`FieldOperationMetadata.IndexConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.IndexConfigDelta) (message)
- [`FieldOperationMetadata.IndexConfigDelta.ChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.IndexConfigDelta.ChangeType) (enum)
- [`FieldOperationMetadata.TtlConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.TtlConfigDelta) (message)
- [`FieldOperationMetadata.TtlConfigDelta.ChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.TtlConfigDelta.ChangeType) (enum)
- [`GetBackupRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetBackupRequest) (message)
- [`GetBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetBackupScheduleRequest) (message)
- [`GetDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetDatabaseRequest) (message)
- [`GetFieldRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetFieldRequest) (message)
- [`GetIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetIndexRequest) (message)
- [`GetUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetUserCredsRequest) (message)
- [`ImportDocumentsMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ImportDocumentsMetadata) (message)
- [`ImportDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ImportDocumentsRequest) (message)
- [`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index) (message)
- [`Index.ApiScope`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.ApiScope) (enum)
- [`Index.Density`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.Density) (enum)
- [`Index.IndexField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField) (message)
- [`Index.IndexField.ArrayConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.ArrayConfig) (enum)
- [`Index.IndexField.Order`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.Order) (enum)
- [`Index.IndexField.SearchConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig) (message)
- [`Index.IndexField.SearchConfig.SearchGeoSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchGeoSpec) (message)
- [`Index.IndexField.SearchConfig.SearchTextIndexSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchTextIndexSpec) (message)
- [`Index.IndexField.SearchConfig.SearchTextSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchTextSpec) (message)
- [`Index.IndexField.SearchConfig.TextIndexType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.TextIndexType) (enum)
- [`Index.IndexField.SearchConfig.TextMatchType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.TextMatchType) (enum)
- [`Index.IndexField.VectorConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.VectorConfig) (message)
- [`Index.IndexField.VectorConfig.FlatIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.VectorConfig.FlatIndex) (message)
- [`Index.QueryScope`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.QueryScope) (enum)
- [`Index.SearchIndexOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.SearchIndexOptions) (message)
- [`Index.State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.State) (enum)
- [`IndexOperationMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.IndexOperationMetadata) (message)
- [`ListBackupSchedulesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupSchedulesRequest) (message)
- [`ListBackupSchedulesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupSchedulesResponse) (message)
- [`ListBackupsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupsRequest) (message)
- [`ListBackupsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupsResponse) (message)
- [`ListDatabasesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListDatabasesRequest) (message)
- [`ListDatabasesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListDatabasesResponse) (message)
- [`ListFieldsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListFieldsRequest) (message)
- [`ListFieldsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListFieldsResponse) (message)
- [`ListIndexesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListIndexesRequest) (message)
- [`ListIndexesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListIndexesResponse) (message)
- [`ListUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListUserCredsRequest) (message)
- [`ListUserCredsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListUserCredsResponse) (message)
- [`LocationMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.LocationMetadata) (message)
- [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) (enum)
- [`PitrSnapshot`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.PitrSnapshot) (message)
- [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) (message)
- [`RealtimeUpdatesMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RealtimeUpdatesMode) (enum)
- [`ResetUserPasswordRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ResetUserPasswordRequest) (message)
- [`RestoreDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RestoreDatabaseMetadata) (message)
- [`RestoreDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RestoreDatabaseRequest) (message)
- [`UpdateBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateBackupScheduleRequest) (message)
- [`UpdateDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateDatabaseMetadata) (message)
- [`UpdateDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateDatabaseRequest) (message)
- [`UpdateFieldRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateFieldRequest) (message)
- [`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds) (message)
- [`UserCreds.ResourceIdentity`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds.ResourceIdentity) (message)
- [`UserCreds.State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds.State) (enum)
- [`WeeklyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.WeeklyRecurrence) (message)

## FirestoreAdmin

The Cloud Firestore Admin API.

This API provides several administrative services for Cloud Firestore.

Project, Database, Namespace, Collection, Collection Group, and Document are used as defined in the Google Cloud Firestore API.

Operation: An Operation represents work being performed in the background.

The index service manages Cloud Firestore indexes.

Index creation is performed asynchronously. An Operation resource is created for each such asynchronous operation. The state of the operation (including any errors encountered) may be queried via the Operation resource.

The Operations collection provides a record of actions performed for the specified Project (including any Operations in progress). Operations are not created directly but through calls on other collections or resources.

An Operation that is done may be deleted so that it is no longer listed as part of the Operation collection. Operations are garbage collected after 30 days. By default, ListOperations will only return in progress and failed operations. To list completed operation, issue a ListOperations request with the filter `done: true` .

Operations are created by service `FirestoreAdmin` , but are accessed via service `google.longrunning.Operations` .

**BulkDeleteDocuments**

`rpc BulkDeleteDocuments( `[`BulkDeleteDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BulkDeleteDocumentsRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Bulk deletes a subset of documents from Google Cloud Firestore. Documents created or updated after the underlying system starts to process the request will not be deleted. The bulk delete occurs in the background and its progress can be monitored and managed via the Operation resource that is created.

For more details on bulk delete behavior, refer to: <https://cloud.google.com/firestore/docs/manage-data/bulk-delete>

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CloneDatabase**

`rpc CloneDatabase( `[`CloneDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CloneDatabaseRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new database by cloning an existing one.

The new database must be in the same cloud region or multi-region location as the existing database. This behaves similar to [`FirestoreAdmin.CreateDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateDatabase) except instead of creating a new empty database, a new database is created with the database type, index configuration, and documents from an existing database.

The [`long-running operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) can be used to track the progress of the clone, with the Operation's [`metadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation.FIELDS.google.protobuf.Any.google.longrunning.Operation.metadata) field type being the [`CloneDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CloneDatabaseMetadata) . The [`response`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation.FIELDS.google.protobuf.Any.google.longrunning.Operation.response) type is the [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) if the clone was successful. The new database is not readable or writeable until the LRO has completed.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateBackupSchedule**

`rpc CreateBackupSchedule( `[`CreateBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateBackupScheduleRequest)` ) returns ( `[`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule)` )`

Creates a backup schedule on a database. At most two backup schedules can be configured on a database, one daily backup schedule and one weekly backup schedule.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateDatabase**

`rpc CreateDatabase( `[`CreateDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateDatabaseRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Create a database.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateIndex**

`rpc CreateIndex( `[`CreateIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateIndexRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a composite index. This returns a [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) which may be used to track the status of the creation. The metadata for the operation will be the type [`IndexOperationMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.IndexOperationMetadata) .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateUserCreds**

`rpc CreateUserCreds( `[`CreateUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.CreateUserCredsRequest)` ) returns ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds)` )`

Create a user creds.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteBackup**

`rpc DeleteBackup( `[`DeleteBackupRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteBackupRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a backup.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteBackupSchedule**

`rpc DeleteBackupSchedule( `[`DeleteBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteBackupScheduleRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a backup schedule.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteDatabase**

`rpc DeleteDatabase( `[`DeleteDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteDatabaseRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes a database.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteIndex**

`rpc DeleteIndex( `[`DeleteIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteIndexRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a composite index.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteUserCreds**

`rpc DeleteUserCreds( `[`DeleteUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DeleteUserCredsRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a user creds.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DisableUserCreds**

`rpc DisableUserCreds( `[`DisableUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DisableUserCredsRequest)` ) returns ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds)` )`

Disables a user creds. No-op if the user creds are already disabled.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**EnableUserCreds**

`rpc EnableUserCreds( `[`EnableUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.EnableUserCredsRequest)` ) returns ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds)` )`

Enables a user creds. No-op if the user creds are already enabled.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ExportDocuments**

`rpc ExportDocuments( `[`ExportDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ExportDocumentsRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage. Recent updates to documents may not be reflected in the export. The export occurs in the background and its progress can be monitored and managed via the Operation resource that is created. The output of an export may only be used once the associated operation is done. If an export operation is cancelled before completion it may leave partial data behind in Google Cloud Storage.

For more details on export behavior and output format, refer to: <https://cloud.google.com/firestore/docs/manage-data/export-import>

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetBackup**

`rpc GetBackup( `[`GetBackupRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetBackupRequest)` ) returns ( `[`Backup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup)` )`

Gets information about a backup.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetBackupSchedule**

`rpc GetBackupSchedule( `[`GetBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetBackupScheduleRequest)` ) returns ( `[`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule)` )`

Gets information about a backup schedule.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetDatabase**

`rpc GetDatabase( `[`GetDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetDatabaseRequest)` ) returns ( `[`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database)` )`

Gets information about a database.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetField**

`rpc GetField( `[`GetFieldRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetFieldRequest)` ) returns ( `[`Field`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field)` )`

Gets the metadata and configuration for a Field.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetIndex**

`rpc GetIndex( `[`GetIndexRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetIndexRequest)` ) returns ( `[`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index)` )`

Gets a composite index.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetUserCreds**

`rpc GetUserCreds( `[`GetUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.GetUserCredsRequest)` ) returns ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds)` )`

Gets a user creds resource. Note that the returned resource does not contain the secret value itself.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ImportDocuments**

`rpc ImportDocuments( `[`ImportDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ImportDocumentsRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Imports documents into Google Cloud Firestore. Existing documents with the same name are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an ImportDocuments operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Firestore.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListBackupSchedules**

`rpc ListBackupSchedules( `[`ListBackupSchedulesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupSchedulesRequest)` ) returns ( `[`ListBackupSchedulesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupSchedulesResponse)` )`

List backup schedules.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListBackups**

`rpc ListBackups( `[`ListBackupsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupsRequest)` ) returns ( `[`ListBackupsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListBackupsResponse)` )`

Lists all the backups.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListDatabases**

`rpc ListDatabases( `[`ListDatabasesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListDatabasesRequest)` ) returns ( `[`ListDatabasesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListDatabasesResponse)` )`

List all the databases in the project.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListFields**

`rpc ListFields( `[`ListFieldsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListFieldsRequest)` ) returns ( `[`ListFieldsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListFieldsResponse)` )`

Lists the field configuration and metadata for this database.

Currently, [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) only supports listing fields that have been explicitly overridden. To issue this query, call [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) with the filter set to `indexConfig.usesAncestorConfig:false` or `ttlConfig:*` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListIndexes**

`rpc ListIndexes( `[`ListIndexesRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListIndexesRequest)` ) returns ( `[`ListIndexesResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListIndexesResponse)` )`

Lists composite indexes.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListUserCreds**

`rpc ListUserCreds( `[`ListUserCredsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListUserCredsRequest)` ) returns ( `[`ListUserCredsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ListUserCredsResponse)` )`

List all user creds in the database. Note that the returned resource does not contain the secret value itself.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ResetUserPassword**

`rpc ResetUserPassword( `[`ResetUserPasswordRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ResetUserPasswordRequest)` ) returns ( `[`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds)` )`

Resets the password of a user creds.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RestoreDatabase**

`rpc RestoreDatabase( `[`RestoreDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RestoreDatabaseRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new database by restoring from an existing backup.

The new database must be in the same cloud region or multi-region location as the existing backup. This behaves similar to [`FirestoreAdmin.CreateDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateDatabase) except instead of creating a new empty database, a new database is created with the database type, index configuration, and documents from an existing backup.

The [`long-running operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) can be used to track the progress of the restore, with the Operation's [`metadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation.FIELDS.google.protobuf.Any.google.longrunning.Operation.metadata) field type being the [`RestoreDatabaseMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RestoreDatabaseMetadata) . The [`response`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation.FIELDS.google.protobuf.Any.google.longrunning.Operation.response) type is the [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) if the restore was successful. The new database is not readable or writeable until the LRO has completed.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateBackupSchedule**

`rpc UpdateBackupSchedule( `[`UpdateBackupScheduleRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateBackupScheduleRequest)` ) returns ( `[`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule)` )`

Updates a backup schedule.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateDatabase**

`rpc UpdateDatabase( `[`UpdateDatabaseRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateDatabaseRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Updates a database.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateField**

`rpc UpdateField( `[`UpdateFieldRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UpdateFieldRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Updates a field configuration. Currently, field updates apply only to single field index configuration. However, calls to [`FirestoreAdmin.UpdateField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.UpdateField) should provide a field mask to avoid changing any configuration that the caller isn't aware of. The field mask should be specified as: `{ paths: "index_config" }` .

This call returns a [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) which may be used to track the status of the field update. The metadata for the operation will be the type [`FieldOperationMetadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata) .

To configure the default field settings for the database, use the special `Field` with resource name: `projects/{project_id}/databases/{database_id}/collectionGroups/__default__/fields/*` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Backup

A Backup of a Cloud Firestore Database.

The backup contains all documents and index configurations for the given database at a specific point in time.

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Output only. The unique resource name of the Backup. Format is `projects/{project}/locations/{location}/backups/{backup}` . The location in the name will be the Standard Managed Multi-Region (SMMR) location (e.g. `us` ) if the backup was created with an SMMR location, or the Google Managed Multi-Region (GMMR) location (e.g. `nam5` ) if the backup was created with a GMMR location. |
| `database`      | `string` Output only. Name of the Firestore database that the backup is from. Format is `projects/{project}/databases/{database}` .                                                                                                                                                                                                                                                                     |
| `database_uid`  | `string` Output only. The system-generated UUID4 for the Firestore database that the backup is from.                                                                                                                                                                                                                                                                                                    |
| `snapshot_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The backup contains an externally consistent copy of the database at this time.                                                                                                                                                                                                                          |
| `expire_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this backup expires.                                                                                                                                                                                                                                                              |
| `state`         | [`State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup.State) Output only. The current state of the backup.                                                                                                                                                                                                                    |

## State

Indicate the current state of the backup.

| Enums               |                                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                           |
| `CREATING`          | The pending backup is still being created. Operations on the backup will be rejected in this state. |
| `READY`             | The backup is complete and ready to use.                                                            |
| `NOT_AVAILABLE`     | The backup is not available at this moment.                                                         |

## BackupSchedule

A backup schedule for a Cloud Firestore Database.

This resource is owned by the database it is backing up, and is deleted along with the database. The actual backups are not though.

| Fields                                                                                                                           |                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                           | `string` Output only. The unique backup schedule identifier across all locations and databases for the given project. This will be auto-assigned. Format is `projects/{project}/databases/{database}/backupSchedules/{backup_schedule}`                             |
| `create_time`                                                                                                                    | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this backup schedule was created and effective since. No backups will be created for this schedule before this time.                          |
| `update_time`                                                                                                                    | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this backup schedule was most recently updated. When a backup schedule is first created, this is the same as create_time.                     |
| `retention`                                                                                                                      | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) At what relative time in the future, compared to its creation time, the backup should be deleted, e.g. keep backups for 7 days. The maximum supported retention period is 14 weeks. |
| Union field `recurrence` . A oneof field to represent when backups will be taken. `recurrence` can be only one of the following: |                                                                                                                                                                                                                                                                     |
| `daily_recurrence`                                                                                                               | [`DailyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.DailyRecurrence) For a schedule that runs daily.                                                                                 |
| `weekly_recurrence`                                                                                                              | [`WeeklyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.WeeklyRecurrence) For a schedule that runs weekly on a specific day.                                                            |

## BulkDeleteDocumentsMetadata

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) results from [`FirestoreAdmin.BulkDeleteDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments) .

| Fields               |                                                                                                                                                                                                                                                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation started.                                                                                                                                                                                                          |
| `end_time`           | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation completed. Will be unset if operation still in progress.                                                                                                                                                          |
| `operation_state`    | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The state of the operation.                                                                                                                                               |
| `progress_documents` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in documents, of this operation.                                                                                                                                        |
| `progress_bytes`     | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in bytes, of this operation.                                                                                                                                            |
| `collection_ids[]`   | `string` The IDs of the collection groups that are being deleted.                                                                                                                                                                                                                                                           |
| `namespace_ids[]`    | `string` Which namespace IDs are being deleted.                                                                                                                                                                                                                                                                             |
| `snapshot_time`      | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The timestamp that corresponds to the version of the database that is being read to get the list of documents to delete. This time can also be used as the timestamp of PITR in case of disaster recovery (subject to PITR window limit). |

## BulkDeleteDocumentsRequest

The request for [`FirestoreAdmin.BulkDeleteDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments) .

When both collection_ids and namespace_ids are set, only documents satisfying both conditions will be deleted.

Requests with namespace_ids and collection_ids both empty will be rejected. Please use [`FirestoreAdmin.DeleteDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase) instead.

| Fields             |                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Required. Database to operate. Should be of the form: `projects/{project_id}/databases/{database_id}` .                                                                                                                                                                                                                                                        |
| `collection_ids[]` | `string` Optional. IDs of the collection groups to delete. Unspecified means all collection groups. Each collection group in this list must be unique.                                                                                                                                                                                                                  |
| `namespace_ids[]`  | `string` Optional. Namespaces to delete. An empty list means all namespaces. This is the recommended usage for databases that don't use namespaces. An empty string element represents the default namespace. This should be used if the database has data in non-default namespaces, but doesn't want to delete from them. Each namespace in this list must be unique. |

## BulkDeleteDocumentsResponse

This type has no fields.

The response for [`FirestoreAdmin.BulkDeleteDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments) .

## CloneDatabaseMetadata

Metadata for the [`long-running operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) from the \[CloneDatabase\]\[google.firestore.admin.v1.CloneDatabase\] request.

| Fields                |                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the clone was started.                                                                                              |
| `end_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the clone finished, unset for ongoing clones.                                                                       |
| `operation_state`     | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The operation state of the clone.                            |
| `database`            | `string` The name of the database being cloned to.                                                                                                                                                             |
| `pitr_snapshot`       | [`PitrSnapshot`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.PitrSnapshot) The snapshot from which this database was cloned.                |
| `progress_percentage` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) How far along the clone is as an estimated percentage of remaining time. |

## CloneDatabaseRequest

The request message for [`FirestoreAdmin.CloneDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CloneDatabase) .

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`            | `string` Required. The project to clone the database in. Format is `projects/{project_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `database_id`       | `string` Required. The ID to use for the database, which will become the final component of the database's resource name. This database ID must not be associated with an existing database. This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/. "(default)" database ID is also valid if the database is Standard edition.                                                                                                                                                                                              |
| `pitr_snapshot`     | [`PitrSnapshot`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.PitrSnapshot) Required. Specification of the PITR data to clone from. The source database must exist. The cloned database will be created in the same location as the source database.                                                                                                                                                                                                                                                                                                                                                                      |
| `encryption_config` | [`EncryptionConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig) Optional. Encryption configuration for the cloned database. If this field is not specified, the cloned database will use the same encryption configuration as the source database, namely [`use_source_encryption`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.FIELDS.google.firestore.admin.v1.Database.EncryptionConfig.SourceEncryptionOptions.google.firestore.admin.v1.Database.EncryptionConfig.use_source_encryption) . |
| `tags`              | `map<string, string>` Optional. Immutable. Tags to be bound to the cloned database. The tags should be provided in the format of `tagKeys/{tag_key_id} -> tagValues/{tag_value_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## CreateBackupScheduleRequest

The request for [`FirestoreAdmin.CreateBackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateBackupSchedule) .

| Fields            |                                                                                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`          | `string` Required. The parent database. Format `projects/{project}/databases/{database}`                                                                                                   |
| `backup_schedule` | [`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule) Required. The backup schedule to create. |

## CreateDatabaseMetadata

This type has no fields.

Metadata related to the create database operation.

## CreateDatabaseRequest

The request for [`FirestoreAdmin.CreateDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateDatabase) .

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`      | `string` Required. A parent name of the form `projects/{project_id}`                                                                                                                                                                                                                                                                                                                                                        |
| `database`    | [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) Required. The Database to create.                                                                                                                                                                                                                                                     |
| `database_id` | `string` Required. The ID to use for the database, which will become the final component of the database's resource name. This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/. "(default)" database ID is also valid if the database is Standard edition. |

## CreateIndexRequest

The request for [`FirestoreAdmin.CreateIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateIndex) .

| Fields   |                                                                                                                                                                          |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent` | `string` Required. A parent name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}`                                            |
| `index`  | [`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index) Required. The composite index to create. |

## CreateUserCredsRequest

The request for [`FirestoreAdmin.CreateUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateUserCreds) .

| Fields          |                                                                                                                                                                                                                                                                                                                                                      |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`        | `string` Required. A parent name of the form `projects/{project_id}/databases/{database_id}`                                                                                                                                                                                                                                                         |
| `user_creds`    | [`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds) Required. The user creds to create.                                                                                                                                                                          |
| `user_creds_id` | `string` Required. The ID to use for the user creds, which will become the final component of the user creds's resource name. This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/. |

## DailyRecurrence

This type has no fields.

Represents a recurring schedule that runs every day.

The time zone is UTC.

## Database

A Cloud Firestore Database.

| Fields                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                | `string` The resource name of the Database. Format: `projects/{project}/databases/{database}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `uid`                                 | `string` Output only. The system-generated UUID4 for this Database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `create_time`                         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this database was created. Databases created before 2016 do not populate create_time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `update_time`                         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this database was most recently updated. Note this only includes updates to the database resource and not data contained by the database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `delete_time`                         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The timestamp at which this database was deleted. Only set if the database has been deleted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `location_id`                         | `string` Required. The location of the database. Available locations are listed at <https://cloud.google.com/firestore/docs/locations> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `type`                                | [`DatabaseType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DatabaseType) Required. The type of the database. See <https://cloud.google.com/datastore/docs/firestore-or-datastore> for information about how to choose.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `concurrency_mode`                    | [`ConcurrencyMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.ConcurrencyMode) The concurrency control mode to use for this database. If unspecified in a CreateDatabase request, this will default based on the database edition: Optimistic for Enterprise and Pessimistic for all other databases.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `version_retention_period`            | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Output only. The period during which past versions of data are retained in the database. Any [`read`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1#google.firestore.v1.GetDocumentRequest.FIELDS.google.protobuf.Timestamp.google.firestore.v1.GetDocumentRequest.read_time) or [`query`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1#google.firestore.v1.ListDocumentsRequest.FIELDS.google.protobuf.Timestamp.google.firestore.v1.ListDocumentsRequest.read_time) can specify a `read_time` within this window, and will read the state of the database at that time. If the PITR feature is enabled, the retention period is 7 days. Otherwise, the retention period is 1 hour. |
| `earliest_version_time`               | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The earliest timestamp at which older versions of the data can be read from the database. See \[version_retention_period\] above; this field is populated with `now - version_retention_period` . This value is continuously updated, and becomes stale the moment it is queried. If you are using this value to recover data, make sure to account for the time from the moment when the value is queried to the moment when you initiate the recovery.                                                                                                                                                                                                                                                                                 |
| `point_in_time_recovery_enablement`   | [`PointInTimeRecoveryEnablement`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.PointInTimeRecoveryEnablement) Whether to enable the PITR feature on this database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `app_engine_integration_mode`         | [`AppEngineIntegrationMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.AppEngineIntegrationMode) The App Engine integration mode to use for this database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `key_prefix`                          | `string` Output only. The key_prefix for this database. This key_prefix is used, in combination with the project ID (" \~ ") to construct the application ID that is returned from the Cloud Datastore APIs in Google App Engine first generation runtimes. This value may be empty in which case the appid to use for URL-encoded keys is the project_id (eg: foo instead of v\~foo).                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `delete_protection_state`             | [`DeleteProtectionState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DeleteProtectionState) State of delete protection for the database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `cmek_config`                         | [`CmekConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.CmekConfig) Optional. Presence indicates CMEK is enabled for this database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `previous_id`                         | `string` Output only. The database resource's prior database ID. This field is only populated for deleted databases.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `source_info`                         | [`SourceInfo`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.SourceInfo) Output only. Information about the provenance of this database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `tags`                                | `map<string, string>` Optional. Input only. Immutable. Tag keys/values directly bound to this resource. For example: "123/environment": "production", "123/costCenter": "marketing"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `etag`                                | `string` This checksum is computed by the server based on the value of other fields, and may be sent on update and delete requests to ensure the client has an up-to-date value before proceeding.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `database_edition`                    | [`DatabaseEdition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DatabaseEdition) Immutable. The edition of the database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `realtime_updates_mode`               | [`RealtimeUpdatesMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.RealtimeUpdatesMode) Immutable. The default Realtime Updates mode to use for this database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `firestore_data_access_mode`          | [`DataAccessMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DataAccessMode) Optional. The Firestore API data access mode to use for this database. If not set on write: - the default value is DATA_ACCESS_MODE_DISABLED for Enterprise Edition. - the default value is DATA_ACCESS_MODE_ENABLED for Standard Edition.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `mongodb_compatible_data_access_mode` | [`DataAccessMode`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.DataAccessMode) Optional. The MongoDB compatible API data access mode to use for this database. If not set on write, the default value is DATA_ACCESS_MODE_ENABLED for Enterprise Edition. The value is always DATA_ACCESS_MODE_DISABLED for Standard Edition.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `free_tier`                           | `bool` Output only. Background: Free tier is the ability of a Firestore database to use a small amount of resources every day without being charged. Once usage exceeds the free tier limit further usage is charged. Whether this database can make use of the free tier. Only one database per project can be eligible for the free tier. The first (or next) database that is created in a project without a free tier database will be marked as eligible for the free tier. Databases that are created while there is a free tier database will not be eligible for the free tier.                                                                                                                                                                                                                                                 |

## AppEngineIntegrationMode

The type of App Engine integration mode.

| Enums                                     |                                                                                                                                                                                                                                  |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `APP_ENGINE_INTEGRATION_MODE_UNSPECIFIED` | Not used.                                                                                                                                                                                                                        |
| `ENABLED`                                 | If an App Engine application exists in the same region as this database, App Engine configuration will impact this database. This includes disabling of the application & database, as well as disabling writes to the database. |
| `DISABLED`                                | App Engine has no effect on the ability of this database to serve requests. This is the default setting for databases created with the Firestore API.                                                                            |

## CmekConfig

The CMEK (Customer Managed Encryption Key) configuration for a Firestore database. If not present, the database is secured by the default Google encryption key.

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kms_key_name`         | `string` Required. Only keys in the same location as this database are allowed to be used for encryption. For Firestore's nam5 multi-region, this corresponds to Cloud KMS multi-region us. For Firestore's eur3 multi-region, this corresponds to Cloud KMS multi-region europe. See <https://cloud.google.com/kms/docs/locations> . The expected format is `projects/{project_id}/locations/{kms_location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |
| `active_key_version[]` | `string` Output only. Currently in-use [KMS key versions](https://cloud.google.com/kms/docs/resource-hierarchy#key_versions) . During [key rotation](https://cloud.google.com/kms/docs/key-rotation) , there can be multiple in-use key versions. The expected format is `projects/{project_id}/locations/{kms_location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}/cryptoKeyVersions/{key_version}` .                                                     |

## ConcurrencyMode

The type of concurrency control mode for transactions.

| Enums                           |                                                                                                                                                                                                                                                                                                        |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CONCURRENCY_MODE_UNSPECIFIED`  | Not used.                                                                                                                                                                                                                                                                                              |
| `OPTIMISTIC`                    | Use optimistic concurrency control by default. This mode is available for Cloud Firestore databases. This is the default setting for Cloud Firestore Enterprise Edition databases.                                                                                                                     |
| `PESSIMISTIC`                   | Use pessimistic concurrency control by default. This mode is available for Cloud Firestore databases. This is the default setting for Cloud Firestore Standard Edition databases.                                                                                                                      |
| `OPTIMISTIC_WITH_ENTITY_GROUPS` | Use optimistic concurrency control with entity groups by default. This mode is enabled for some databases that were automatically upgraded from Cloud Datastore to Cloud Firestore with Datastore Mode. It is not recommended for any new databases, and not supported for Firestore Native databases. |

## DataAccessMode

The data access mode.

| Enums                          |                                                       |
|--------------------------------|-------------------------------------------------------|
| `DATA_ACCESS_MODE_UNSPECIFIED` | Not Used.                                             |
| `DATA_ACCESS_MODE_ENABLED`     | Accessing the database through the API is allowed.    |
| `DATA_ACCESS_MODE_DISABLED`    | Accessing the database through the API is disallowed. |

## DatabaseEdition

The edition of the database.

| Enums                          |                                                                 |
|--------------------------------|-----------------------------------------------------------------|
| `DATABASE_EDITION_UNSPECIFIED` | Not used.                                                       |
| `STANDARD`                     | Standard edition. This is the default setting if not specified. |
| `ENTERPRISE`                   | Enterprise edition.                                             |

## DatabaseType

The type of the database. See <https://cloud.google.com/datastore/docs/firestore-or-datastore> for information about how to choose.

Mode changes are only allowed if the database is empty.

| Enums                       |                              |
|-----------------------------|------------------------------|
| `DATABASE_TYPE_UNSPECIFIED` | Not used.                    |
| `FIRESTORE_NATIVE`          | Firestore Native Mode        |
| `DATASTORE_MODE`            | Firestore in Datastore Mode. |

## DeleteProtectionState

The delete protection state of the database.

| Enums                                 |                                                            |
|---------------------------------------|------------------------------------------------------------|
| `DELETE_PROTECTION_STATE_UNSPECIFIED` | The default value. Delete protection type is not specified |
| `DELETE_PROTECTION_DISABLED`          | Delete protection is disabled                              |
| `DELETE_PROTECTION_ENABLED`           | Delete protection is enabled                               |

## EncryptionConfig

Encryption configuration for a new database being created from another source.

The source could be a [`Backup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup) or a [`PitrSnapshot`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.PitrSnapshot) .

| Fields                                                                                                                      |                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `encryption_type` . The method for encrypting the database. `encryption_type` can be only one of the following: |                                                                                                                                                                                                                                                                             |
| `google_default_encryption`                                                                                                 | [`GoogleDefaultEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.GoogleDefaultEncryptionOptions) Use Google default encryption.                                  |
| `use_source_encryption`                                                                                                     | [`SourceEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.SourceEncryptionOptions) The database will use the same encryption configuration as the source.        |
| `customer_managed_encryption`                                                                                               | [`CustomerManagedEncryptionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.CustomerManagedEncryptionOptions) Use Customer Managed Encryption Keys (CMEK) for encryption. |

## CustomerManagedEncryptionOptions

The configuration options for using CMEK (Customer Managed Encryption Key) encryption.

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kms_key_name` | `string` Required. Only keys in the same location as the database are allowed to be used for encryption. For Firestore's nam5 multi-region, this corresponds to Cloud KMS multi-region us. For Firestore's eur3 multi-region, this corresponds to Cloud KMS multi-region europe. See <https://cloud.google.com/kms/docs/locations> . The expected format is `projects/{project_id}/locations/{kms_location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

## GoogleDefaultEncryptionOptions

This type has no fields.

The configuration options for using Google default encryption.

## SourceEncryptionOptions

This type has no fields.

The configuration options for using the same encryption method as the source.

## PointInTimeRecoveryEnablement

Point In Time Recovery feature enablement.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>POINT_IN_TIME_RECOVERY_ENABLEMENT_UNSPECIFIED</code></td>
<td>Not used.</td>
</tr>
<tr class="even">
<td><code>POINT_IN_TIME_RECOVERY_ENABLED</code></td>
<td><p>Reads are supported on selected versions of the data from within the past 7 days:</p>
<ul>
<li>Reads against any timestamp within the past hour</li>
<li>Reads against 1-minute snapshots beyond 1 hour and within 7 days</li>
</ul>
<p><code>version_retention_period</code> and <code>earliest_version_time</code> can be used to determine the supported versions.</p></td>
</tr>
<tr class="odd">
<td><code>POINT_IN_TIME_RECOVERY_DISABLED</code></td>
<td>Reads are supported on any version of the data from within the past 1 hour.</td>
</tr>
</tbody>
</table>

## SourceInfo

Information about the provenance of this database.

| Fields                                                                                                            |                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `operation`                                                                                                       | `string` The associated long-running operation. This field may not be set after the operation has completed. Format: `projects/{project}/databases/{database}/operations/{operation}` .                                                                 |
| Union field `source` . The source from which this database is derived. `source` can be only one of the following: |                                                                                                                                                                                                                                                         |
| `backup`                                                                                                          | [`BackupSource`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.SourceInfo.BackupSource) If set, this database was restored from the specified backup (or a snapshot thereof). |

## BackupSource

Information about a backup that was used to restore a database.

| Fields   |                                                                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backup` | `string` The resource name of the backup that was used to restore this database. Format: `projects/{project}/locations/{location}/backups/{backup}` . |

## DeleteBackupRequest

The request for [`FirestoreAdmin.DeleteBackup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DeleteBackup) .

| Fields |                                                                                                                         |
|--------|-------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. Name of the backup to delete. format is `projects/{project}/locations/{location}/backups/{backup}` . |

## DeleteBackupScheduleRequest

The request for \[FirestoreAdmin.DeleteBackupSchedules\]\[\].

| Fields |                                                                                                                                        |
|--------|----------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the backup schedule. Format `projects/{project}/databases/{database}/backupSchedules/{backup_schedule}` |

## DeleteDatabaseMetadata

This type has no fields.

Metadata related to the delete database operation.

## DeleteDatabaseRequest

The request for [`FirestoreAdmin.DeleteDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase) .

| Fields |                                                                                                                                                                                                   |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}`                                                                                                             |
| `etag` | `string` The current etag of the Database. If an etag is provided and does not match the current etag of the database, deletion will be blocked and a FAILED_PRECONDITION error will be returned. |

## DeleteIndexRequest

The request for [`FirestoreAdmin.DeleteIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DeleteIndex) .

| Fields |                                                                                                                                           |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/indexes/{index_id}` |

## DeleteUserCredsRequest

The request for [`FirestoreAdmin.DeleteUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DeleteUserCreds) .

| Fields |                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/userCreds/{user_creds_id}` |

## DisableUserCredsRequest

The request for [`FirestoreAdmin.DisableUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.DisableUserCreds) .

| Fields |                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/userCreds/{user_creds_id}` |

## EnableUserCredsRequest

The request for [`FirestoreAdmin.EnableUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.EnableUserCreds) .

| Fields |                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/userCreds/{user_creds_id}` |

## ExportDocumentsMetadata

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) results from [`FirestoreAdmin.ExportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ExportDocuments) .

| Fields               |                                                                                                                                                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation started.                                                                                                                                                     |
| `end_time`           | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation completed. Will be unset if operation still in progress.                                                                                                     |
| `operation_state`    | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The state of the export operation.                                                                                   |
| `progress_documents` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in documents, of this operation.                                                                                   |
| `progress_bytes`     | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in bytes, of this operation.                                                                                       |
| `collection_ids[]`   | `string` Which collection IDs are being exported.                                                                                                                                                                                                                      |
| `output_uri_prefix`  | `string` Where the documents are being exported to.                                                                                                                                                                                                                    |
| `namespace_ids[]`    | `string` Which namespace IDs are being exported.                                                                                                                                                                                                                       |
| `snapshot_time`      | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The timestamp that corresponds to the version of the database that is being exported. If unspecified, there are no guarantees about the consistency of the documents being exported. |

## ExportDocumentsRequest

The request for [`FirestoreAdmin.ExportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ExportDocuments) .

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`              | `string` Required. Database to export. Should be of the form: `projects/{project_id}/databases/{database_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `collection_ids[]`  | `string` IDs of the collection groups to export. Unspecified means all collection groups. Each collection group in this list must be unique.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `output_uri_prefix` | `string` The output URI. Currently only supports Google Cloud Storage URIs of the form: `gs://BUCKET_NAME[/NAMESPACE_PATH]` , where `BUCKET_NAME` is the name of the Google Cloud Storage bucket and `NAMESPACE_PATH` is an optional Google Cloud Storage namespace path. When choosing a name, be sure to consider Google Cloud Storage naming guidelines: <https://cloud.google.com/storage/docs/naming> . If the URI is a bucket (without a namespace path), a prefix will be generated based on the start time.                                                                                                                                                                           |
| `namespace_ids[]`   | `string` An empty list represents all namespaces. This is the preferred usage for databases that don't use namespaces. An empty string element represents the default namespace. This should be used if the database has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique.                                                                                                                                                                                                                                                                                                                                                        |
| `snapshot_time`     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The timestamp that corresponds to the version of the database to be exported. The timestamp must be in the past, rounded to the minute and not older than [`earliestVersionTime`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.FIELDS.google.protobuf.Timestamp.google.firestore.admin.v1.Database.earliest_version_time) . If specified, then the exported documents will represent a consistent view of the database at the provided time. Otherwise, there are no guarantees about the consistency of the exported documents. |

## ExportDocumentsResponse

Returned in the [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) response field.

| Fields              |                                                                                                                                                                               |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `output_uri_prefix` | `string` Location of the output files. This can be used to begin an import into Cloud Firestore (this project or another project) after the operation completes successfully. |

## Field

Represents a single field in the database.

Fields are grouped by their "Collection Group", which represent all collections in the database with the same ID.

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Required. A field name of the form: `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/fields/{field_path}` A field path can be a simple field name, e.g. `address` or a path to fields within `map_value` , e.g. `address.city` , or a special field path. The only valid special field is `*` , which represents any field. Field paths can be quoted using `` ` `` (backtick). The only character that must be escaped within a quoted field path is the backtick character itself, escaped using a backslash. Special characters in field paths that must be quoted include: `*` , `.` , `` ` `` (backtick), `[` , `]` , as well as any ascii symbolic characters. Examples: `` `address.city` `` represents a field named `address.city` , not the map key `city` in the field `address` . `` `*` `` represents a field named `*` , not any field. A special `Field` contains the default indexing settings for all fields. This field's resource name is: `projects/{project_id}/databases/{database_id}/collectionGroups/__default__/fields/*` Indexes defined on this `Field` will be applied to all fields which do not have their own `Field` index configuration. |
| `index_config` | [`IndexConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.IndexConfig) The index configuration for this field. If unset, field indexing will revert to the configuration defined by the `ancestor_field` . To explicitly remove all indexes for this field, specify an index config with an empty list of indexes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `ttl_config`   | [`TtlConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.TtlConfig) The TTL configuration for this `Field` . Setting or unsetting this will enable or disable the TTL for documents that have this `Field` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

## IndexConfig

The index configuration for this field.

| Fields                 |                                                                                                                                                                                                                                                                                                             |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexes[]`            | [`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index) The indexes supported for this field.                                                                                                                                       |
| `uses_ancestor_config` | `bool` Output only. When true, the `Field` 's index configuration is set from the configuration specified by the `ancestor_field` . When false, the `Field` 's index configuration is defined explicitly.                                                                                                   |
| `ancestor_field`       | `string` Output only. Specifies the resource name of the `Field` from which this field's index configuration is set (when `uses_ancestor_config` is true), or from which it *would* be set if this field had no index configuration (when `uses_ancestor_config` is false).                                 |
| `reverting`            | `bool` Output only When true, the `Field` 's index configuration is in the process of being reverted. Once complete, the index config will transition to the same state as the field specified by `ancestor_field` , at which point `uses_ancestor_config` will be `true` and `reverting` will be `false` . |

## TtlConfig

The TTL (time-to-live) configuration for documents that have this `Field` set.

A timestamp stored in a TTL-enabled field will be used to determine the expiration time of the document. The expiration time is the sum of the timestamp value and the `expiration_offset` .

For Enterprise edition databases, the timestamp value may alternatively be stored in an array value in the TTL-enabled field.

An expiration time in the past indicates that the document is eligible for immediate expiration. Using any other data type or leaving the field absent will disable expiration for the individual document.

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`             | [`State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field.TtlConfig.State) Output only. The state of the TTL configuration.                                                                                                                                                                                                                                                                        |
| `expiration_offset` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Optional. The offset, relative to the timestamp value from the TTL-enabled field, used to determine the document's expiration time. `expiration_offset.seconds` must be between 0 and 2,147,483,647 inclusive. Values more precise than seconds are rejected. If unset, defaults to 0, in which case the expiration time is the same as the timestamp value from the TTL-enabled field. |

## State

The state of applying the TTL configuration to all documents.

| Enums               |                                                                                                                                                                                                                                                                                                                 |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified or unknown.                                                                                                                                                                                                                                                                            |
| `CREATING`          | The TTL is being applied. There is an active long-running operation to track the change. Newly written documents will have TTLs applied as requested. Requested TTLs on existing documents are still being processed. When TTLs on all existing documents have been processed, the state will move to 'ACTIVE'. |
| `ACTIVE`            | The TTL is active for all documents.                                                                                                                                                                                                                                                                            |
| `NEEDS_REPAIR`      | The TTL configuration could not be enabled for all existing documents. Newly written documents will continue to have their TTL applied. The LRO returned when last attempting to enable TTL for this `Field` has failed, and may have more details.                                                             |

## FieldOperationMetadata

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) results from [`FirestoreAdmin.UpdateField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.UpdateField) .

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation started.                                                                                                                                                                                                                                                                                                 |
| `end_time`              | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation completed. Will be unset if operation still in progress.                                                                                                                                                                                                                                                 |
| `field`                 | `string` The field resource that this operation is acting on. For example: `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/fields/{field_path}`                                                                                                                                                                                                                                    |
| `index_config_deltas[]` | [`IndexConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.IndexConfigDelta) A list of [`IndexConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.IndexConfigDelta) , which describe the intent of this operation. |
| `state`                 | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The state of the operation.                                                                                                                                                                                                                                      |
| `progress_documents`    | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in documents, of this operation.                                                                                                                                                                                                                               |
| `progress_bytes`        | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in bytes, of this operation.                                                                                                                                                                                                                                   |
| `ttl_config_delta`      | [`TtlConfigDelta`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.TtlConfigDelta) Describes the deltas of TTL configuration.                                                                                                                                                                                                |

## IndexConfigDelta

Information about an index configuration change.

| Fields        |                                                                                                                                                                                                                        |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `change_type` | [`ChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.IndexConfigDelta.ChangeType) Specifies how the index is changing. |
| `index`       | [`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index) The index being changed.                                                               |

## ChangeType

Specifies how the index is changing.

| Enums                     |                                               |
|---------------------------|-----------------------------------------------|
| `CHANGE_TYPE_UNSPECIFIED` | The type of change is not specified or known. |
| `ADD`                     | The single field index is being added.        |
| `REMOVE`                  | The single field index is being removed.      |

## TtlConfigDelta

Information about a TTL configuration change.

| Fields              |                                                                                                                                                                                                                                  |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `change_type`       | [`ChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FieldOperationMetadata.TtlConfigDelta.ChangeType) Specifies how the TTL configuration is changing. |
| `expiration_offset` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) The offset, relative to the timestamp value in the TTL-enabled field, used determine the document's expiration time.                             |

## ChangeType

Specifies how the TTL config is changing.

| Enums                     |                                               |
|---------------------------|-----------------------------------------------|
| `CHANGE_TYPE_UNSPECIFIED` | The type of change is not specified or known. |
| `ADD`                     | The TTL config is being added.                |
| `REMOVE`                  | The TTL config is being removed.              |

## GetBackupRequest

The request for [`FirestoreAdmin.GetBackup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetBackup) .

| Fields |                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. Name of the backup to fetch. Format is `projects/{project}/locations/{location}/backups/{backup}` . |

## GetBackupScheduleRequest

The request for [`FirestoreAdmin.GetBackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetBackupSchedule) .

| Fields |                                                                                                                                        |
|--------|----------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the backup schedule. Format `projects/{project}/databases/{database}/backupSchedules/{backup_schedule}` |

## GetDatabaseRequest

The request for [`FirestoreAdmin.GetDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetDatabase) .

| Fields |                                                                                       |
|--------|---------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}` |

## GetFieldRequest

The request for [`FirestoreAdmin.GetField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetField) .

| Fields |                                                                                                                                          |
|--------|------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/fields/{field_id}` |

## GetIndexRequest

The request for [`FirestoreAdmin.GetIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetIndex) .

| Fields |                                                                                                                                           |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/indexes/{index_id}` |

## GetUserCredsRequest

The request for [`FirestoreAdmin.GetUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.GetUserCreds) .

| Fields |                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/userCreds/{user_creds_id}` |

## ImportDocumentsMetadata

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) results from [`FirestoreAdmin.ImportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ImportDocuments) .

| Fields               |                                                                                                                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation started.                                                                   |
| `end_time`           | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation completed. Will be unset if operation still in progress.                   |
| `operation_state`    | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The state of the import operation. |
| `progress_documents` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in documents, of this operation. |
| `progress_bytes`     | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in bytes, of this operation.     |
| `collection_ids[]`   | `string` Which collection IDs are being imported.                                                                                                                                    |
| `input_uri_prefix`   | `string` The location of the documents being imported.                                                                                                                               |
| `namespace_ids[]`    | `string` Which namespace IDs are being imported.                                                                                                                                     |

## ImportDocumentsRequest

The request for [`FirestoreAdmin.ImportDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ImportDocuments) .

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Required. Database to import into. Should be of the form: `projects/{project_id}/databases/{database_id}` .                                                                                                                                                                                                                                                                                                                                                  |
| `collection_ids[]` | `string` IDs of the collection groups to import. Unspecified means all collection groups that were included in the export. Each collection group in this list must be unique.                                                                                                                                                                                                                                                                                         |
| `input_uri_prefix` | `string` Location of the exported files. This must match the output_uri_prefix of an ExportDocumentsResponse from an export that has completed successfully. See: [`google.firestore.admin.v1.ExportDocumentsResponse.output_uri_prefix`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.ExportDocumentsResponse.FIELDS.string.google.firestore.admin.v1.ExportDocumentsResponse.output_uri_prefix) . |
| `namespace_ids[]`  | `string` An empty list represents all namespaces. This is the preferred usage for databases that don't use namespaces. An empty string element represents the default namespace. This should be used if the database has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique.                                                                                                                                |

## Index

Cloud Firestore indexes enable simple and complex queries against documents in a database.

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Output only. A server defined name for this index. The form of this name for composite indexes will be: `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/indexes/{composite_index_id}` For single field indexes, this field will be empty.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `query_scope`          | [`QueryScope`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.QueryScope) Indexes with a collection query scope specified allow queries against a collection that is the child of a specific document, specified at query time, and that has the same collection ID. Indexes with a collection group query scope specified allow queries against all collections descended from a specific document, specified at query time, and that have the same collection ID as this index.                                                                                                                                                                                                               |
| `api_scope`            | [`ApiScope`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.ApiScope) The API scope supported by this index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `fields[]`             | [`IndexField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField) The fields supported by this index. For composite indexes, this requires a minimum of 2 and a maximum of 100 fields. The last field entry is always for the field path `__name__` . If, on creation, `__name__` was not specified as the last field, it will be added automatically with the same direction as that of the last field defined. If the final field in a composite index is not directional, the `__name__` will be ordered ASCENDING (unless explicitly specified). For single field indexes, this will always be exactly one entry with a field path equal to the field path of the associated field. |
| `state`                | [`State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.State) Output only. The serving state of the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `density`              | [`Density`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.Density) Immutable. The density configuration of the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `multikey`             | `bool` Optional. Whether the index is multikey. By default, the index is not multikey. For non-multikey indexes, none of the paths in the index definition reach or traverse an array, except via an explicit array index. For multikey indexes, at most one of the paths in the index definition reach or traverse an array, except via an explicit array index. Violations will result in errors. Note this field only applies to index with MONGODB_COMPATIBLE_API ApiScope.                                                                                                                                                                                                                                                                                       |
| `shard_count`          | `int32` Optional. The number of shards for the index.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `unique`               | `bool` Optional. Whether it is an unique index. Unique index ensures all values for the indexed field(s) are unique across documents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `search_index_options` | [`SearchIndexOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.SearchIndexOptions) Optional. Options for search indexes that are at the index definition level.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

## ApiScope

API Scope defines the APIs (Firestore Native, or Firestore in Datastore Mode) that are supported for queries.

| Enums                    |                                                                                    |
|--------------------------|------------------------------------------------------------------------------------|
| `ANY_API`                | The index can only be used by the Firestore Native query API. This is the default. |
| `DATASTORE_MODE_API`     | The index can only be used by the Firestore in Datastore Mode query API.           |
| `MONGODB_COMPATIBLE_API` | The index can only be used by the MONGODB_COMPATIBLE_API.                          |

## Density

The density configuration for the index.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>DENSITY_UNSPECIFIED</code></td>
<td>Unspecified. It will use database default setting. This value is input only.</td>
</tr>
<tr class="even">
<td><code>SPARSE_ALL</code></td>
<td><p>An index entry will only exist if ALL fields are present in the document.</p>
<p>This is both the default and only allowed value for Standard Edition databases (for both Cloud Firestore <code>ANY_API</code> and Cloud Datastore <code>DATASTORE_MODE_API</code> ).</p>
<p>Take for example the following document:</p>
<pre data-fenced=""><code>{
  &quot;__name__&quot;: &quot;...&quot;,
  &quot;a&quot;: 1,
  &quot;b&quot;: 2,
  &quot;c&quot;: 3
}</code></pre>
<p>an index on <code>(a ASC, b ASC, c ASC, __name__ ASC)</code> will generate an index entry for this document since <code>a</code> , 'b', <code>c</code> , and <code>__name__</code> are all present but an index of <code>(a ASC, d ASC, __name__ ASC)</code> will not generate an index entry for this document since <code>d</code> is missing.</p>
<p>This means that such indexes can only be used to serve a query when the query has either implicit or explicit requirements that all fields from the index are present.</p></td>
</tr>
<tr class="odd">
<td><code>SPARSE_ANY</code></td>
<td><p>An index entry will exist if ANY field are present in the document.</p>
<p>This is used as the definition of a sparse index for Enterprise Edition databases.</p>
<p>Take for example the following document:</p>
<pre data-fenced=""><code>{
  &quot;__name__&quot;: &quot;...&quot;,
  &quot;a&quot;: 1,
  &quot;b&quot;: 2,
  &quot;c&quot;: 3
}</code></pre>
<p>an index on <code>(a ASC, d ASC)</code> will generate an index entry for this document since <code>a</code> is present, and will fill in an <code>unset</code> value for <code>d</code> . An index on <code>(d ASC, e ASC)</code> will not generate any index entry as neither <code>d</code> nor <code>e</code> are present.</p>
<p>An index that contains <code>__name__</code> will generate an index entry for all documents since Firestore guarantees that all documents have a <code>__name__</code> field.</p></td>
</tr>
<tr class="even">
<td><code>DENSE</code></td>
<td><p>An index entry will exist regardless of if the fields are present or not.</p>
<p>This is the default density for an Enterprise Edition database.</p>
<p>The index will store <code>unset</code> values for fields that are not present in the document.</p></td>
</tr>
</tbody>
</table>

## IndexField

A field in an index. The field_path describes which field is indexed, the value_mode describes how the field value is indexed.

| Fields                                                                                                    |                                                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field_path`                                                                                              | `string` Can be **name** . For single field indexes, this must match the name of the field or may be omitted.                                                                                                                                                   |
| Union field `value_mode` . How the field value is indexed. `value_mode` can be only one of the following: |                                                                                                                                                                                                                                                                 |
| `order`                                                                                                   | [`Order`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.Order) Indicates that this field supports ordering by the specified order or comparing using =, !=, \<, \<=, \>, \>=. |
| `array_config`                                                                                            | [`ArrayConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.ArrayConfig) Indicates that this field supports operations on `array_value` s.                                  |
| `vector_config`                                                                                           | [`VectorConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.VectorConfig) Indicates that this field supports nearest neighbor and distance operations on vector.           |
| `search_config`                                                                                           | [`SearchConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig) Indicates that this field supports search operations.                                            |

## ArrayConfig

The supported array value configurations.

| Enums                      |                                                      |
|----------------------------|------------------------------------------------------|
| `ARRAY_CONFIG_UNSPECIFIED` | The index does not support additional array queries. |
| `CONTAINS`                 | The index supports array containment queries.        |

## Order

The supported orderings.

| Enums               |                                                  |
|---------------------|--------------------------------------------------|
| `ORDER_UNSPECIFIED` | The ordering is unspecified. Not a valid option. |
| `ASCENDING`         | The field is ordered by ascending field value.   |
| `DESCENDING`        | The field is ordered by descending field value.  |

## SearchConfig

The configuration for how to index a field for search.

| Fields      |                                                                                                                                                                                                                                                           |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text_spec` | [`SearchTextSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchTextSpec) Optional. The specification for building a text search index for a field. |
| `geo_spec`  | [`SearchGeoSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchGeoSpec) Optional. The specification for building a geo search index for a field.    |

## SearchGeoSpec

The specification for how to build a geo search index for a field.

| Fields                       |                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------|
| `geo_json_indexing_disabled` | `bool` Optional. Disables geoJSON indexing for the field. By default, geoJSON points are indexed. |

## SearchTextIndexSpec

Specification of how the field should be indexed for search text indexes.

| Fields       |                                                                                                                                                                                                                            |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index_type` | [`TextIndexType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.TextIndexType) Required. How to index the text field value. |
| `match_type` | [`TextMatchType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.TextMatchType) Required. How to match the text field value. |

## SearchTextSpec

The specification for how to build a text search index for a field.

| Fields          |                                                                                                                                                                                                                                                                                                                     |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index_specs[]` | [`SearchTextIndexSpec`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.SearchConfig.SearchTextIndexSpec) Required. Specifications for how the field should be indexed. Repeated so that the field can be indexed in multiple ways. |

## TextIndexType

Ways to index the text field value.

| Enums                         |                                                    |
|-------------------------------|----------------------------------------------------|
| `TEXT_INDEX_TYPE_UNSPECIFIED` | The index type is unspecified. Not a valid option. |
| `TOKENIZED`                   | Field values are tokenized.                        |

## TextMatchType

Types of text matches that are supported for the field.

| Enums                         |                                                    |
|-------------------------------|----------------------------------------------------|
| `TEXT_MATCH_TYPE_UNSPECIFIED` | The match type is unspecified. Not a valid option. |
| `MATCH_GLOBALLY`              | Match on any indexed field.                        |

## VectorConfig

The index configuration to support vector search operations

| Fields                                                                                |                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dimension`                                                                           | `int32` Required. The vector dimension this configuration applies to. The resulting index will only include vectors of this dimension, and can be used for vector search with the same dimension.                 |
| Union field `type` . The type of index used. `type` can be only one of the following: |                                                                                                                                                                                                                   |
| `flat`                                                                                | [`FlatIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index.IndexField.VectorConfig.FlatIndex) Indicates the vector index is a flat index. |

## FlatIndex

This type has no fields.

An index that stores vectors in a flat data structure, and supports exhaustive search.

## QueryScope

Query Scope defines the scope at which a query is run. This is specified on a StructuredQuery's `from` field.

| Enums                     |                                                                                                                                                                                                              |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `QUERY_SCOPE_UNSPECIFIED` | The query scope is unspecified. Not a valid option.                                                                                                                                                          |
| `COLLECTION`              | Indexes with a collection query scope specified allow queries against a collection that is the child of a specific document, specified at query time, and that has the collection ID specified by the index. |
| `COLLECTION_GROUP`        | Indexes with a collection group query scope specified allow queries against all collections that has the collection ID specified by the index.                                                               |
| `COLLECTION_RECURSIVE`    | Include all the collections's ancestor in the index. Only available for Datastore Mode databases.                                                                                                            |

## SearchIndexOptions

Options for search indexes at the definition level.

| Fields                              |                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text_language`                     | `string` Optional. The language to use for text search indexes. Used as the default language if not overridden at the document level by specifying the `text_language_override_field` . The language is specified as a BCP 47 language code. For indexes with MONGODB_COMPATIBLE_API ApiScope: If unspecified, the default language is English. For indexes with `ANY_API` ApiScope: If unspecified, the default behavior is autodetect. |
| `text_language_override_field_path` | `string` Optional. The field in the document that specifies which language to use for that specific document. For indexes with MONGODB_COMPATIBLE_API ApiScope: if unspecified, the language is taken from the "language" field if it exists or from `text_language` if it does not.                                                                                                                                                     |

## State

The state of an index. During index creation, an index will be in the `CREATING` state. If the index is created successfully, it will transition to the `READY` state. If the index creation encounters a problem, the index will transition to the `NEEDS_REPAIR` state.

| Enums               |                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                                                                                                                                                                                                                                                                                                                                      |
| `CREATING`          | The index is being created. There is an active long-running operation for the index. The index is updated when writing a document. Some index data may exist.                                                                                                                                                                                                                                                  |
| `READY`             | The index is ready to be used. The index is updated when writing a document. The index is fully populated from all stored documents it applies to.                                                                                                                                                                                                                                                             |
| `NEEDS_REPAIR`      | The index was being created, but something went wrong. There is no active long-running operation for the index, and the most recently finished long-running operation failed. The index is not updated when writing a document. Some index data may exist. Use the google.longrunning.Operations API to determine why the operation that last attempted to create this index failed, then re-create the index. |

## IndexOperationMetadata

Metadata for [`google.longrunning.Operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) results from [`FirestoreAdmin.CreateIndex`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.CreateIndex) .

| Fields               |                                                                                                                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation started.                                                                   |
| `end_time`           | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time this operation completed. Will be unset if operation still in progress.                   |
| `index`              | `string` The index resource that this operation is acting on. For example: `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}/indexes/{index_id}`       |
| `state`              | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The state of the operation.        |
| `progress_documents` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in documents, of this operation. |
| `progress_bytes`     | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) The progress, in bytes, of this operation.     |

## ListBackupSchedulesRequest

The request for [`FirestoreAdmin.ListBackupSchedules`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules) .

| Fields   |                                                                                               |
|----------|-----------------------------------------------------------------------------------------------|
| `parent` | `string` Required. The parent database. Format is `projects/{project}/databases/{database}` . |

## ListBackupSchedulesResponse

The response for [`FirestoreAdmin.ListBackupSchedules`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules) .

| Fields               |                                                                                                                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backup_schedules[]` | [`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule) List of all backup schedules. |

## ListBackupsRequest

The request for [`FirestoreAdmin.ListBackups`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListBackups) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The location to list backups from.</p>
<p>Format is <code>projects/{project}/locations/{location}</code> . Use <code>{location} = '-'</code> to list backups from all locations for the given project. This allows listing backups from a single location or from all locations.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>An expression that filters the list of returned backups.</p>
<p>A filter expression consists of a field name, a comparison operator, and a value for filtering. The value must be a string, a number, or a boolean. The comparison operator must be one of: <code>&lt;</code> , <code>&gt;</code> , <code>&lt;=</code> , <code>&gt;=</code> , <code>!=</code> , <code>=</code> , or <code>:</code> . Colon <code>:</code> is the contains operator. Filter rules are not case sensitive.</p>
<p>The following fields in the <a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup"><code>Backup</code></a> are eligible for filtering:</p>
<ul>
<li><code>database_uid</code> (supports <code>=</code> only)</li>
</ul></td>
</tr>
</tbody>
</table>

## ListBackupsResponse

The response for [`FirestoreAdmin.ListBackups`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListBackups) .

| Fields          |                                                                                                                                                                                                                                                                                                                                            |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backups[]`     | [`Backup`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Backup) List of all backups for the project.                                                                                                                                                                     |
| `unreachable[]` | `string` List of locations that existing backups were not able to be fetched from. Instead of failing the entire requests when a single location is unreachable, this response returns a partial result set and list of locations unable to be reached here. The request can be retried against a single location to get a concrete error. |

## ListDatabasesRequest

A request to list the Firestore Databases in all locations for a project.

| Fields         |                                                                      |
|----------------|----------------------------------------------------------------------|
| `parent`       | `string` Required. A parent name of the form `projects/{project_id}` |
| `show_deleted` | `bool` If true, also returns deleted resources.                      |

## ListDatabasesResponse

The list of databases for a project.

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `databases[]`   | [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) The databases in the project.                                                                                                                                                                                                                                                                                                                                                          |
| `unreachable[]` | `string` In the event that data about individual databases cannot be listed they will be recorded here. An example entry might be: projects/some_project/locations/some_location This can happen if the Cloud Region that the Database resides in is currently unavailable. In this case we can't fetch all the details about the database. You may be able to get a more detailed error message (or possibly fetch the resource) by sending a 'Get' request for the resource or a 'List' request for the specific location. |

## ListFieldsRequest

The request for [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) .

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. A parent name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `filter`     | `string` The filter to apply to list results. Currently, [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) only supports listing fields that have been explicitly overridden. To issue this query, call [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) with a filter that includes `indexConfig.usesAncestorConfig:false` or `ttlConfig:*` . |
| `page_size`  | `int32` The number of results to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `page_token` | `string` A page token, returned from a previous call to [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) , that may be used to get the next page of results.                                                                                                                                                                                                                                                                                                         |

## ListFieldsResponse

The response for [`FirestoreAdmin.ListFields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListFields) .

| Fields            |                                                                                                                                                       |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]`        | [`Field`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field) The requested fields. |
| `next_page_token` | `string` A page token that may be used to request another page of results. If blank, this is the last page.                                           |

## ListIndexesRequest

The request for [`FirestoreAdmin.ListIndexes`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListIndexes) .

| Fields       |                                                                                                                                                                                                                                                                                       |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. A parent name of the form `projects/{project_id}/databases/{database_id}/collectionGroups/{collection_id}`                                                                                                                                                         |
| `filter`     | `string` The filter to apply to list results.                                                                                                                                                                                                                                         |
| `page_size`  | `int32` The number of results to return.                                                                                                                                                                                                                                              |
| `page_token` | `string` A page token, returned from a previous call to [`FirestoreAdmin.ListIndexes`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListIndexes) , that may be used to get the next page of results. |

## ListIndexesResponse

The response for [`FirestoreAdmin.ListIndexes`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListIndexes) .

| Fields            |                                                                                                                                                        |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexes[]`       | [`Index`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Index) The requested indexes. |
| `next_page_token` | `string` A page token that may be used to request another page of results. If blank, this is the last page.                                            |

## ListUserCredsRequest

The request for [`FirestoreAdmin.ListUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListUserCreds) .

| Fields   |                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------|
| `parent` | `string` Required. A parent database name of the form `projects/{project_id}/databases/{database_id}` |

## ListUserCredsResponse

The response for [`FirestoreAdmin.ListUserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ListUserCreds) .

| Fields         |                                                                                                                                                                          |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `user_creds[]` | [`UserCreds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds) The user creds for the database. |

## LocationMetadata

This type has no fields.

The metadata message for [`google.cloud.location.Location.metadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Location.FIELDS.google.protobuf.Any.google.cloud.location.Location.metadata) .

## OperationState

Describes the state of the operation.

| Enums                         |                                                                                                                                |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `OPERATION_STATE_UNSPECIFIED` | Unspecified.                                                                                                                   |
| `INITIALIZING`                | Request is being prepared for processing.                                                                                      |
| `PROCESSING`                  | Request is actively being processed.                                                                                           |
| `CANCELLING`                  | Request is in the process of being cancelled after user called google.longrunning.Operations.CancelOperation on the operation. |
| `FINALIZING`                  | Request has been processed and is in its finalization stage.                                                                   |
| `SUCCESSFUL`                  | Request has completed successfully.                                                                                            |
| `FAILED`                      | Request has finished being processed, but encountered an error.                                                                |
| `CANCELLED`                   | Request has finished being cancelled after user called google.longrunning.Operations.CancelOperation.                          |

## PitrSnapshot

A consistent snapshot of a database at a specific point in time. A PITR (Point-in-time recovery) snapshot with previous versions of a database's data is available for every minute up to the associated database's data retention period. If the PITR feature is enabled, the retention period is 7 days; otherwise, it is one hour.

| Fields          |                                                                                                                              |
|-----------------|------------------------------------------------------------------------------------------------------------------------------|
| `database`      | `string` Required. The name of the database that this was a snapshot of. Format: `projects/{project}/databases/{database}` . |
| `database_uid`  | `bytes` Output only. Public UUID of the database the snapshot was associated with.                                           |
| `snapshot_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Required. Snapshot time of the database.   |

## Progress

Describes the progress of the operation. Unit of work is generic and must be interpreted based on where [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) is used.

| Fields           |                                       |
|------------------|---------------------------------------|
| `estimated_work` | `int64` The amount of work estimated. |
| `completed_work` | `int64` The amount of work completed. |

## RealtimeUpdatesMode

The Realtime Updates mode.

| Enums                               |                                                                                                                        |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `REALTIME_UPDATES_MODE_UNSPECIFIED` | The Realtime Updates feature is not specified.                                                                         |
| `REALTIME_UPDATES_MODE_ENABLED`     | The Realtime Updates feature is enabled by default. This could potentially degrade write performance for the database. |
| `REALTIME_UPDATES_MODE_DISABLED`    | The Realtime Updates feature is disabled by default.                                                                   |

## ResetUserPasswordRequest

The request for [`FirestoreAdmin.ResetUserPassword`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.ResetUserPassword) .

| Fields |                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. A name of the form `projects/{project_id}/databases/{database_id}/userCreds/{user_creds_id}` |

## RestoreDatabaseMetadata

Metadata for the [`long-running operation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.longrunning#google.longrunning.Operation) from the \[RestoreDatabase\]\[google.firestore.admin.v1.RestoreDatabase\] request.

| Fields                |                                                                                                                                                                                                                  |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the restore was started.                                                                                              |
| `end_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the restore finished, unset for ongoing restores.                                                                     |
| `operation_state`     | [`OperationState`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.OperationState) The operation state of the restore.                            |
| `database`            | `string` The name of the database being restored to.                                                                                                                                                             |
| `backup`              | `string` The name of the backup restoring from.                                                                                                                                                                  |
| `progress_percentage` | [`Progress`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Progress) How far along the restore is as an estimated percentage of remaining time. |

## RestoreDatabaseRequest

The request message for [`FirestoreAdmin.RestoreDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.RestoreDatabase) .

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`            | `string` Required. The project to restore the database in. Format is `projects/{project_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `database_id`       | `string` Required. The ID to use for the database, which will become the final component of the database's resource name. This database ID must not be associated with an existing database. This value should be 4-63 characters. Valid characters are /\[a-z\]\[0-9\]-/ with first character a letter and the last a letter or a number. Must not be UUID-like /\[0-9a-f\]{8}(-\[0-9a-f\]{4}){3}-\[0-9a-f\]{12}/. "(default)" database ID is also valid if the database is Standard edition.                                                                                                                                                                                         |
| `backup`            | `string` Required. Backup to restore from. Must be from the same project as the parent. The restored database will be created in the same location as the source backup. Format is: `projects/{project_id}/locations/{location}/backups/{backup}`                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `encryption_config` | [`EncryptionConfig`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig) Optional. Encryption configuration for the restored database. If this field is not specified, the restored database will use the same encryption configuration as the backup, namely [`use_source_encryption`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database.EncryptionConfig.FIELDS.google.firestore.admin.v1.Database.EncryptionConfig.SourceEncryptionOptions.google.firestore.admin.v1.Database.EncryptionConfig.use_source_encryption) . |
| `tags`              | `map<string, string>` Optional. Immutable. Tags to be bound to the restored database. The tags should be provided in the format of `tagKeys/{tag_key_id} -> tagValues/{tag_value_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## UpdateBackupScheduleRequest

The request for [`FirestoreAdmin.UpdateBackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.UpdateBackupSchedule) .

| Fields            |                                                                                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `backup_schedule` | [`BackupSchedule`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.BackupSchedule) Required. The backup schedule to update. |
| `update_mask`     | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) The list of fields to be updated.                                                                       |

## UpdateDatabaseMetadata

This type has no fields.

Metadata related to the update database operation.

## UpdateDatabaseRequest

The request for [`FirestoreAdmin.UpdateDatabase`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.UpdateDatabase) .

| Fields        |                                                                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`    | [`Database`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Database) Required. The database to update. |
| `update_mask` | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) The list of fields to be updated.                                                    |

## UpdateFieldRequest

The request for [`FirestoreAdmin.UpdateField`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.FirestoreAdmin.UpdateField) .

| Fields        |                                                                                                                                                                                                               |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field`       | [`Field`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.Field) Required. The field to be updated.                                            |
| `update_mask` | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) A mask, relative to the field. If specified, only configuration specified by this field_mask will be updated in the field. |

## UserCreds

A Cloud Firestore User Creds.

| Fields                                                                                                                            |                                                                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                            | `string` Identifier. The resource name of the UserCreds. Format: `projects/{project}/databases/{database}/userCreds/{user_creds}`                                                                                                       |
| `create_time`                                                                                                                     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time the user creds were created.                                                                                                    |
| `update_time`                                                                                                                     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time the user creds were last updated.                                                                                               |
| `state`                                                                                                                           | [`State`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds.State) Output only. Whether the user creds are enabled or disabled. Defaults to ENABLED on creation. |
| `secure_password`                                                                                                                 | `string` Output only. The plaintext server-generated password for the user creds. Only populated in responses for CreateUserCreds and ResetUserPassword.                                                                                |
| Union field `UserCredsIdentity` . Identity associated with this User Creds. `UserCredsIdentity` can be only one of the following: |                                                                                                                                                                                                                                         |
| `resource_identity`                                                                                                               | [`ResourceIdentity`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.admin.v1#google.firestore.admin.v1.UserCreds.ResourceIdentity) Resource Identity descriptor.                                           |

## ResourceIdentity

Describes a Resource Identity principal.

| Fields      |                                                                                                                   |
|-------------|-------------------------------------------------------------------------------------------------------------------|
| `principal` | `string` Output only. Principal identifier string. See: <https://cloud.google.com/iam/docs/principal-identifiers> |

## State

The state of the user creds (ENABLED or DISABLED).

| Enums               |                                        |
|---------------------|----------------------------------------|
| `STATE_UNSPECIFIED` | The default value. Should not be used. |
| `ENABLED`           | The user creds are enabled.            |
| `DISABLED`          | The user creds are disabled.           |

## WeeklyRecurrence

Represents a recurring schedule that runs on a specified day of the week.

The time zone is UTC.

| Fields |                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `day`  | [`DayOfWeek`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.type#google.type.DayOfWeek) The day of week to run. DAY_OF_WEEK_UNSPECIFIED is not allowed. |
