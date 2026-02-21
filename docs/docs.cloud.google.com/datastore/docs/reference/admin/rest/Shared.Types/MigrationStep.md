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
