## Resource: Database

A Cloud Firestore Database.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;uid&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;deleteTime&quot;: string,
  &quot;locationId&quot;: string,
  &quot;type&quot;: enum (DatabaseType),
  &quot;concurrencyMode&quot;: enum (ConcurrencyMode),
  &quot;versionRetentionPeriod&quot;: string,
  &quot;earliestVersionTime&quot;: string,
  &quot;pointInTimeRecoveryEnablement&quot;: enum (PointInTimeRecoveryEnablement),
  &quot;appEngineIntegrationMode&quot;: enum (AppEngineIntegrationMode),
  &quot;keyPrefix&quot;: string,
  &quot;deleteProtectionState&quot;: enum (DeleteProtectionState),
  &quot;cmekConfig&quot;: {
    object (CmekConfig)
  },
  &quot;previousId&quot;: string,
  &quot;sourceInfo&quot;: {
    object (SourceInfo)
  },
  &quot;tags&quot;: {
    string: string,
    ...
  },
  &quot;etag&quot;: string,
  &quot;databaseEdition&quot;: enum (DatabaseEdition),
  &quot;realtimeUpdatesMode&quot;: enum (RealtimeUpdatesMode),
  &quot;firestoreDataAccessMode&quot;: enum (DataAccessMode),
  &quot;mongodbCompatibleDataAccessMode&quot;: enum (DataAccessMode),
  &quot;freeTier&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

The resource name of the Database. Format: `  projects/{project}/databases/{database}  `

`  uid  `

`  string  `

Output only. The system-generated UUID4 for this Database.

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The timestamp at which this database was created. Databases created before 2016 do not populate createTime.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. The timestamp at which this database was most recently updated. Note this only includes updates to the database resource and not data contained by the database.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  deleteTime  `

`  string ( Timestamp  ` format)

Output only. The timestamp at which this database was deleted. Only set if the database has been deleted.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  locationId  `

`  string  `

The location of the database. Available locations are listed at <https://cloud.google.com/firestore/docs/locations> .

`  type  `

`  enum ( DatabaseType  ` )

The type of the database. See <https://cloud.google.com/datastore/docs/firestore-or-datastore> for information about how to choose.

`  concurrencyMode  `

`  enum ( ConcurrencyMode  ` )

The concurrency control mode to use for this database.

If unspecified in a databases.create request, this will default based on the database edition: Optimistic for Enterprise and Pessimistic for all other databases.

`  versionRetentionPeriod  `

`  string ( Duration  ` format)

Output only. The period during which past versions of data are retained in the database.

Any `  read  ` or `  query  ` can specify a `  readTime  ` within this window, and will read the state of the database at that time.

If the PITR feature is enabled, the retention period is 7 days. Otherwise, the retention period is 1 hour.

A duration in seconds with up to nine fractional digits, ending with ' `  s  ` '. Example: `  "3.5s"  ` .

`  earliestVersionTime  `

`  string ( Timestamp  ` format)

Output only. The earliest timestamp at which older versions of the data can be read from the database. See \[versionRetentionPeriod\] above; this field is populated with `  now - versionRetentionPeriod  ` .

