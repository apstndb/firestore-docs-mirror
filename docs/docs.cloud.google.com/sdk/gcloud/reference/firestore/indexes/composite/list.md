---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list
title: gcloud firestore indexes composite list
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore indexes composite list - list composite indexes

SYNOPSIS

`gcloud firestore indexes composite list` \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--database) = `DATABASE` \] \[ [`--filter`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--filter) = `EXPRESSION` \] \[ [`--limit`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--limit) = `LIMIT` \] \[ [`--page-size`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--page-size) = `PAGE_SIZE` \] \[ [`--sort-by`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--sort-by) =\[ `FIELD` , …\]\] \[ [`--uri`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#--uri) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/composite/list#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

List composite indexes.

By default, this command pretty prints a summary of the index specification. For the full index specification, please specify a format using the `--format=json|yaml|text|etc.` flag. For more information about format, run `$ `[`gcloud topic formats`](https://docs.cloud.google.com/sdk/gcloud/reference/topic/formats) .

EXAMPLES

The following command lists all composite indexes in the database:

```
gcloud firestore indexes composite list
```

```
gcloud firestore indexes composite list --database=(default)
```

The following command lists composite indexes in the `Events` collection group:

```
gcloud firestore indexes composite list --filter=COLLECTION_GROUP:Events
```

FLAGS

Collection group resource - Collection group of the index. This represents a Cloud resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument \[--collection-group\] on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

To set the `collection-group` attribute:

- provide the argument \[--collection-group\] on the command line.

`--database` = `DATABASE`

Database of the collection group. To set the `database` attribute:

- provide the argument \[--collection-group\] on the command line with a fully specified name;
- provide the argument `--database` on the command line;
- the default value of argument \[--database\] is `(default)` .

LIST COMMAND FLAGS

`--filter` = `EXPRESSION`  
Apply a Boolean filter `EXPRESSION` to each resource item to be listed. If the expression evaluates `True` , then that item is listed. For more details and examples of filter expressions, run \$ [gcloud topic filters](https://docs.cloud.google.com/sdk/gcloud/reference/topic/filters) . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--limit` = `LIMIT`  
Maximum number of resources to list. The default is `unlimited` . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--page-size` = `PAGE_SIZE`  
Some services group resource list output into pages. This flag specifies the maximum number of resources per page. The default is determined by the service if it supports paging, otherwise it is `unlimited` (no paging). Paging may be applied before or after `--filter` and `--limit` depending on the service.

`--sort-by` =\[ `FIELD` ,…\]  
Comma-separated list of resource field key names to sort by. The default order is ascending. Prefix a field with \`\`\~´´ for descending order on that field. This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--uri`  
Print a list of resource URIs instead of the default output, and change the command output to a list of URIs. If this flag is used with `--format` , the formatting is applied on this URI list. To display URIs alongside other keys instead, use the `uri()` transform.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `firestore/v1` API. The full documentation for this API can be found at: <https://cloud.google.com/firestore>

NOTES

These variants are also available:

```
gcloud alpha firestore indexes composite list
```

```
gcloud beta firestore indexes composite list
```
