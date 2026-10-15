---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create
title: gcloud firestore change-streams create
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore change-streams create - create a Cloud Firestore change stream

SYNOPSIS

`gcloud firestore change-streams create` [`CHANGE_STREAM`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#CHANGE_STREAM) ( [`--collection-group-scope`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#--collection-group-scope) = `COLLECTION_GROUP_ID` \| [`--database-scope`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#--database-scope) ) \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#--database) = `DATABASE` ; default="(default)"\] \[ [`--retention`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#--retention) = `RETENTION` ; default="7d"\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/change-streams/create#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To create a database-scoped change stream named `my-stream` in database `my-db` :

```
gcloud firestore change-streams create my-stream --database=my-db --database-scope
```

To create a collection-group-scoped change stream named `my-cg-stream` for collection group `my-cg` in database `my-db` with a retention period of 1 day:

```
gcloud firestore change-streams create my-cg-stream --database=my-db --collection-group-scope=my-cg --retention=1d
```

POSITIONAL ARGUMENTS

`CHANGE_STREAM`  
The ID of the change stream.

REQUIRED FLAGS

Exactly one of these must be specified:

`--collection-group-scope` = `COLLECTION_GROUP_ID`  
Create a collection-group-scoped change stream for the specified collection group (e.g., --collection-group-scope=my-collection-group).

`--database-scope`  
Create a database-scoped change stream.

OPTIONAL FLAGS

`--database` = `DATABASE` ; default="(default)"  
The database to operate on. The default value is `(default)` .

For example, to operate on database `foo` :

```
gcloud firestore change-streams create --database='foo'
```

`--retention` = `RETENTION` ; default="7d"  
The retention period of the change stream (e.g. 1d, 7d). Must be between 1 and 7 days, in day granularity. Default is 7d.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore change-streams create
```

```
gcloud beta firestore change-streams create
```
