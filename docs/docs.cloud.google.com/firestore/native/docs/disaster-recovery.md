# Plan disaster recovery

This page describes Firestore features that can help you create and implement disaster recovery plans.

## Disaster recovery planning for cloud infrastructure outages

To protect against potential cloud infrastructure disruptions in Google Cloud such as a zone or region experiencing an outage, Firestore replicates data across multiple replica databases.

The replication architecture depends on whether the database is in a regional location or a multi-region location. Regional databases synchronously replicate data across at least three zones. Multi-region databases synchronously replicate data across five zones in three regions with two serving regions and one witness region. Multi-region databases maximize the availability and durability of databases by providing 99.999% availability. Regional databases provide 99.99% availability.

Firestore automatically handles replication for you and doesn't require additional configuration or provisioning. For additional information, see the following:

For more information on the replication architecture, see [Architecting disaster recovery for cloud infrastructure outages](https://cloud.google.com/architecture/disaster-recovery#firestore) .

## Disaster recovery planning for data

To protect against data disasters like accidental deletion or modification of data, use scheduled backups and point-in-time recovery (PITR). Depending on your disaster recovery requirements, you might use both features together.

### Scheduled backups

Backups support a maximum retention period of 14 weeks. You can schedule daily or weekly backups. You can restore your database from a backup to a new Firestore database in the same project. For more details, see [Back up and restore data](/firestore/native/docs/backups) .

Backups provide a higher retention period than PITR. Restoring a database from a backup costs less than restoring a database from PITR data.

### Point-in-time recovery (PITR)

Enable PITR to read documents from a point in time up to seven days in the past. You can read data at a granularity level of 1 minute and surgically write back into the your database with a recovery time objective (maximum time for recovery) of 0. The recovery point objective (maximum possible data loss) is 1 minute. For more details, see [Point in time recovery](/firestore/native/docs/pitr) .

If you don't need to restore an entire database, PITR reads can recover only the data required. PITR reads also provide a lower recovery time objective and lower recovery point objective than backups.

#### Data exports

For data retention needs beyond 14 weeks, you can use PITR to create an export of your entire database and save this data in Cloud Storage indefinitely. A PITR data export captures data from a timestamp up to seven days in the past.

PITR data exports are useful for archiving data from your database. When compared to backups, recovering a database from a PITR export is generally more expensive than recovering the same data from a backup.

To start a PITR export operation, see [Export and import from PITR data](/firestore/native/docs/use-pitr#export-import) .

#### Database clone

You can recover data by cloning your database from a point in time in the past. If PITR is enabled, you can clone from up to seven days in the past. If PITR is not enabled, you can clone from up to one hour in the past.

To start a clone operation, see [Clone from a database](/firestore/native/docs/use-pitr#clone) .

## What's next

  - [Learn about backups](/firestore/native/docs/backups)
  - [Learn about PITR exports](/firestore/native/docs/pitr)
