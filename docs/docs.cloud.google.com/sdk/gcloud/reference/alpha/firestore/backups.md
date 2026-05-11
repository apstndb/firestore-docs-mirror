---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/backups
title: gcloud alpha firestore backups
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha firestore backups - the set of commands to manage backups for Cloud Firestore

SYNOPSIS

`gcloud alpha firestore backups` `  GROUP  ` | `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` The set of commands to manage backups for Cloud Firestore.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run ` $ gcloud help  ` for details.

GROUPS

`  GROUP  ` is one of the following:

  - `  schedules  `  
    `(ALPHA)` Manage the backup schedules for a Cloud Firestore Database.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  delete  `  
    `(ALPHA)` Deletes a Cloud Firestore backup.
  - `  describe  `  
    `(ALPHA)` Retrieves information about a Cloud Firestore backup.
  - `  list  `  
    `(ALPHA)` List backups available to Cloud Firestore.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

    gcloud firestore backups

    gcloud beta firestore backups
