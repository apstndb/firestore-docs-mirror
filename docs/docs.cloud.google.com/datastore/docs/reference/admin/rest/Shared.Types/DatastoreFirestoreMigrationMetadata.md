---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/DatastoreFirestoreMigrationMetadata
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/DatastoreFirestoreMigrationMetadata
title: DatastoreFirestoreMigrationMetadata
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/DatastoreFirestoreMigrationMetadata#SCHEMA_REPRESENTATION)

Metadata for Datastore to Firestore migration operations.

The DatastoreFirestoreMigration operation is not started by the end-user via an explicit "creation" method. This is an intentional deviation from the LRO design pattern.

This singleton resource can be accessed at: "projects/{projectId}/operations/datastore-firestore-migration"

**JSON representation**

```
{
  "migrationState": enum (MigrationState),
  "migrationStep": enum (MigrationStep)
}
```

| Fields           |                                                                                                                                                                                                                          |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `migrationState` | `enum ( `[`MigrationState`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationState)` )` The current state of migration from Cloud Datastore to Cloud Firestore in Datastore mode. |
| `migrationStep`  | `enum ( `[`MigrationStep`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStep)` )` The current step of migration from Cloud Datastore to Cloud Firestore in Datastore mode.    |
