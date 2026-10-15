---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/describe
title: gcloud firestore change-streams describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore change-streams describe - describe a Cloud Firestore change stream

SYNOPSIS

`gcloud firestore change-streams describe` [`CHANGE_STREAM`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/describe#CHANGE_STREAM) [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/describe#--database) = `DATABASE` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/describe#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To describe a change stream named `my-stream` in database `my-db` :

```
gcloud firestore change-streams describe my-stream --database=my-db
```

POSITIONAL ARGUMENTS

`CHANGE_STREAM`  
The ID of the change stream.

REQUIRED FLAGS

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore change-streams describe --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore change-streams describe
```

```
gcloud beta firestore change-streams describe
```
