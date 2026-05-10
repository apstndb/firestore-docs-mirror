---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/beta/firestore/operations/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/beta/firestore/operations/delete
title: gcloud beta firestore operations delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:14Z"
---

NAME

gcloud beta firestore operations delete - delete a completed Cloud Firestore admin operation

SYNOPSIS

`gcloud beta firestore operations delete` `  NAME  ` \[ `  --database  ` = `  DATABASE  ` ; default="(default)"\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(BETA)` Delete a completed Cloud Firestore admin operation.

EXAMPLES

To delete the completed `exampleOperationId` operation, run:

    gcloud beta firestore operations delete exampleOperationId

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the operation to delete, formatted as either the full or relative resource path:
    
        projects/my-app-id/databases/(default)/operations/foo
    
    or:
    
        foo

FLAGS

  - `--database` = `  DATABASE  ` ; default="(default)"  
    The database to operate on. The default value is `(default)` .
    
    For example, to operate on database `foo` :
    
        gcloud beta firestore operations delete --database='foo'

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

    gcloud firestore operations delete

    gcloud alpha firestore operations delete
