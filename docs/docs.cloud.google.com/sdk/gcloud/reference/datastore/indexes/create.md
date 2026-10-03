---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/datastore/indexes/create
uri: https://docs.cloud.google.com/sdk/gcloud/reference/datastore/indexes/create
title: gcloud datastore indexes create
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud datastore indexes create - create new datastore indexes based on your local index configuration

SYNOPSIS

`gcloud datastore indexes create` [`INDEX_FILE`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/indexes/create#INDEX_FILE) \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/indexes/create#--database) = `DATABASE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/datastore/indexes/create#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Create new datastore indexes based on your local index configuration. Any indexes in your index file that do not exist will be created.

EXAMPLES

To create new indexes based on your local configuration, run:

```
gcloud datastore indexes create ~/myapp/index.yaml
```

Detailed information about index configuration can be found at the [index.yaml reference](https://cloud.google.com/datastore/docs/tools/indexconfig) .

POSITIONAL ARGUMENTS

`INDEX_FILE`  
The path to your `index.yaml` file. For a detailed look into defining your `index.yaml` file, refer to this configuration guide: <https://cloud.google.com/datastore/docs/tools/indexconfig#Datastore_About_index_yaml>

FLAGS

`--database` = `DATABASE`  
The database to operate on. If not specified, the CLI refers the `(default)` database by default.

For example, to operate on database `testdb` :

```
gcloud datastore indexes create --database='testdb'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha datastore indexes create
```

```
gcloud beta datastore indexes create
```
