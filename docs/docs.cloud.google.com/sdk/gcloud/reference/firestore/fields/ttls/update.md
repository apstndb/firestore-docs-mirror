---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update
title: gcloud firestore fields ttls update
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore fields ttls update - update the TTL configuration of the given field

SYNOPSIS

`gcloud firestore fields ttls update` ( [`FIELD`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#FIELD) : [`--collection-group`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--collection-group) = `COLLECTION_GROUP` [`--database`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--database) = `DATABASE` ) ( [`--disable-ttl`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--disable-ttl) \| \[ [`--enable-ttl`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--enable-ttl) : [`--expiration-offset`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--expiration-offset) = `EXPIRATION_OFFSET` \]) \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#--async) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/firestore/fields/ttls/update#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Update the TTL configuration of the given field.

This enables or disables using a field as the TTL field for its collection group or kind. Note that only one field can be the TTL field for a collection group.

EXAMPLES

The following command sets the `expiry` field of the `Events` collection group (kind) to be the TTL field:

```
gcloud firestore fields ttls update expiry --collection-group=Events --enable-ttl
```

The following command disables the `expiry` field so it is no longer the TTL for the `Events` collection group (kind):

```
gcloud firestore fields ttls update expiry --collection-group=Events --disable-ttl
```

The following command sets the `expiry` field of the `Events` collection group (kind) to be the TTL field, with an expiration offset of one week:

```
gcloud firestore fields ttls update expiry --collection-group=Events --enable-ttl --expiration-offset=7d
```

POSITIONAL ARGUMENTS

Field resource - Field to update. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `field` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`FIELD`  
ID of the field or fully qualified identifier for the field.

To set the `field` attribute:

- provide the argument `field` on the command line.

This positional argument must be specified if any of the other arguments in this group are specified.

`--collection-group` = `COLLECTION_GROUP`  
Collection group of the field. To set the `collection-group` attribute:

- provide the argument `field` on the command line with a fully specified name;
- provide the argument `--collection-group` on the command line.

`--database` = `DATABASE`  
Database of the field. To set the `database` attribute:

- provide the argument `field` on the command line with a fully specified name;
- provide the argument `--database` on the command line;
- the default value of argument \[--database\] is `(default)` .

REQUIRED FLAGS

Exactly one of these must be specified:

`--disable-ttl`

Set to make this field no longer the TTL for its collection group.

Or at least one of these can be specified:

`--enable-ttl`  
Set to enable this field as the TTL for its collection group.

This flag argument must be specified if any of the other arguments in this group are specified.

`--expiration-offset` = `EXPIRATION_OFFSET`  
The offset, relative to the timestamp value from the TTL-enabled field, used to determine the document's expiration time. If unset, defaults to 0.

OPTIONAL FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `firestore/v1` API. The full documentation for this API can be found at: <https://cloud.google.com/firestore>

NOTES

These variants are also available:

```
gcloud alpha firestore fields ttls update
```

```
gcloud beta firestore fields ttls update
```
