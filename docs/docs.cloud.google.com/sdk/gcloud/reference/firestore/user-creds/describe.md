---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/user-creds/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/user-creds/describe
title: gcloud firestore user-creds describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore user-creds describe - describes a Cloud Firestore user creds

SYNOPSIS

`gcloud firestore user-creds describe` [`USER_CREDS`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/user-creds/describe#USER_CREDS) [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/user-creds/describe#--database) = `DATABASE` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/user-creds/describe#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To describe user creds 'test-user-creds-id' under database testdb.

```
gcloud firestore user-creds describe test-user-creds-id --database='testdb'
```

POSITIONAL ARGUMENTS

`USER_CREDS`  
The user creds to operate on.

For example, to operate on user creds `creds-name-1` :

```
gcloud firestore user-creds describe creds-name-1
```

REQUIRED FLAGS

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore user-creds describe --database='foo'
```

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore user-creds describe
```

```
gcloud beta firestore user-creds describe
```
