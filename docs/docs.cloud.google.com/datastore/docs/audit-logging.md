---
name: documents/docs.cloud.google.com/datastore/docs/audit-logging
uri: https://docs.cloud.google.com/datastore/docs/audit-logging
title: Datastore audit logging
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

This document lists the audited methods for Datastore. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

- [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types)
- [Audit log entry structure](https://docs.cloud.google.com/logging/docs/audit#audit_log_entry_structure)
- [Storing and routing audit logs](https://docs.cloud.google.com/logging/docs/audit#storing_and_routing_audit_logs)
- [Cloud Logging pricing summary](https://docs.cloud.google.com/stackdriver/pricing#logs-pricing-summary)
- [Enable Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit/configure-data-access)

## Notes

When configuring audit logging, the service name `datastore.googleapis.com` configures logs for both `datastore.googleapis.com` and `firestore.googleapis.com` API calls.  
  
To view the time it took to process a `DATA_READ` or `DATA_WRITE` request, see the `processing_duration` field within the `metadata` object of an [`AuditLog`](https://docs.cloud.google.com/reference/audit/auditlog/rest/Shared.Types/AuditLog) . `processing_duration` describes the time the database took to actually process a request. This is smaller than the end-user latency. In particular, it does not include network overhead.

## Service name

To view the Datastore audit logs, do the following:

1.  In the Google Cloud console, go to the Logs Explorer page:

2.  Copy and paste the following query into the **Query** field of the Logs Explorer, and then click **Run query** .

    ```
    protoPayload.serviceName="datastore.googleapis.com"
    ```

## Methods by permission type

Each IAM permission has a `type` property, whose value is an enum that can be one of four values: `ADMIN_READ` , `ADMIN_WRITE` , `DATA_READ` , or `DATA_WRITE` . When you call a method, Datastore generates an audit log whose category is dependent on the `type` property of the permission required to perform the method. Methods that require an IAM permission with the `type` property value of `DATA_READ` , `DATA_WRITE` , or `ADMIN_READ` generate [Data Access](https://docs.cloud.google.com/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `type` property value of `ADMIN_WRITE` generate [Admin Activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro) .

| Permission type | Methods                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ADMIN_READ`    | `google.datastore.admin.v1.DatastoreAdmin.GetIndex` `google.datastore.admin.v1.DatastoreAdmin.ListIndexes` `google.longrunning.Operations.GetOperation` `google.longrunning.Operations.ListOperations`                                                                                                                                                                                                                                                                                        |
| `ADMIN_WRITE`   | `google.datastore.admin.v1.DatastoreAdmin.CreateIndex` (LRO) `google.datastore.admin.v1.DatastoreAdmin.DeleteIndex` `google.datastore.admin.v1.DatastoreAdmin.ExportEntities` (LRO) `google.datastore.admin.v1.DatastoreAdmin.ImportEntities` (LRO) `google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities` (LRO) `google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities` (LRO) `google.longrunning.Operations.CancelOperation` `google.longrunning.Operations.DeleteOperation` |
| `DATA_READ`     | `google.datastore.v1.Datastore.BeginTransaction` `google.datastore.v1.Datastore.Lookup` `google.datastore.v1.Datastore.Rollback` `google.datastore.v1.Datastore.RunAggregationQuery` `google.datastore.v1.Datastore.RunQuery` `google.datastore.v1beta3.Datastore.BeginTransaction` `google.datastore.v1beta3.Datastore.Lookup` `google.datastore.v1beta3.Datastore.Rollback` `google.datastore.v1beta3.Datastore.RunAggregationQuery` `google.datastore.v1beta3.Datastore.RunQuery`          |
| `DATA_WRITE`    | `google.datastore.v1.Datastore.AllocateIds` `google.datastore.v1.Datastore.Commit` `google.datastore.v1.Datastore.ReserveIds` `google.datastore.v1beta3.Datastore.AllocateIds` `google.datastore.v1beta3.Datastore.Commit` `google.datastore.v1beta3.Datastore.ReserveIds`                                                                                                                                                                                                                    |

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for Datastore.

### `google.datastore.admin.v1.DatastoreAdmin`

The following audit logs are associated with methods belonging to `google.datastore.admin.v1.DatastoreAdmin` .

#### `CreateIndex`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.CreateIndex`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.CreateIndex)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.indexes.create - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.CreateIndex"`  

#### `DeleteIndex`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.DeleteIndex`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.DeleteIndex)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.indexes.delete - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.DeleteIndex"`  

#### `ExportEntities`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.ExportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.ExportEntities)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.databases.export - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.ExportEntities"`  

#### `GetIndex`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.GetIndex`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.GetIndex)  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.indexes.get - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.GetIndex"`  

#### `ImportEntities`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.ImportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.ImportEntities)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.databases.import - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.ImportEntities"`  

#### `ListIndexes`

- **Method** : [`google.datastore.admin.v1.DatastoreAdmin.ListIndexes`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.DatastoreAdmin.ListIndexes)  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.indexes.list - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1.DatastoreAdmin.ListIndexes"`  

### `google.datastore.admin.v1beta1.DatastoreAdmin`

The following audit logs are associated with methods belonging to `google.datastore.admin.v1beta1.DatastoreAdmin` .

#### `ExportEntities`

- **Method** : [`google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.databases.export - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1beta1.DatastoreAdmin.ExportEntities"`  

#### `ImportEntities`

- **Method** : [`google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1beta1#google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.databases.import - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.datastore.admin.v1beta1.DatastoreAdmin.ImportEntities"`  

### `google.datastore.v1.Datastore`

The following audit logs are associated with methods belonging to `google.datastore.v1.Datastore` .

#### `AllocateIds`

- **Method** : `google.datastore.v1.Datastore.AllocateIds`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.allocateIds - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.AllocateIds"`  

#### `BeginTransaction`

- **Method** : `google.datastore.v1.Datastore.BeginTransaction`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.databases.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.BeginTransaction"`  

#### `Commit`

- **Method** : `google.datastore.v1.Datastore.Commit`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.databases.get - DATA_READ`
  - `datastore.entities.create - DATA_WRITE`
  - `datastore.entities.delete - DATA_WRITE`
  - `datastore.entities.update - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.Commit"`  

#### `Lookup`

- **Method** : `google.datastore.v1.Datastore.Lookup`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.Lookup"`  

#### `ReserveIds`

- **Method** : `google.datastore.v1.Datastore.ReserveIds`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.allocateIds - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.ReserveIds"`  

#### `Rollback`

- **Method** : `google.datastore.v1.Datastore.Rollback`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.databases.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.Rollback"`  

#### `RunAggregationQuery`

- **Method** : `google.datastore.v1.Datastore.RunAggregationQuery`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
  - `datastore.entities.list - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.RunAggregationQuery"`  

#### `RunQuery`

- **Method** : `google.datastore.v1.Datastore.RunQuery`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
  - `datastore.entities.list - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1.Datastore.RunQuery"`  

### `google.datastore.v1beta3.Datastore`

The following audit logs are associated with methods belonging to `google.datastore.v1beta3.Datastore` .

#### `AllocateIds`

- **Method** : `google.datastore.v1beta3.Datastore.AllocateIds`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.allocateIds - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.AllocateIds"`  

#### `BeginTransaction`

- **Method** : `google.datastore.v1beta3.Datastore.BeginTransaction`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.databases.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.BeginTransaction"`  

#### `Commit`

- **Method** : `google.datastore.v1beta3.Datastore.Commit`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.create - DATA_WRITE`
  - `datastore.entities.update - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.Commit"`  

#### `Lookup`

- **Method** : `google.datastore.v1beta3.Datastore.Lookup`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.Lookup"`  

#### `ReserveIds`

- **Method** : `google.datastore.v1beta3.Datastore.ReserveIds`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.allocateIds - DATA_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.ReserveIds"`  

#### `Rollback`

- **Method** : `google.datastore.v1beta3.Datastore.Rollback`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.databases.get - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.Rollback"`  

#### `RunAggregationQuery`

- **Method** : `google.datastore.v1beta3.Datastore.RunAggregationQuery`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
  - `datastore.entities.list - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.RunAggregationQuery"`  

#### `RunQuery`

- **Method** : `google.datastore.v1beta3.Datastore.RunQuery`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.entities.get - DATA_READ`
  - `datastore.entities.list - DATA_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.datastore.v1beta3.Datastore.RunQuery"`  

### `google.longrunning.Operations`

The following audit logs are associated with methods belonging to `google.longrunning.Operations` .

#### `CancelOperation`

- **Method** : [`google.longrunning.Operations.CancelOperation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operations.CancelOperation)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.operations.cancel - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.CancelOperation"`  

#### `DeleteOperation`

- **Method** : [`google.longrunning.Operations.DeleteOperation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operations.DeleteOperation)  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `datastore.operations.delete - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.DeleteOperation"`  

#### `GetOperation`

- **Method** : [`google.longrunning.Operations.GetOperation`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operations.GetOperation)  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.operations.get - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.GetOperation"`  

#### `ListOperations`

- **Method** : [`google.longrunning.Operations.ListOperations`](https://docs.cloud.google.com/datastore/docs/reference/admin/rpc/google.longrunning#google.longrunning.Operations.ListOperations)  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `datastore.operations.list - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.ListOperations"`  

## Methods that don't produce audit logs

A method might not produce audit logs for one or more of the following reasons:

- It is a high volume method involving significant log generation and storage costs.
- It has low auditing value.
- Another audit or platform log already provides method coverage.

The following methods don't produce audit logs:

- `google.longrunning.Operations.WaitOperation`
