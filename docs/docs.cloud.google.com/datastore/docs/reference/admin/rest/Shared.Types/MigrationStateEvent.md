---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStateEvent
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStateEvent
title: MigrationStateEvent
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStateEvent#SCHEMA_REPRESENTATION)

An event signifying a change in state of a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

**JSON representation**

```
{
  "state": enum (MigrationState)
}
```

| Fields  |                                                                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state` | `enum ( `[`MigrationState`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationState)` )` The new state of the migration. |
