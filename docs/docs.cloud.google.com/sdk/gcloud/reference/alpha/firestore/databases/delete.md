---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/databases/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/firestore/databases/delete
title: gcloud alpha firestore databases delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:26:12Z"
---

NAME

gcloud alpha firestore databases delete - delete a Google Cloud Firestore database

SYNOPSIS

`gcloud alpha firestore databases delete` `  --database  ` = `  DATABASE  ` \[ `  --etag  ` = `  ETAG  ` \] \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To delete a Firestore database test.

    gcloud alpha firestore databases delete --database=test

To delete the Firestore (default) database.

    gcloud alpha firestore databases delete --database=(default)

To delete a Firestore database test providing etag.

    gcloud alpha firestore databases delete --database=test --etag=etag

REQUIRED FLAGS

  - `--database` = `  DATABASE  `  
    The database to operate on.

OPTIONAL FLAGS

  - `--etag` = `  ETAG  `  
    The current etag of the Database. If an etag is provided and does not match the current etag of the database, deletion will be blocked and a FAILED\_PRECONDITION error will be returned.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

    gcloud firestore databases delete

    gcloud beta firestore databases delete
