---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/fields/ttls
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/fields/ttls
title: gcloud alpha firestore fields ttls
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha firestore fields ttls - manage Time-to-live metadata for Cloud Firestore

SYNOPSIS

`gcloud alpha firestore fields ttls` `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Manage Time-to-live metadata for Cloud Firestore.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run ` $ gcloud help  ` for details.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  list  `  
    `(ALPHA)` List all fields used as a Time To Live expiration setting.
  - `  update  `  
    `(ALPHA)` Update the TTL configuration of the given field.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

    gcloud firestore fields ttls

    gcloud beta firestore fields ttls
