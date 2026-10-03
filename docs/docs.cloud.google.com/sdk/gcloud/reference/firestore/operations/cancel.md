---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel
title: gcloud firestore operations cancel
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore operations cancel - cancel a currently-running Cloud Firestore admin operation

SYNOPSIS

`gcloud firestore operations cancel` [`NAME`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel#NAME) \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel#--database) = `DATABASE` ; default="(default)"\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/cancel#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Cancel a currently-running Cloud Firestore admin operation.

EXAMPLES

To cancel the currently-running `exampleOperationId` operation, run:

```
gcloud firestore operations cancel exampleOperationId
```

POSITIONAL ARGUMENTS

`NAME`  
The unique name of the Operation to cancel, formatted as either the full or relative resource path:

```
projects/my-app-id/databases/(default)/operations/foo
```

or:

```
foo
```

FLAGS

`--database` = `DATABASE` ; default="(default)"  
The database to operate on. The default value is `(default)` .

For example, to operate on database `foo` :

```
gcloud firestore operations cancel --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore operations cancel
```

```
gcloud beta firestore operations cancel
```
