---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/datastore/operations/cancel
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/datastore/operations/cancel
title: gcloud alpha datastore operations cancel
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:27Z"
---

NAME

gcloud alpha datastore operations cancel - cancel a currently-running Cloud Datastore admin operation

SYNOPSIS

`gcloud alpha datastore operations cancel` `  NAME  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Cancel a currently-running Cloud Datastore admin operation.

EXAMPLES

To cancel the currently-running operation with id `exampleId` , run:

    gcloud alpha datastore operations cancel exampleId

or

    gcloud alpha datastore operations cancel projects/your-project-id/operations/exampleId

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to cancel, formatted as either the full or relative resource path:
    
        projects/my-app-id/operations/foo
    
    or:
    
        foo

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

    gcloud datastore operations cancel

    gcloud beta datastore operations cancel
