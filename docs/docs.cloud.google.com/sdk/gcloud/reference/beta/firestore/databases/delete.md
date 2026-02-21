NAME

gcloud beta firestore databases delete - delete a Google Cloud Firestore database

SYNOPSIS

`  gcloud beta firestore databases delete  ` `  --database  ` = `  DATABASE  ` \[ `  --etag  ` = `  ETAG  ` \] \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To delete a Firestore database test.

``` text
gcloud beta firestore databases delete --database=test
```

To delete the Firestore (default) database.

``` text
gcloud beta firestore databases delete --database=(default)
```

To delete a Firestore database test providing etag.

``` text
gcloud beta firestore databases delete --database=test --etag=etag
```

REQUIRED FLAGS

  - `  --database  ` = `  DATABASE  `  
    The database to operate on.

OPTIONAL FLAGS

  - `  --etag  ` = `  ETAG  `  
    The current etag of the Database. If an etag is provided and does not match the current etag of the database, deletion will be blocked and a FAILED\_PRECONDITION error will be returned.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

``` text
gcloud firestore databases delete
```

``` text
gcloud alpha firestore databases delete
```
