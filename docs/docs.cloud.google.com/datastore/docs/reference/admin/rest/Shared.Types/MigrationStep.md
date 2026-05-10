---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStep
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/MigrationStep
title: MigrationStep
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

Steps in a migration.

Enums

`MIGRATION_STEP_UNSPECIFIED`

Unspecified.

`PREPARE`

Pre-migration: the database is prepared for migration.

`START`

Start of migration.

`APPLY_WRITES_SYNCHRONOUSLY`

Writes are applied synchronously to at least one replica.

`COPY_AND_VERIFY`

Data is copied to Cloud Firestore and then verified to match the data in Cloud Datastore.

`REDIRECT_EVENTUALLY_CONSISTENT_READS`

Eventually-consistent reads are redirected to Cloud Firestore.

`REDIRECT_STRONGLY_CONSISTENT_READS`

Strongly-consistent reads are redirected to Cloud Firestore.

`REDIRECT_WRITES`

Writes are redirected to Cloud Firestore.
