---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules
title: 'REST Resource: projects.databases.backupSchedules'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Resource: BackupSchedule

A backup schedule for a Cloud Firestore Database.

This resource is owned by the database it is backing up, and is deleted along with the database. The actual backups are not though.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "retention": string,

  // Union field recurrence can be only one of the following:
  "dailyRecurrence": {
    object (DailyRecurrence)
  },
  "weeklyRecurrence": {
    object (WeeklyRecurrence)
  }
  // End of list of possible types for union field recurrence.
}
```

| Fields                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                           | `string` Output only. The unique backup schedule identifier across all locations and databases for the given project. This will be auto-assigned. Format is `projects/{project}/databases/{database}/backupSchedules/{backupSchedule}`                                                                                                                                                                                                                                                                                             |
| `createTime`                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The timestamp at which this backup schedule was created and effective since. No backups will be created for this schedule before this time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .     |
| `updateTime`                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The timestamp at which this backup schedule was most recently updated. When a backup schedule is first created, this is the same as createTime. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `retention`                                                                                                                      | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` At what relative time in the future, compared to its creation time, the backup should be deleted, e.g. keep backups for 7 days. The maximum supported retention period is 14 weeks. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                         |
| Union field `recurrence` . A oneof field to represent when backups will be taken. `recurrence` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `dailyRecurrence`                                                                                                                | `object ( `[`DailyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules#DailyRecurrence)` )` For a schedule that runs daily.                                                                                                                                                                                                                                                                                                                                              |
| `weeklyRecurrence`                                                                                                               | `object ( `[`WeeklyRecurrence`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules#WeeklyRecurrence)` )` For a schedule that runs weekly on a specific day.                                                                                                                                                                                                                                                                                                                         |

## DailyRecurrence

This type has no fields.

Represents a recurring schedule that runs every day.

The time zone is UTC.

## WeeklyRecurrence

Represents a recurring schedule that runs on a specified day of the week.

The time zone is UTC.

**JSON representation**

```
{
  "day": enum (DayOfWeek)
}
```

| Fields |                                                                                                                                                                                                         |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `day`  | `enum ( `[`DayOfWeek`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules#DayOfWeek)` )` The day of week to run. DAY_OF_WEEK_UNSPECIFIED is not allowed. |

## DayOfWeek

Represents a day of the week.

| Enums                     |                                     |
|---------------------------|-------------------------------------|
| `DAY_OF_WEEK_UNSPECIFIED` | The day of the week is unspecified. |
| `MONDAY`                  | Monday                              |
| `TUESDAY`                 | Tuesday                             |
| `WEDNESDAY`               | Wednesday                           |
| `THURSDAY`                | Thursday                            |
| `FRIDAY`                  | Friday                              |
| `SATURDAY`                | Saturday                            |
| `SUNDAY`                  | Sunday                              |

| Methods                                                                                                              |                                           |
|----------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| [`create`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/create) | Creates a backup schedule on a database.  |
| [`delete`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/delete) | Deletes a backup schedule.                |
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/get)       | Gets information about a backup schedule. |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/list)     | List backup schedules.                    |
| [`patch`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.backupSchedules/patch)   | Updates a backup schedule.                |
