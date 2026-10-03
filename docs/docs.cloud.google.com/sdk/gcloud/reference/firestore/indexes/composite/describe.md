---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/describe
title: gcloud firestore indexes composite describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore indexes composite describe - describe the given composite index

SYNOPSIS

`gcloud firestore indexes composite describe` ( [`INDEX`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/describe#INDEX) : [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/describe#--database) = `DATABASE` ) \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/describe#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Describe the given composite index.

By default, this command pretty prints a summary of the index specification. For the full index specification, please specify a format using the `--format=json|yaml|text|etc.` flag. For more information about format, run `$ `[`gcloud topic formats`](https://docs.cloud.google.com/sdk/gcloud/reference/topic/formats) .

EXAMPLES

The following command describes the composite index with ID `3421ef` :

```
gcloud firestore indexes composite describe 3421ef
```

```
gcloud firestore indexes composite describe 3421ef --database=(default)
```

POSITIONAL ARGUMENTS

Composite index resource - Index to describe. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `index` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

To set the `collection-group` attribute:

- provide the argument `index` on the command line with a fully specified name;
- provide the argument \[--collection-group\] on the command line.

This must be specified.

`INDEX`  
ID of the composite index or fully qualified identifier for the composite index.

To set the `index` attribute:

- provide the argument `index` on the command line.

This positional argument must be specified if any of the other arguments in this group are specified.

`--database` = `DATABASE`  
Database of the composite index. To set the `database` attribute:

- provide the argument `index` on the command line with a fully specified name;
- provide the argument `--database` on the command line;
- the default value of argument \[--database\] is `(default)` .

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `firestore/v1` API. The full documentation for this API can be found at: <https://cloud.google.com/firestore>

NOTES

These variants are also available:

```
gcloud alpha firestore indexes composite describe
```

```
gcloud beta firestore indexes composite describe
```
