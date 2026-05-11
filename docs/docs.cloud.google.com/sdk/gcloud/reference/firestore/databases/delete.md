---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/firestore/databases/delete
title: gcloud firestore databases delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud firestore databases delete - delete a Google Cloud Firestore database

SYNOPSIS

`gcloud firestore databases delete` `  --database  ` = `  DATABASE  ` \[ `  --etag  ` = `  ETAG  ` \] \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To delete a Firestore database test.

    gcloud firestore databases delete --database=test

To delete the Firestore (default) database.

    gcloud firestore databases delete --database=(default)

To delete a Firestore database test providing etag.

    gcloud firestore databases delete --database=test --etag=etag

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

These variants are also available:

    gcloud alpha firestore databases delete

    gcloud beta firestore databases delete
