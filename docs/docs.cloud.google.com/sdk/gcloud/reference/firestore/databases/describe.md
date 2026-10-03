---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/describe
title: gcloud firestore databases describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore databases describe - describes information about a Cloud Firestore database

SYNOPSIS

`gcloud firestore databases describe` \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/describe#--database) = `DATABASE` ; default="(default)"\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/describe#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

The following command describes a Google Cloud Firestore database.

EXAMPLES

To describe a Firestore database with a databaseId `testdb` .

```
gcloud firestore databases describe --database=testdb
```

If databaseId is not specified, the command will describe information about the `(default)` database.

```
gcloud firestore databases describe
```

FLAGS

`--database` = `DATABASE` ; default="(default)"  
The database to operate on. The default value is `(default)` .

For example, to operate on database `foo` :

```
gcloud firestore databases describe --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore databases describe
```

```
gcloud beta firestore databases describe
```
