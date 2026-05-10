---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/backups/describe
title: gcloud firestore backups describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:01Z"
---

NAME

gcloud firestore backups describe - retrieves information about a Cloud Firestore backup

SYNOPSIS

`gcloud firestore backups describe` `  --backup  ` = `  BACKUP  ` `  --location  ` = `  LOCATION  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To retrieve information about the `cf9f748a-7980-4703-b1a1-d1ffff591db0` backup in us-east1.

    gcloud firestore backups describe --location=us-east1 --backup=cf9f748a-7980-4703-b1a1-d1ffff591db0

REQUIRED FLAGS

  - `--backup` = `  BACKUP  `  
    The backup to operate on.
    
    For example, to operate on backup `cf9f748a-7980-4703-b1a1-d1ffff591db0` :
    
        gcloud firestore backups describe --backup='cf9f748a-7980-4703-b1a1-d1ffff591db0'

  - `--location` = `  LOCATION  `  
    The location to operate on. Available locations are listed at <https://cloud.google.com/firestore/docs/locations> .
    
    For example, to operate on location `us-east1` :
    
        gcloud firestore backups describe --location='us-east1'

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

These variants are also available:

    gcloud alpha firestore backups describe

    gcloud beta firestore backups describe
