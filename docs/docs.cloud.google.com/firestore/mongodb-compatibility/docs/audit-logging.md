# Audit logging information

This document describes audit logging for Firestore with MongoDB compatibility. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources.

For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](https://cloud.google.com/logging/docs/audit#types)
  - [Audit log entry structure](https://cloud.google.com/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](https://cloud.google.com/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](https://cloud.google.com/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](https://cloud.google.com/logging/docs/audit/configure-data-access)

## Notes

When configuring audit logging, use the service name `  datastore.googleapis.com  ` to configure both `  datastore.googleapis.com  ` and `  firestore.googleapis.com. Once configured, logs for the Firestore with MongoDB compatibility API include the service name  ` firestore.googleapis.com\`.

To view the time it took to process a `  DATA_READ  ` or `  DATA_WRITE  ` request, see the `  processing_duration  ` field within the `  metadata  ` object of an `  AuditLog  ` . The `  processing_duration  ` field describes the time the database took to process a request. This is smaller than the end-user latency. In particular, it does not include network overhead.

## Service name

Firestore audit logs use the service name `  firestore.googleapis.com  ` . Filter for this service:

``` text
protoPayload.serviceName="firestore.googleapis.com"
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, Firestore generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method.

Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](https://cloud.google.com/logging/docs/audit/configure-data-access) audit logs.

Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](https://cloud.google.com/logging/docs/audit#admin-activity) audit logs.

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
<code dir="ltr" translate="no">       google.firestore.admin.v1.MongoDBCompatible.ListIndexes      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.MongoDBCompatible.ListDatabases      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.CreateIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteBackup      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.DeleteIndex      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.RestoreDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateBackupSchedule      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateDatabase      </code><br />
<code dir="ltr" translate="no">       google.firestore.admin.v1.FirestoreAdmin.UpdateField      </code><br />
<code dir="ltr" translate="no">       google.longrunning.Operations.CancelOperation      </code><br />
<code dir="ltr" translate="no">       google.longrunning.Operations.DeleteOperation      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATA_READ      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Find      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Aggregate      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.GetMore      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.ListCollections      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Count      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Distinct      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.CommitTransaction      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.AbortTransaction      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.EndSessions      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.KillCursors      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATA_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Insert      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Update      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.Delete      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.FindAndModify      </code><br />
<code dir="ltr" translate="no">       google.firestore.v1.MongoDBCompatible.CreateCollection      </code></td>
</tr>
</tbody>
</table>

## Identify request callers

Audit Log entries include information about the identity that performed the logged operation. To identify a request caller, see the following fields within an [`  AuditLog  `](https://cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) object:

  - The caller's identity is held in the [`  AuthenticationInfo  `](https://cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog#AuthenticationInfo) field. This can include the `  principalEmail  ` of the user. This information is [sometimes redacted](https://cloud.google.com/logging/docs/audit#user-id) .

  - The `  callerIp  ` field within the [`  requestMetadata  `](https://cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog#requestmetadata) object of an `  AuditLog  ` entry includes the IP address of the caller.
