---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete
title: gcloud firestore databases delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore databases delete - delete a Google Cloud Firestore database

SYNOPSIS

`gcloud firestore databases delete` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete#--database) = `DATABASE` \[ [`--etag`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete#--etag) = `ETAG` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To delete a Firestore database test.

```
gcloud firestore databases delete --database=test
```

To delete the Firestore (default) database.

```
gcloud firestore databases delete --database=(default)
```

To delete a Firestore database test providing etag.

```
gcloud firestore databases delete --database=test --etag=etag
```

REQUIRED FLAGS

`--database` = `DATABASE`  
The database to operate on.

OPTIONAL FLAGS

`--etag` = `ETAG`  
The current etag of the Database. If an etag is provided and does not match the current etag of the database, deletion will be blocked and a FAILED_PRECONDITION error will be returned.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore databases delete
```

```
gcloud beta firestore databases delete
```
