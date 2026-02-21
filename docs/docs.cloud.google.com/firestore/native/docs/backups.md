# Back up and restore data

This page describes how to use the Firestore scheduled backups feature. Use backups to protect your data from application-level data corruption or from accidental data deletion.

Backups let you configure backup schedules to take daily or weekly backups of the specified database. You can then use these backups to restore data to a new database.

## About backups

A backup is a consistent copy of the database at a point in time. The backup contains all data and index configurations at that point in time.

A backup does not contain database [time to live policies](/firestore/native/docs/ttl) or [Firebase Security Rules.](/firestore/docs/security/get-started) A backup resides in the same location as the source database.

Backups have a configurable retention period and are stored until the retention period expires or until you delete the backup. Deleting the source database does not automatically delete related backups.

Firestore stores metadata related to backups and backup schedules related to a database. Firestore retains this metadata until **all** backups for the database expire or are deleted.

Creating or retaining backups does not affect the performance of reads or writes in your live database.

## Costs

When you use backups, you're charged for the following:

  - The amount of storage used by each backup.
  - For a restore operation, you're charged based on the size of the backup.

For more details and exact rates, see the [Pricing](/firestore/pricing) page.

## Before you begin

Make sure that billing is enabled for your Google Cloud project. Learn how to [check if billing is enabled on a project](/billing/docs/how-to/verify-billing-enabled) .

### Required roles

To get the permissions that you need to manage backups and backup schedules, ask your administrator to grant you one or more of the following Identity and Access Management roles:

  - `  roles/datastore.owner  ` : Full access to the Firestore database
  - `  roles/datastore.backupsAdmin  ` : Read and write access to backups
  - `  roles/datastore.backupsViewer  ` : Read access to backups
  - `  roles/datastore.backupSchedulesAdmin  ` : Read and write access to backup schedules
  - `  roles/datastore.backupSchedulesViewer  ` : Read access to backup schedules
  - `  roles/datastore.restoreAdmin  ` : Permissions to initiate restore operations

## Create and manage backup schedules

The following examples demonstrate how to set up a backup schedule. For each database, you can configure up to one daily backup schedule and up to one weekly backup schedule. You cannot configure multiple weekly backups schedules for different days of the week.

You cannot configure the exact time of day of the backup. Backups are taken at different times each day. For weekly backup schedules, you can configure the day of the week to take a backup.

### Create a backup schedule

Use one of the following tools to create a backup schedule.

#### Create a daily backup schedule

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  Click **Edit** to edit disaster recovery settings.

4.  Select the **Daily** checkbox, set the retention period, and then click **Save** .

##### gcloud

To create a backup schedule for a database, use the [`  gcloud firestore backups schedules create  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/schedules/create) command. To create a daily backup schedule, set the `  --recurrence  ` flag to `  daily  ` :

``` bash
gcloud firestore backups schedules create \
--database='DATABASE_ID' \
--recurrence=daily \
--retention=RETENTION_PERIOD
```

Replace the following:

  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - RETENTION\_PERIOD : Set this to a value up to 14 weeks ( `  14w  ` ).

##### Terraform

To create a daily backup schedule, create a `  google_firestore_backup_schedule  ` resource.

``` text
resource "google_firestore_backup_schedule" "daily-backup" {
  project  = PROJECT_ID
  database = DATABASE_ID

  retention = RETENTION_PERIOD_SECONDS

  daily_recurrence {}
}
```

Replace the following:

  - PROJECT\_ID : The ID of the project.
  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - RETENTION\_PERIOD\_SECONDS : Set this to a value in seconds, followed by "s". The maximum value is `  8467200s  ` (14 weeks).

#### Create a weekly backup schedule

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  Click **Edit** to edit disaster recovery settings.

4.  Select the **Weekly** checkbox, select a backup day, set the retention period, and then click **Save** .

##### gcloud

To create a weekly backup schedule, set the `  --recurrence  ` flag to `  weekly  ` :

``` bash
gcloud firestore backups schedules create \
--database='DATABASE_ID' \
--recurrence=weekly \
--retention=RETENTION_PERIOD \
--day-of-week=DAY
```

Replace the following:

  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - RETENTION\_PERIOD : Set this to a value up to 14 weeks ( `  14w  ` ).
  - DAY : The day of the week to take the backup. Set to one of the following:
      - `  SUN  ` for Sunday
      - `  MON  ` for Monday
      - `  TUE  ` for Tuesday
      - `  WED  ` for Wednesday
      - `  THU  ` for Thursday
      - `  FRI  ` for Friday
      - `  SAT  ` for Saturday

##### Terraform

To create a weekly backup schedule, create a `  google_firestore_backup_schedule  ` resource.

``` text
resource "google_firestore_backup_schedule" "weekly-backup" {
  project  = PROJECT_ID
  database = DATABASE_ID

  retention = RETENTION_PERIOD_SECONDS

  weekly_recurrence {
    day = DAY
  }
}
```

Replace the following:

  - PROJECT\_ID : The ID of the project.
  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - RETENTION\_PERIOD\_SECONDS : Set this to a value in seconds, followed by "s". The maximum value is `  8467200s  ` (14 weeks).
  - DAY : The day of the week to take the backup. Set to one of the following:
      - `  SUNDAY  ` for Sunday
      - `  MONDAY  ` for Monday
      - `  TUESDAY  ` for Tuesday
      - `  WEDNESDAY  ` for Wednesday
      - `  THURSDAY  ` for Thursday
      - `  FRIDAY  ` for Friday
      - `  SATURDAY  ` for Saturday

### List backup schedules

To list all backup schedules for a database, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  The **Disaster recovery** page opens. This page describes backup schedules and lists available backups.

##### gcloud

Use the [`  gcloud firestore backups schedules list  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/schedules/list) command.

