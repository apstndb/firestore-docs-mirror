---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update
title: gcloud firestore backups schedules update
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore backups schedules update - updates a Cloud Firestore backup schedule

SYNOPSIS

`gcloud firestore backups schedules update` [`--backup-schedule`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update#--backup-schedule) = `BACKUP_SCHEDULE` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update#--database) = `DATABASE` \[ [`--retention`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update#--retention) = `RETENTION` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/update#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To update backup schedule 'cf9f748a-7980-4703-b1a1-d1ffff591db0' under database testdb to 7 days retention.

```
gcloud firestore backups schedules update --database='testdb' --backup-schedule='cf9f748a-7980-4703-b1a1-d1ffff591db0' --retention='7d'
```

REQUIRED FLAGS

`--backup-schedule` = `BACKUP_SCHEDULE`  
The backup schedule to operate on.

For example, to operate on backup schedule `091a49a0-223f-4c98-8c69-a284abbdb26b` :

```
gcloud firestore backups schedules update --backup-schedule='091a49a0-223f-4c98-8c69-a284abbdb26b'
```

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore backups schedules update --database='foo'
```

OPTIONAL FLAGS

`--retention` = `RETENTION`  
The rention of the backup. At what relative time in the future, compared to the creation time of the backup should the backup be deleted, i.e. keep backups for 7 days.

For example, to set retention as 7 days.

```
gcloud firestore backups schedules update --retention=7d
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore backups schedules update
```

```
gcloud beta firestore backups schedules update
```
