---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete
title: gcloud firestore bulk-delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore bulk-delete - bulk delete Cloud Firestore documents

SYNOPSIS

`gcloud firestore bulk-delete` \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete#--async) \] \[ [`--collection-ids`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete#--collection-ids) =\[ `COLLECTION_GROUP_IDS` , …\]\] \[ [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete#--database) = `DATABASE` ; default="(default)"\] \[ [`--namespace-ids`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete#--namespace-ids) =\[ `NAMESPACE_IDS` , …\]\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/bulk-delete#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

bulk delete Cloud Firestore documents.

EXAMPLES

To bulk delete a specific set of collections groups asynchronously, run:

```
gcloud firestore bulk-delete --collection-ids='specific collection group1','specific
 collection group2' --async
```

To bulk delete all collection groups from certain namespace, run:

```
gcloud firestore bulk-delete --namespace-ids='specific namespace id'
```

FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

`--collection-ids` =\[ `COLLECTION_GROUP_IDS` ,…\]  
List specifying which collection groups will be included in the operation. When omitted, all collection groups are included.

For example, to operate on only the `customers` and `orders` collections groups:

```
gcloud firestore bulk-delete --collection-ids='customers','orders'
```

`--database` = `DATABASE` ; default="(default)"  
The database to operate on. The default value is `(default)` .

For example, to operate on database `foo` :

```
gcloud firestore bulk-delete --database='foo'
```

`--namespace-ids` =\[ `NAMESPACE_IDS` ,…\]  
List specifying which namespaces will be included in the operation. When omitted, all namespaces are included.

This is only supported for Datastore Mode databases.

For example, to operate on only the `customers` and `orders` namespaces:

```
gcloud firestore bulk-delete --namespaces-ids='customers','orders'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore bulk-delete
```

```
gcloud beta firestore bulk-delete
```
