---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/datastore/import
uri: https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import
title: gcloud datastore import
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud datastore import - import Cloud Datastore entities from Google Cloud Storage

SYNOPSIS

`gcloud datastore import` [`INPUT_URL`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#INPUT_URL) \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#--async) \] \[ [`--kinds`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#--kinds) =\[ `KIND` , …\]\] \[ [`--namespaces`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#--namespaces) =\[ `NAMESPACE` , …\]\] \[ [`--operation-labels`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#--operation-labels) =\[ `OPERATION_LABEL` , …\]\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/import#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Imports entities into Google Cloud Datastore. Existing entities with the same key are overwritten. The import occurs in the background and its progress can be monitored and managed via the Operation resource that is created. If an Import operation is cancelled, it is possible that a subset of the data has already been imported to Cloud Datastore. This data will not be removed.

EXAMPLES

To import all data exported to the output URL `gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata` , run:

```
gcloud datastore import gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata
```

To import all data exported to the output URL `gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata` without waiting for the operation to complete, run:

```
gcloud datastore import gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata --async
```

To import only the `exampleKind` from the data exported to the output URL `gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata` , run:

```
gcloud datastore import gs://exampleBucket/exampleExport/exampleExport.overall_export_metadata --kinds='exampleKind'
```

POSITIONAL ARGUMENTS

`INPUT_URL`  
Location of the import metadata. Must be a valid Google Cloud Storage object. The file extension is 'overall_export_metadata'.

This location is the 'output_url' field of a previous export, and can be found via the 'operations describe' command.

FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

`--kinds` =\[ `KIND` ,…\]  
A list specifying what kinds will be included in the operation. When omitted, all Kinds are included. For example, to operate on only the 'Customer' and 'Order' Kinds:

```
gcloud datastore import --kinds='Customer','Order'
```

`--namespaces` =\[ `NAMESPACE` ,…\]  
A list specifying what namespaces will be included in the operation. When omitted, all namespaces are included in the operation, including the default namespace. To specify that `only` the default namespace should be operated on, use the special symbol '(default)'. For example, to operate on entities from both the 'customers' and default namespaces:

```
gcloud datastore import --namespaces='(default)','customers'
```

`--operation-labels` =\[ `OPERATION_LABEL` ,…\]  
A string:string map of custom labels to associate with this operation. For example:

```
gcloud datastore import --operation-labels=comment='customer orders','sales rep'=pending
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha datastore import
```

```
gcloud beta datastore import
```
