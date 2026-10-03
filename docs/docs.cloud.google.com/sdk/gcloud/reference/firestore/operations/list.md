---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list
title: gcloud firestore operations list
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore operations list - list pending Cloud Firestore admin operations and their status

SYNOPSIS

`gcloud firestore operations list` \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--database) = `DATABASE` ; default="(default)"\] \[ [`--filter`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--filter) = `EXPRESSION` \] \[ [`--limit`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--limit) = `LIMIT` ; default=100\] \[ [`--page-size`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--page-size) = `PAGE_SIZE` ; default=100\] \[ [`--sort-by`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--sort-by) =\[ `FIELD` , …\]\] \[ [`--uri`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#--uri) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/operations/list#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Filters are case-sensitive and have the following syntax:

```
field = value [AND [field = value]] …
```

Only the logical `AND` operator is supported; space-separated items are treated as having an implicit `AND` operator.

EXAMPLES

To retrieve information about recent operations, run:

```
gcloud firestore operations list
```

To only list operations that are done, run:

```
gcloud firestore operations list --filter="done:true"
```

FLAGS

`--database` = `DATABASE` ; default="(default)"  
The database to operate on. The default value is `(default)` .

For example, to operate on database `foo` :

```
gcloud firestore operations list --database='foo'
```

LIST COMMAND FLAGS

`--filter` = `EXPRESSION`  
Apply a Boolean filter `EXPRESSION` to each resource item to be listed. If the expression evaluates `True` , then that item is listed. For more details and examples of filter expressions, run \$ [gcloud topic filters](https://docs.cloud.google.com/sdk/gcloud/reference/topic/filters) . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--limit` = `LIMIT` ; default=100  
Maximum number of resources to list. The default is `100` . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--page-size` = `PAGE_SIZE` ; default=100  
Some services group resource list output into pages. This flag specifies the maximum number of resources per page. The default is `100` . Paging may be applied before or after `--filter` and `--limit` depending on the service.

`--sort-by` =\[ `FIELD` ,…\]  
Comma-separated list of resource field key names to sort by. The default order is ascending. Prefix a field with \`\`\~´´ for descending order on that field. This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--uri`  
Print a list of resource URIs instead of the default output, and change the command output to a list of URIs. If this flag is used with `--format` , the formatting is applied on this URI list. To display URIs alongside other keys instead, use the `uri()` transform.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore operations list
```

```
gcloud beta firestore operations list
```
