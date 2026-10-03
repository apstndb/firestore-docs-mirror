---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/ping
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/ping
title: gcloud firestore databases ping
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore databases ping - times the connection and ping time for a Firestore with MongoDB compatibility database

SYNOPSIS

`gcloud firestore databases ping` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/ping#--database) = `DATABASE` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/ping#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To time the connection and ping times for a Firestore with MongoDB compatibility database `testdb` :

```
gcloud firestore databases ping --database=testdb
```

REQUIRED FLAGS

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore databases ping --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore databases ping
```

```
gcloud beta firestore databases ping
```
