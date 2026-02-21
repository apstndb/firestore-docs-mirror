# Firestore audit logging information

This document describes audit logging for Firestore. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Notes

When configuring audit logging, use the service name `  datastore.googleapis.com  ` to configure both `  datastore.googleapis.com  ` and `  firestore.googleapis.com  ` .Once configured, logs for the Firestore API include the the service name `  firestore.googleapis.com  ` .  
  
To view the time it took to process a `  DATA_READ  ` or `  DATA_WRITE  ` request, see the `  processing_duration  ` field within the `  metadata  ` object of an `  AuditLog  ` . `  processing_duration  ` describes the time the database took to actually process a request. This is smaller than the end-user latency. In particular, it does not include network overhead.  
  
For [`  Listen  `](/firestore/docs/reference/rpc/google.firestore.v1#google.firestore.v1.Firestore.Listen) requests, `  processing_duration  ` is only present on the Audit Log for the initial result set returned. Its absent from subsequent Audit Logs for that same `  Listen  ` target.  
  
Individual writes from import, bulk delete operations and TTL are not audit logged.

## Service name

Firestore audit logs use the service name `  firestore.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="firestore.googleapis.com"
  
```

## Methods by permission type

Firestore also includes the following operations as part of the [Key Visualizer](/firestore/docs/key-visualizer) diagnostic tool. These are [Data Access](/logging/docs/audit#data-access) audit logs and have the service name `  firestorekeyvisualizer.googleapis.com  ` . They are enabled by turning on `  DATA_READ  ` for the `  firestore.googleapis.com  ` service.

  - `  google.cloud.keyvisualizer.KeyVisualizer.GetScan  `
  - `  google.cloud.keyvisualizer.KeyVisualizer.ListScans  `

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, Firestore generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](/logging/docs/audit/understanding-audit-logs#lro) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission type</th>
<th>Methods</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ADMIN_READ      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.location.Locations.GetLocation      </code><br />
<code dir="ltr" translate="no">       google.cloud.location.Locations.ListLocations      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.GetBackup      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.GetBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.GetDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.GetField      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.GetIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ListBackups      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ListDatabases      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ListFields      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ListIndexes      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.GetIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.ListIndexes      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.GetField      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.GetIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.ListFields      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.ListIndexes      </code><br />
<code dir="ltr" translate="no">       google.longrunning.Operations.GetOperation      </code><br />
<code dir="ltr" translate="no">       google.longrunning.Operations.ListOperations      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateIndex      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteBackup      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ExportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.ImportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.RestoreDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateField      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.CreateIndex      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.DeleteIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.ExportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta1.FirestoreAdmin.ImportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.CreateIndex      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.DeleteIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.ExportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.ImportDocuments      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.firestore.admin.v1beta2.FirestoreAdmin.UpdateField      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.longrunning.Operations.CancelOperation      </code><br />
<code dir="ltr" translate="no">       google.longrunning.Operations.DeleteOperation      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATA_READ      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.v1.Firestore.BatchGetDocuments      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.BeginTransaction      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.GetDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.ListCollectionIds      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.ListDocuments      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.Listen      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.PartitionQuery      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.Rollback      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.RunAggregationQuery      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.RunQuery      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.BatchGetDocuments      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.BatchWrite      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.BeginTransaction      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.GetDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.ListCollectionIds      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.ListDocuments      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.PartitionQuery      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.Rollback      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.RunAggregationQuery      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.RunQuery      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATA_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.v1.Firestore.BatchWrite      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.Commit      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.CreateDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.DeleteDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.UpdateDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.Firestore.Write      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.BatchWrite      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.Commit      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.CreateDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.DeleteDocument      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1beta1.Firestore.UpdateDocument      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for Firestore.

### `     google.cloud.location.Locations    `

The following audit logs are associated with methods belonging to `  google.cloud.location.Locations  ` .

#### `     GetLocation    `

  - **Method** : `  google.cloud.location.Locations.GetLocation  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.locations.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.location.Locations.GetLocation"  `  

#### `     ListLocations    `

  - **Method** : `  google.cloud.location.Locations.ListLocations  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.locations.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.location.Locations.ListLocations"  `  

### `     google.firestore.admin.v1.FirestoreAdmin    `

The following audit logs are associated with methods belonging to `  google.firestore.admin.v1.FirestoreAdmin  ` .

#### `     BulkDeleteDocuments    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.bulkDelete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.BulkDeleteDocuments"  `  

#### `     CreateBackupSchedule    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.CreateBackupSchedule  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.backupSchedules.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.CreateBackupSchedule"  `  

#### `     CreateDatabase    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.CreateDatabase  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.CreateDatabase"  `  

#### `     CreateIndex    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.CreateIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.CreateIndex"  `  

#### `     DeleteBackup    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.DeleteBackup  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.backups.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.DeleteBackup"  `  

#### `     DeleteBackupSchedule    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.DeleteBackupSchedule  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.backupSchedules.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.DeleteBackupSchedule"  `  

#### `     DeleteDatabase    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase"  `  

#### `     DeleteIndex    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.DeleteIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.DeleteIndex"  `  

#### `     ExportDocuments    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ExportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.export - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ExportDocuments"  `  

#### `     GetBackup    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.GetBackup  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.backups.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.GetBackup"  `  

#### `     GetBackupSchedule    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.GetBackupSchedule  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.backupSchedules.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.GetBackupSchedule"  `  

#### `     GetDatabase    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.GetDatabase  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.getMetadata - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.GetDatabase"  `  

#### `     GetField    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.GetField  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.GetField"  `  

#### `     GetIndex    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.GetIndex  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.GetIndex"  `  

#### `     ImportDocuments    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ImportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.import - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ImportDocuments"  `  

#### `     ListBackupSchedules    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.backupSchedules.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ListBackupSchedules"  `  

#### `     ListBackups    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ListBackups  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.backups.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ListBackups"  `  

#### `     ListDatabases    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ListDatabases  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ListDatabases"  `  

#### `     ListFields    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ListFields  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ListFields"  `  

#### `     ListIndexes    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.ListIndexes  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.ListIndexes"  `  

#### `     RestoreDatabase    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.RestoreDatabase  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.backups.restoreDatabase - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.RestoreDatabase"  `  

#### `     UpdateBackupSchedule    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.UpdateBackupSchedule  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.backupSchedules.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.UpdateBackupSchedule"  `  

#### `     UpdateDatabase    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.UpdateDatabase  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.UpdateDatabase"  `  

#### `     UpdateField    `

  - **Method** : `  google.firestore.admin.v1.FirestoreAdmin.UpdateField  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1.FirestoreAdmin.UpdateField"  `  

### `     google.firestore.admin.v1beta1.FirestoreAdmin    `

The following audit logs are associated with methods belonging to `  google.firestore.admin.v1beta1.FirestoreAdmin  ` .

#### `     CreateIndex    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.CreateIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.CreateIndex"  `  

#### `     DeleteIndex    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.DeleteIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.DeleteIndex"  `  

#### `     ExportDocuments    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.ExportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.export - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.ExportDocuments"  `  

#### `     GetIndex    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.GetIndex  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.GetIndex"  `  

#### `     ImportDocuments    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.ImportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.import - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.ImportDocuments"  `  

#### `     ListIndexes    `

  - **Method** : `  google.firestore.admin.v1beta1.FirestoreAdmin.ListIndexes  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta1.FirestoreAdmin.ListIndexes"  `  

### `     google.firestore.admin.v1beta2.FirestoreAdmin    `

The following audit logs are associated with methods belonging to `  google.firestore.admin.v1beta2.FirestoreAdmin  ` .

#### `     CreateIndex    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.CreateIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.CreateIndex"  `  

#### `     DeleteIndex    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.DeleteIndex  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.DeleteIndex"  `  

#### `     ExportDocuments    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.ExportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.export - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.ExportDocuments"  `  

#### `     GetField    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.GetField  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.GetField"  `  

#### `     GetIndex    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.GetIndex  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.GetIndex"  `  

#### `     ImportDocuments    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.ImportDocuments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.databases.import - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.ImportDocuments"  `  

#### `     ListFields    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.ListFields  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.ListFields"  `  

#### `     ListIndexes    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.ListIndexes  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.indexes.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.ListIndexes"  `  

#### `     UpdateField    `

  - **Method** : `  google.firestore.admin.v1beta2.FirestoreAdmin.UpdateField  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.indexes.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.admin.v1beta2.FirestoreAdmin.UpdateField"  `  

### `     google.firestore.v1.Firestore    `

The following audit logs are associated with methods belonging to `  google.firestore.v1.Firestore  ` .

#### `     BatchGetDocuments    `

  - **Method** : `  google.firestore.v1.Firestore.BatchGetDocuments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.BatchGetDocuments"  `  

#### `     BatchWrite    `

  - **Method** : `  google.firestore.v1.Firestore.BatchWrite  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.delete - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.BatchWrite"  `  

#### `     BeginTransaction    `

  - **Method** : `  google.firestore.v1.Firestore.BeginTransaction  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.BeginTransaction"  `  

#### `     Commit    `

  - **Method** : `  google.firestore.v1.Firestore.Commit  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.delete - DATA_WRITE  `
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.Commit"  `  

#### `     CreateDocument    `

  - **Method** : `  google.firestore.v1.Firestore.CreateDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.allocateIds - DATA_WRITE  `
      - `  datastore.entities.create - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.CreateDocument"  `  

#### `     DeleteDocument    `

  - **Method** : `  google.firestore.v1.Firestore.DeleteDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.delete - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.DeleteDocument"  `  

#### `     GetDocument    `

  - **Method** : `  google.firestore.v1.Firestore.GetDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.GetDocument"  `  

#### `     ListCollectionIds    `

  - **Method** : `  google.firestore.v1.Firestore.ListCollectionIds  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.ListCollectionIds"  `  

#### `     ListDocuments    `

  - **Method** : `  google.firestore.v1.Firestore.ListDocuments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.ListDocuments"  `  

#### `     Listen    `

  - **Method** : `  google.firestore.v1.Firestore.Listen  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : [**Streaming RPC**](/logging/docs/audit/understanding-audit-logs#streaming)  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.Listen"  `  

**Note:**

`  Listen  ` is a long-lived RPC that combines multiple streaming targets. Each target is a query or a set of document keys. The stream for each target includes an initial result set and a sequence of updates, additions, and removals to the result set. The targets are the relevant audit unit. Firestore audits each target as follows:

  - When the target is added, emit a log entry with the targets query or document key set. In these entries, [`  operation.first  `](/logging/docs/reference/v2/rest/v2/LogEntry#logentryoperation) is true. This audit log is **omitted** when the stream is a resumption of an earlier Listen target stream.
  - Emit periodic updates reporting the count of updates since the last audit log for this target.
  - Emit a log entry when the target is removed from the stream, either explicitly or due to the termination for the `  Listen  ` RPC. This log entry reports the count of updates since the last audit log for this target. In these entries, [`  operation.last  `](/logging/docs/reference/v2/rest/v2/LogEntry#logentryoperation) is true.
  - The emitted log entries use the same [`  operation.id  `](/logging/docs/reference/v2/rest/v2/LogEntry#logentryoperation) .

#### `     PartitionQuery    `

  - **Method** : `  google.firestore.v1.Firestore.PartitionQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.PartitionQuery"  `  

#### `     Rollback    `

  - **Method** : `  google.firestore.v1.Firestore.Rollback  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.Rollback"  `  

#### `     RunAggregationQuery    `

  - **Method** : `  google.firestore.v1.Firestore.RunAggregationQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.RunAggregationQuery"  `  

#### `     RunQuery    `

  - **Method** : `  google.firestore.v1.Firestore.RunQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.RunQuery"  `  

**Note:** `  RunQuery  ` is a short-lived streaming RPC and emits a log entry when the last message (document) is sent.

#### `     UpdateDocument    `

  - **Method** : `  google.firestore.v1.Firestore.UpdateDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.UpdateDocument"  `  

#### `     Write    `

  - **Method** : `  google.firestore.v1.Firestore.Write  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1.Firestore.Write"  `  

**Note:** `  Write  ` emits a log entry for every message received as each message corresponds to an independent write to the database. The emitted log entries use the same [`  operation.id  `](/logging/docs/reference/v2/rest/v2/LogEntry#logentryoperation) .

### `     google.firestore.v1beta1.Firestore    `

The following audit logs are associated with methods belonging to `  google.firestore.v1beta1.Firestore  ` .

#### `     BatchGetDocuments    `

  - **Method** : `  google.firestore.v1beta1.Firestore.BatchGetDocuments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
      - `  datastore.entities.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.BatchGetDocuments"  `  

#### `     BatchWrite    `

  - **Method** : `  google.firestore.v1beta1.Firestore.BatchWrite  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.BatchWrite"  `  

#### `     BeginTransaction    `

  - **Method** : `  google.firestore.v1beta1.Firestore.BeginTransaction  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.BeginTransaction"  `  

#### `     Commit    `

  - **Method** : `  google.firestore.v1beta1.Firestore.Commit  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.delete - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.Commit"  `  

#### `     CreateDocument    `

  - **Method** : `  google.firestore.v1beta1.Firestore.CreateDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.allocateIds - DATA_WRITE  `
      - `  datastore.entities.create - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.CreateDocument"  `  

#### `     DeleteDocument    `

  - **Method** : `  google.firestore.v1beta1.Firestore.DeleteDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.delete - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.DeleteDocument"  `  

#### `     GetDocument    `

  - **Method** : `  google.firestore.v1beta1.Firestore.GetDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.GetDocument"  `  

#### `     ListCollectionIds    `

  - **Method** : `  google.firestore.v1beta1.Firestore.ListCollectionIds  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.ListCollectionIds"  `  

#### `     ListDocuments    `

  - **Method** : `  google.firestore.v1beta1.Firestore.ListDocuments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.ListDocuments"  `  

#### `     PartitionQuery    `

  - **Method** : `  google.firestore.v1beta1.Firestore.PartitionQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.PartitionQuery"  `  

#### `     Rollback    `

  - **Method** : `  google.firestore.v1beta1.Firestore.Rollback  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.databases.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.Rollback"  `  

#### `     RunAggregationQuery    `

  - **Method** : `  google.firestore.v1beta1.Firestore.RunAggregationQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.RunAggregationQuery"  `  

#### `     RunQuery    `

  - **Method** : `  google.firestore.v1beta1.Firestore.RunQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.get - DATA_READ  `
      - `  datastore.entities.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.RunQuery"  `  

**Note:** `  RunQuery  ` is a short-lived streaming RPC and emits a log entry when the last message (document) is sent.

#### `     UpdateDocument    `

  - **Method** : `  google.firestore.v1beta1.Firestore.UpdateDocument  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.entities.create - DATA_WRITE  `
      - `  datastore.entities.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.firestore.v1beta1.Firestore.UpdateDocument"  `  

### `     google.longrunning.Operations    `

The following audit logs are associated with methods belonging to `  google.longrunning.Operations  ` .

#### `     CancelOperation    `

  - **Method** : `  google.longrunning.Operations.CancelOperation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.operations.cancel - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.longrunning.Operations.CancelOperation"  `  

#### `     DeleteOperation    `

  - **Method** : `  google.longrunning.Operations.DeleteOperation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  datastore.operations.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.longrunning.Operations.DeleteOperation"  `  

#### `     GetOperation    `

  - **Method** : `  google.longrunning.Operations.GetOperation  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.operations.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.longrunning.Operations.GetOperation"  `  

#### `     ListOperations    `

  - **Method** : `  google.longrunning.Operations.ListOperations  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  datastore.operations.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.longrunning.Operations.ListOperations"  `  

## Identify request callers

Audit Log entries include information about the identity that performed the logged operation. To identify a request caller, see the following fields within an [`  AuditLog  `](/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) object:

  - The caller's identity is held in the [`  AuthenticationInfo  `](/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog#AuthenticationInfo) field. This can include the `  principalEmail  ` of the user. This information is [sometimes redacted](/logging/docs/audit#user-id) .
    
    If a JSON Web Token (JWT) was used for third-party authentication, the `  thirdPartyPrincipal  ` field includes the token's header and payload. For example, audit logs for requests authenticated with [Firebase Authentication](https://firebase.google.com/docs/auth) include that request's [auth token](https://firebase.google.com/docs/auth/users#auth_tokens) .

  - The `  callerIp  ` field within the [`  requestMetadata  `](/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog#requestmetadata) object of an `  AuditLog  ` entry includes the IP address of the caller.
