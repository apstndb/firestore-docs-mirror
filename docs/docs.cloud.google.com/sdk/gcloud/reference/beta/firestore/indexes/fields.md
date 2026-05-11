---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/beta/firestore/indexes/fields
uri: https://docs.cloud.google.com/sdk/gcloud/reference/beta/firestore/indexes/fields
title: gcloud beta firestore indexes fields
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud beta firestore indexes fields - manage single-field indexes for Cloud Firestore

SYNOPSIS

`gcloud beta firestore indexes fields` `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(BETA)` Changes here apply to index settings for individual fields, and won't affect any composite indexes using those fields.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run ` $ gcloud help  ` for details.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  describe  `  
    `(BETA)` Describe the index configuration of the given field.
  - `  list  `  
    `(BETA)` List fields with non-default index settings.
  - `  update  `  
    `(BETA)` Update the index configuration of the given field.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

    gcloud firestore indexes fields

    gcloud alpha firestore indexes fields