This value is continuously updated, and becomes stale the moment it is queried. If you are using this value to recover data, make sure to account for the time from the moment when the value is queried to the moment when you initiate the recovery.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  pointInTimeRecoveryEnablement  `

`  enum ( PointInTimeRecoveryEnablement  ` )

Whether to enable the PITR feature on this database.

`  appEngineIntegrationMode  `

`  enum ( AppEngineIntegrationMode  ` )

The App Engine integration mode to use for this database.

`  keyPrefix  `

`  string  `

Output only. The keyPrefix for this database. This keyPrefix is used, in combination with the project ID (" \~ ") to construct the application ID that is returned from the Cloud Datastore APIs in Google App Engine first generation runtimes.

This value may be empty in which case the appid to use for URL-encoded keys is the projectId (eg: foo instead of v\~foo).

`  deleteProtectionState  `

`  enum ( DeleteProtectionState  ` )

State of delete protection for the database.

`  cmekConfig  `

`  object ( CmekConfig  ` )

Optional. Presence indicates CMEK is enabled for this database.

`  previousId  `

`  string  `

Output only. The database resource's prior database ID. This field is only populated for deleted databases.

`  sourceInfo  `

`  object ( SourceInfo  ` )

Output only. Information about the provenance of this database.

`  tags  `

`  map (key: string, value: string)  `

Optional. Input only. Immutable. Tag keys/values directly bound to this resource. For example: "123/environment": "production", "123/costCenter": "marketing"

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  etag  `

`  string  `

This checksum is computed by the server based on the value of other fields, and may be sent on update and delete requests to ensure the client has an up-to-date value before proceeding.

`  databaseEdition  `

`  enum ( DatabaseEdition  ` )

Immutable. The edition of the database.

`  realtimeUpdatesMode  `

`  enum ( RealtimeUpdatesMode  ` )

Immutable. The default Realtime Updates mode to use for this database.

`  firestoreDataAccessMode  `

`  enum ( DataAccessMode  ` )

Optional. The Firestore API data access mode to use for this database. If not set on write: - the default value is DATA\_ACCESS\_MODE\_DISABLED for Enterprise Edition. - the default value is DATA\_ACCESS\_MODE\_ENABLED for Standard Edition.

`  mongodbCompatibleDataAccessMode  `

`  enum ( DataAccessMode  ` )

Optional. The MongoDB compatible API data access mode to use for this database. If not set on write, the default value is DATA\_ACCESS\_MODE\_ENABLED for Enterprise Edition. The value is always DATA\_ACCESS\_MODE\_DISABLED for Standard Edition.

`  freeTier  `

`  boolean  `

Output only. Background: Free tier is the ability of a Firestore database to use a small amount of resources every day without being charged. Once usage exceeds the free tier limit further usage is charged.

Whether this database can make use of the free tier. Only one database per project can be eligible for the free tier.

The first (or next) database that is created in a project without a free tier database will be marked as eligible for the free tier. Databases that are created while there is a free tier database will not be eligible for the free tier.

## DatabaseType

The type of the database. See <https://cloud.google.com/datastore/docs/firestore-or-datastore> for information about how to choose.

Mode changes are only allowed if the database is empty.

Enums

`  DATABASE_TYPE_UNSPECIFIED  `

Not used.

`  FIRESTORE_NATIVE  `

Firestore Native Mode

`  DATASTORE_MODE  `

Firestore in Datastore Mode.

## ConcurrencyMode

The type of concurrency control mode for transactions.

Enums

`  CONCURRENCY_MODE_UNSPECIFIED  `

Not used.

`  OPTIMISTIC  `

Use optimistic concurrency control by default. This mode is available for Cloud Firestore databases.

This is the default setting for Cloud Firestore Enterprise Edition databases.

`  PESSIMISTIC  `

Use pessimistic concurrency control by default. This mode is available for Cloud Firestore databases.

This is the default setting for Cloud Firestore Standard Edition databases.

`  OPTIMISTIC_WITH_ENTITY_GROUPS  `

Use optimistic concurrency control with entity groups by default.

This mode is enabled for some databases that were automatically upgraded from Cloud Datastore to Cloud Firestore with Datastore Mode.

It is not recommended for any new databases, and not supported for Firestore Native databases.

## PointInTimeRecoveryEnablement

Point In Time Recovery feature enablement.

Enums

`  POINT_IN_TIME_RECOVERY_ENABLEMENT_UNSPECIFIED  `

Not used.

`  POINT_IN_TIME_RECOVERY_ENABLED  `

Reads are supported on selected versions of the data from within the past 7 days:

  - Reads against any timestamp within the past hour
  - Reads against 1-minute snapshots beyond 1 hour and within 7 days

`  versionRetentionPeriod  ` and `  earliestVersionTime  ` can be used to determine the supported versions.

`  POINT_IN_TIME_RECOVERY_DISABLED  `

Reads are supported on any version of the data from within the past 1 hour.

## AppEngineIntegrationMode

The type of App Engine integration mode.

Enums

`  APP_ENGINE_INTEGRATION_MODE_UNSPECIFIED  `

Not used.

`  ENABLED  `

If an App Engine application exists in the same region as this database, App Engine configuration will impact this database. This includes disabling of the application & database, as well as disabling writes to the database.

`  DISABLED  `

App Engine has no effect on the ability of this database to serve requests.

This is the default setting for databases created with the Firestore API.

## DeleteProtectionState

The delete protection state of the database.

Enums

`  DELETE_PROTECTION_STATE_UNSPECIFIED  `

The default value. Delete protection type is not specified

`  DELETE_PROTECTION_DISABLED  `

Delete protection is disabled

`  DELETE_PROTECTION_ENABLED  `

Delete protection is enabled

## CmekConfig

The CMEK (Customer Managed Encryption Key) configuration for a Firestore database. If not present, the database is secured by the default Google encryption key.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kmsKeyName&quot;: string,
  &quot;activeKeyVersion&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kmsKeyName  `

`  string  `

Required. Only keys in the same location as this database are allowed to be used for encryption.

For Firestore's nam5 multi-region, this corresponds to Cloud KMS multi-region us. For Firestore's eur3 multi-region, this corresponds to Cloud KMS multi-region europe. See <https://cloud.google.com/kms/docs/locations> .

The expected format is `  projects/{projectId}/locations/{kms_location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}  ` .

`  activeKeyVersion[]  `

`  string  `

Output only. Currently in-use [KMS key versions](https://cloud.google.com/kms/docs/resource-hierarchy#key_versions) . During [key rotation](https://cloud.google.com/kms/docs/key-rotation) , there can be multiple in-use key versions.

The expected format is `  projects/{projectId}/locations/{kms_location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}/cryptoKeyVersions/{key_version}  ` .

## SourceInfo

Information about the provenance of this database.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;operation&quot;: string,

  // Union field source can be only one of the following:
  &quot;backup&quot;: {
    object (BackupSource)
  }
  // End of list of possible types for union field source.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  operation  `

`  string  `

The associated long-running operation. This field may not be set after the operation has completed. Format: `  projects/{project}/databases/{database}/operations/{operation}  ` .

Union field `  source  ` . The source from which this database is derived. `  source  ` can be only one of the following:

`  backup  `

`  object ( BackupSource  ` )

