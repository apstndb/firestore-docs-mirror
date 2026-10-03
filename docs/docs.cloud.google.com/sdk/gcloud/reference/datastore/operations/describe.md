---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe
title: gcloud datastore operations describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud datastore operations describe - retrieves information about a Cloud Datastore admin operation

SYNOPSIS

`gcloud datastore operations describe` [`NAME`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe#NAME) \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Retrieves information about a Cloud Datastore admin operation.

EXAMPLES

To see information on the operation with id `exampleId` , run:

```
gcloud datastore operations describe exampleId
```

or

```
gcloud datastore operations describe projects/your-project-id/operations/exampleId
```

POSITIONAL ARGUMENTS

`NAME`  
The unique name of the Operation to retrieve, formatted as either the full or relative resource path:

```
projects/my-app-id/operations/foo
```

or:

```
foo
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha datastore operations describe
```

```
gcloud beta datastore operations describe
```
