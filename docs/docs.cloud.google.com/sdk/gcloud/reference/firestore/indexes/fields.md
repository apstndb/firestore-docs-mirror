---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/fields
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/indexes/fields
title: gcloud firestore indexes fields
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:30Z"
---

NAME

gcloud firestore indexes fields - manage single-field indexes for Cloud Firestore

SYNOPSIS

`gcloud firestore indexes fields` `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

Changes here apply to index settings for individual fields, and won't affect any composite indexes using those fields.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run ` $ gcloud help  ` for details.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  describe  `  
    Describe the index configuration of the given field.
  - `  list  `  
    List fields with non-default index settings.
  - `  update  `  
    Update the index configuration of the given field.

NOTES

These variants are also available:

    gcloud alpha firestore indexes fields

    gcloud beta firestore indexes fields