If set, this database was restored from the specified backup (or a snapshot thereof).

## BackupSource

Information about a backup that was used to restore a database.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;backup&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  backup  `

`  string  `

The resource name of the backup that was used to restore this database. Format: `  projects/{project}/locations/{location}/backups/{backup}  ` .

## DatabaseEdition

The edition of the database.

Enums

`  DATABASE_EDITION_UNSPECIFIED  `

Not used.

`  STANDARD  `

Standard edition.

This is the default setting if not specified.

`  ENTERPRISE  `

Enterprise edition.

## RealtimeUpdatesMode

The Realtime Updates mode.

Enums

`  REALTIME_UPDATES_MODE_UNSPECIFIED  `

The Realtime Updates feature is not specified.

`  REALTIME_UPDATES_MODE_ENABLED  `

The Realtime Updates feature is enabled by default.

This could potentially degrade write performance for the database.

`  REALTIME_UPDATES_MODE_DISABLED  `

The Realtime Updates feature is disabled by default.

## DataAccessMode

The data access mode.

Enums

`  DATA_ACCESS_MODE_UNSPECIFIED  `

Not Used.

`  DATA_ACCESS_MODE_ENABLED  `

Accessing the database through the API is allowed.

`  DATA_ACCESS_MODE_DISABLED  `

Accessing the database through the API is disallowed.

## Methods

### `             bulkDeleteDocuments           `

Bulk deletes a subset of documents from Google Cloud Firestore.

### `             clone           `

Creates a new database by cloning an existing one.

### `             create           `

Create a database.

### `             delete           `

Deletes a database.

### `             exportDocuments           `

Exports a copy of all or a subset of documents from Google Cloud Firestore to another storage system, such as Google Cloud Storage.

### `             get           `

Gets information about a database.

### `             importDocuments           `

Imports documents into Google Cloud Firestore.

### `             list           `

List all the databases in the project.

### `             patch           `

Updates a database.

### `             restore           `

Creates a new database by restoring from an existing backup.
