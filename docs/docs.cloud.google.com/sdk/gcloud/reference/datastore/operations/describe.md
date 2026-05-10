---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/datastore/operations/describe
title: gcloud datastore operations describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:14Z"
---

NAME

gcloud datastore operations describe - retrieves information about a Cloud Datastore admin operation

SYNOPSIS

`gcloud datastore operations describe` `  NAME  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

Retrieves information about a Cloud Datastore admin operation.

EXAMPLES

To see information on the operation with id `exampleId` , run:

    gcloud datastore operations describe exampleId

or

    gcloud datastore operations describe projects/your-project-id/operations/exampleId

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to retrieve, formatted as either the full or relative resource path:
    
        projects/my-app-id/operations/foo
    
    or:
    
        foo

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

These variants are also available:

    gcloud alpha datastore operations describe

    gcloud beta datastore operations describe
