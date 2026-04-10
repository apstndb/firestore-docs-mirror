NAME

gcloud firestore databases describe - describes information about a Cloud Firestore database

SYNOPSIS

`  gcloud firestore databases describe  ` \[ `  --database  ` = `  DATABASE  ` ; default="(default)"\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

The following command describes a Google Cloud Firestore database.

EXAMPLES

To describe a Firestore database with a databaseId `  testdb  ` .

``` wrap-code
gcloud firestore databases describe --database=testdb
```

If databaseId is not specified, the command will describe information about the `  (default)  ` database.

``` wrap-code
gcloud firestore databases describe
```

FLAGS

  - `  --database  ` = `  DATABASE  ` ; default="(default)"  
    The database to operate on. The default value is `  (default)  ` .
    
    For example, to operate on database `  foo  ` :
    
    ``` wrap-code
    gcloud firestore databases describe --database='foo'
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

These variants are also available:

``` wrap-code
gcloud alpha firestore databases describe
```

``` wrap-code
gcloud beta firestore databases describe
```
