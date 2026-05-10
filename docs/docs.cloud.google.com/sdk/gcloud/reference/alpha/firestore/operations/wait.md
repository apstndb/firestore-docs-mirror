---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/operations/wait
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/operations/wait
title: gcloud alpha firestore operations wait
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:28:49Z"
---

NAME

gcloud alpha firestore operations wait - waits a Cloud Firestore admin operation to complete

SYNOPSIS

`gcloud alpha firestore operations wait` `  NAME  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Waits a Cloud Firestore admin operation to complete.

EXAMPLES

To wait a Cloud Firestore admin operation `exampleOperationId` to complete, run:

    gcloud alpha firestore operations wait exampleOperationId

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to retrieve, formatted as full resource path:
    
        projects/my-app-id/databases/(default)/operations/foo

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
