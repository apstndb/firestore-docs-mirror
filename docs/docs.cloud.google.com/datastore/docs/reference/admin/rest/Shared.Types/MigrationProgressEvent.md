---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent
title: MigrationProgressEvent
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#SCHEMA_REPRESENTATION)
- [PrepareStepDetails](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#PrepareStepDetails)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#PrepareStepDetails.SCHEMA_REPRESENTATION)
- [RedirectWritesStepDetails](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#RedirectWritesStepDetails)
  - [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#RedirectWritesStepDetails.SCHEMA_REPRESENTATION)

An event signifying the start of a new step in a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

**JSON representation**

```
{
  "step": enum (MigrationStep),

  // Union field step_details can be only one of the following:
  "prepareStepDetails": {
    object (PrepareStepDetails)
  },
  "redirectWritesStepDetails": {
    object (RedirectWritesStepDetails)
  }
  // End of list of possible types for union field step_details.
}
```

| Fields                                                                                                 |                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `step`                                                                                                 | `enum ( `[`MigrationStep`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStep)` )` The step that is starting. An event with step set to `START` indicates that the migration has been reverted back to the initial pre-migration state. |
| Union field `step_details` . Details about this step. `step_details` can be only one of the following: |                                                                                                                                                                                                                                                                                   |
| `prepareStepDetails`                                                                                   | `object ( `[`PrepareStepDetails`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#PrepareStepDetails)` )` Details for the `PREPARE` step.                                                                                   |
| `redirectWritesStepDetails`                                                                            | `object ( `[`RedirectWritesStepDetails`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationProgressEvent#RedirectWritesStepDetails)` )` Details for the `REDIRECT_WRITES` step.                                                             |

## PrepareStepDetails

Details for the `PREPARE` step.

**JSON representation**

```
{
  "concurrencyMode": enum (ConcurrencyMode)
}
```

| Fields            |                                                                                                                                                                                                                          |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `concurrencyMode` | `enum ( `[`ConcurrencyMode`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ConcurrencyMode)` )` The concurrency mode this database will use when it reaches the `REDIRECT_WRITES` step. |

## RedirectWritesStepDetails

Details for the `REDIRECT_WRITES` step.

**JSON representation**

```
{
  "concurrencyMode": enum (ConcurrencyMode)
}
```

| Fields            |                                                                                                                                                                          |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `concurrencyMode` | `enum ( `[`ConcurrencyMode`](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/ConcurrencyMode)` )` The concurrency mode for this database. |
