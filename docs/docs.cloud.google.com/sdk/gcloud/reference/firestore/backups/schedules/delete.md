---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/delete
title: gcloud firestore backups schedules delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore backups schedules delete - deletes a Cloud Firestore backup schedule

SYNOPSIS

`gcloud firestore backups schedules delete` [`--backup-schedule`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/delete#--backup-schedule) = `BACKUP_SCHEDULE` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/delete#--database) = `DATABASE` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/schedules/delete#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To delete backup schedule 'cf9f748a-7980-4703-b1a1-d1ffff591db0' under database testdb.

```
gcloud firestore backups schedules delete --database='testdb' --backup-schedule='cf9f748a-7980-4703-b1a1-d1ffff591db0'
```

REQUIRED FLAGS

`--backup-schedule` = `BACKUP_SCHEDULE`  
The backup schedule to operate on.

For example, to operate on backup schedule `091a49a0-223f-4c98-8c69-a284abbdb26b` :

```
gcloud firestore backups schedules delete --backup-schedule='091a49a0-223f-4c98-8c69-a284abbdb26b'
```

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore backups schedules delete --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore backups schedules delete
```

```
gcloud beta firestore backups schedules delete
```