``` bash
gcloud firestore backups schedules list \
--database='DATABASE_ID'
```

Replace DATABASE\_ID with the ID of the database. Use `  '(default)'  ` for the default database.

### Describe backup schedule

To retrieve information about a backup schedule, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  The **Disaster recovery** page opens. This page describes backup schedules and lists available backups.

##### gcloud

Use the [`  gcloud firestore backups schedules describe  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/schedules/describe) command:

``` bash
gcloud firestore backups schedules describe \
--database='DATABASE_ID' \
--backup-schedule=BACKUP_SCHEDULE_ID
```

Replace the following:

  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - BACKUP\_SCHEDULE\_ID : The ID of a backup schedule. You can view the ID of each backup schedule when you [list all backup schedules](#list_backup_schedules) .

### Update a backup schedule

To update the retention period of a backup schedule, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** .

3.  Click **Edit** to edit disaster recovery settings.

4.  Edit the backup schedule settings and then click **Save** .

##### gcloud

Use the [`  gcloud firestore backups schedules update  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/schedules/update) command:

``` bash
gcloud firestore backups schedules update \
--database='DATABASE_ID' \
--backup-schedule=BACKUP_SCHEDULE_ID \
--retention=RETENTION_PERIOD
```

Replace the following:

  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - BACKUP\_SCHEDULE\_ID : The ID of a backup schedule. You can view the ID of each backup schedule when you [list all backup schedules](#list_backup_schedules) .
  - RETENTION\_PERIOD : Set this to a value up to 14 weeks ( `  14w  ` ).

You can update the retention period of a backup schedule, but you cannot update its recurrence. If you need a backup schedule with a different recurrence, delete the old backup schedule if it is no longer required and create a new backup schedule with the preferred recurrence.

### Delete a backup schedule

To delete a backup schedule, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  Click **Edit** to edit disaster recovery settings.

4.  Edit the backup schedule settings and then click **Save** .

##### gcloud

Use the [`  gcloud firestore backups schedules delete  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/schedules/delete) command:

``` bash
gcloud firestore backups schedules delete \
--database='DATABASE_ID' \
--backup-schedule=BACKUP_SCHEDULE_ID
```

Replace the following:

  - DATABASE\_ID : The ID of the database to back up. Set to `  '(default)'  ` for the default database.
  - BACKUP\_SCHEDULE\_ID : The ID of a backup schedule. You can view the ID of each backup schedule when you [list all backup schedules](#list_backup_schedules) .

Note that deleting a backup schedule won't delete backups already created by this schedule. You can wait for them to expire after their retention period, or to manually delete a backup, see [delete backup](#delete_backup) .

## Manage backups

### List backups

To list available backups, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  Click **Edit** to edit disaster recovery settings.

4.  Edit the backup schedule settings and then click **Save** .

##### gcloud

Use the [`  gcloud firestore backups list  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/list) command:

``` bash
gcloud firestore backups list \
--format="table(name, database, state)"
```

The `  --format="table(name, database, state)"  ` flag formats the output into a more readable format. To list only the backups from a specific location, use the `  --location  ` flag:

``` bash
gcloud firestore backups list \
--location=LOCATION \
--format="table(name, database, state)"
```

Replace `  LOCATION  ` with the name of a Firestore location.

### Describe a backup

To view details about a backup, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists.

3.  The **Disaster recovery** page opens. This page describes backup schedules and lists available backups.

##### gcloud

Use the [`  gcloud firestore backups describe  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/describe) command:

``` bash
gcloud firestore backups describe \
--location=LOCATION \
--backup=BACKUP_ID
```

Replace the following:

  - LOCATION : The location of the database.
  - BACKUP\_ID : The ID of a backup. You can view the ID of each backup when you [list all backups](#list_backups) .

### Delete backup

To delete a backup, use one of the following methods.

**Warning:** You cannot recover a deleted backup.

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists. The **Disaster recovery** page opens. This page describes backup schedules and lists available backups.

3.  In the **Backups** table, find the row for a backup and in the **Actions** column, click **View more** ( more\_vert ). Click **Delete** .

4.  Confirm the action using the text field and click **Delete** .

##### gcloud

Use the [`  gcloud firestore backups delete  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups/delete) command:

``` bash
gcloud firestore backups delete \
--location=LOCATION \
--backup=BACKUP_ID
```

Replace the following:

  - LOCATION : The location of the database.
  - BACKUP\_ID : The ID of a backup. You can view the ID of each backup when you [list all backups](#list_backups) .

**Note:** Firestore stores metadata related to backups and backup schedules related to a database. Firestore retains this metadata until **all** backups for the database expire or are deleted.

## Restore data from a database backup

A restore operation writes the data from a backup to a new Firestore database.

To begin a restore operation, use one of the following methods:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, find the row for the database. In the **Scheduled backups** column click either **View backups** or **Edit settings** , depending on whether a backup schedule exists. The **Disaster recovery** page opens. This page describes backup schedules and lists available backups.

3.  In the **Backups** table, find the row for a backup and in the **Actions** column, click **View more** ( more\_vert ). Click **Restore with Cloud Shell** .

4.  The Cloud Shell panel opens with a gcloud CLI command to restore from the selected backup. Replace ID\_OF\_NEW\_DATABASE with an ID for the database and run the command.
    
    Running the command returns a response with more information about the operation. The database soon appears in your list of databases. The restore operation will take some time and must complete before the database is accessible.

##### gcloud

Use the [`  gcloud firestore databases restore  `](https://cloud.google.com/sdk/gcloud/reference/alpha/firestore/databases/restore) command:

``` bash
gcloud firestore databases restore \
--source-backup=projects/PROJECT_ID/locations/LOCATION/backups/BACKUP_ID \
--destination-database='DATABASE_ID \
--tags=[KEY=VALUE]'
```

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The location of the database backup and the location of the new database created for the restored data.
  - BACKUP\_ID : The ID of a backup. You can view the ID of each backup when you [list all backups](#list_backups) .
  - DATABASE\_ID : A database ID for the new database. You cannot use a database ID that is already in use.
  - \[ KEY = VALUE \]: A optional list of tags KEY=VALUE pairs to bind. For example:
      - `  --tags=123/environment=production,123/costCenter=marketing  `
      - `  --tags=tagKeys/333=tagValues/444  `

The database mode will match that of the backup. The output will include `  metadata  ` , `  name  ` , and `  response  ` components:

``` text
metadata:
  '@type': type.googleapis.com/google.firestore.admin.v1.RestoreDatabaseMetadata
  backup: projects/PROJECT_ID/locations/LOCATION/backups/BACKUP_ID
  database: projects/PROJECT_ID/databases/DATABASE_ID
  operationState: PROCESSING
  progressPercentage:
    completedWork: '20'
    estimatedWork: '100'
  startTime: '2023-12-06T14:20:17.398325Z'
name: projects/PROJECT_ID/databases/DATABASE_ID/operations/operation_uuid
response:
  '@type': type.googleapis.com/google.firestore.admin.v1.Database
  createTime: '2023-12-06T14:20:17.398325Z'
  name: projects/PROJECT_ID/databases/DATABASE_ID
  ...
```

The `  metadata  ` field includes a `  progressPercentage  ` component, detailing the estimated progress of the restore thus far, and an `  operationState  ` specifying the overall state of the restore. To retrieve this information again, use `  gcloud firestore operations list  ` :

``` bash
gcloud firestore operations list --database=DATABASE_ID
```

or, using the `  name  ` field from the output described above, with `  gcloud firestore operations describe  ` :

``` bash
gcloud firestore operations describe OPERATION_NAME
```

### Limitations

A restore operation does not restore [App Engine search data](https://cloud.google.com/appengine/docs/legacy/standard/python/search) or [blob entities](https://cloud.google.com/appengine/docs/legacy/standard/python/blobstore) from a `  (default)  ` database. This data is only valid for the `  (default)  ` database, and it won't be useful if you restore from `  (default)  ` to a database which does not support such data, so it is excluded from backups.

### What to do after restoring

After you finish restoring, you should do the following:

  - If you previously used [Firebase Security Rules](/firestore/docs/security/get-started) , configure your rules for the restored database. By default, the rules for a database that was not previously used prohibit all reads and writes from web and mobile clients. If the database ID you chose was previously used in the same project, you should check if Security Rules for that database ID already exist and, if so, if they are compatible with the requirements of your application.

  - Verify that appropriate [IAM controls](/firestore/native/docs/security/iam) are applied to your new database.

  - If you previously used [TTL](/firestore/native/docs/ttl) policies, reapply them to the new database. TTL policies are not included in backups and are not automatically reapplied to restored databases.
