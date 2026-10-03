---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string
title: gcloud firestore databases connection-string
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore databases connection-string - prints the mongo connection string for the given Firestore database

SYNOPSIS

`gcloud firestore databases connection-string` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string#--database) = `DATABASE` \[ [`--auth`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string#--auth) = `AUTH` ; default="none" \| [`--validate`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string#--validate) = `VALIDATE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/connection-string#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To get the connection string for a Firestore database with a databaseId `testdb` without auth configuration.

```
gcloud firestore databases connection-string --database=testdb --auth=none
```

To get the connection string for a Firestore database with a databaseId `testdb` with Google Compute Engine VM auth.

```
gcloud firestore databases connection-string --database=testdb --auth=gce-vm
```

REQUIRED FLAGS

`--database` = `DATABASE`  
The database to operate on.

For example, to operate on database `foo` :

```
gcloud firestore databases connection-string --database='foo'
```

OPTIONAL FLAGS

At most one of these can be specified:

`--auth` = `AUTH` ; default="none"  
The auth configuration for the connection string.

If connecting from a Google Compute Engine VM, use `gce-vm` . For short term access using the gcloud CLI's access token, use `access-token` . For password auth use scram-sha-256. Otherwise, use `none` and configure auth manually.

`AUTH` must be one of: `none` , `gce-vm` , `access-token` , `scram-sha-256` .

`--validate` = `VALIDATE`  
Validate the specified connection string for the current database. This command checks that the connection string is well formed, contains the required parameters, and specifies correct configuration values for the current database.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

These variants are also available:

```
gcloud alpha firestore databases connection-string
```

```
gcloud beta firestore databases connection-string
```
