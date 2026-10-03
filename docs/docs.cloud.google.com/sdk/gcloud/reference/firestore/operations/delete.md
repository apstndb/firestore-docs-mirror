---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/delete
title: gcloud firestore operations delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore operations delete - delete a completed Cloud Firestore admin operation

SYNOPSIS

`gcloud firestore operations delete` [`NAME`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/delete#NAME) \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/delete#--database) = `DATABASE` ; default="(default)"\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/delete#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Delete a completed Cloud Firestore admin operation.

EXAMPLES

To delete the completed `exampleOperationId` operation, run:

```
gcloud firestore operations delete exampleOperationId
```

POSITIONAL ARGUMENTS

`NAME`  
The unique name of the operation to delete, formatted as either the full or relative resource path:

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
gcloud firestore operations delete --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore operations delete
```

```
gcloud beta firestore operations delete
```
