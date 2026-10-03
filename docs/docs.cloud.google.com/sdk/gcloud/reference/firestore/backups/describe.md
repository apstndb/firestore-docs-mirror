---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe
title: gcloud firestore backups describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore backups describe - retrieves information about a Cloud Firestore backup

SYNOPSIS

`gcloud firestore backups describe` [`--backup`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe#--backup) = `BACKUP` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe#--location) = `LOCATION` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To retrieve information about the `cf9f748a-7980-4703-b1a1-d1ffff591db0` backup in us-east1.

```
gcloud firestore backups describe --location=us-east1 --backup=cf9f748a-7980-4703-b1a1-d1ffff591db0
```

REQUIRED FLAGS

`--backup` = `BACKUP`  
The backup to operate on.

For example, to operate on backup `cf9f748a-7980-4703-b1a1-d1ffff591db0` :

```
gcloud firestore backups describe --backup='cf9f748a-7980-4703-b1a1-d1ffff591db0'
```

`--location` = `LOCATION`  
The location to operate on. Available locations are listed at <https://cloud.google.com/firestore/docs/locations> .

For example, to operate on location `us-east1` :

```
gcloud firestore backups describe --location='us-east1'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore backups describe
```

```
gcloud beta firestore backups describe
```
