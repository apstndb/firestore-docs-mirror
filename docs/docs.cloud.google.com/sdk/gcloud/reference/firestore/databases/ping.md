NAME

gcloud firestore databases ping - times the connection and ping time for a Firestore with MongoDB compatibility database

SYNOPSIS

`  gcloud firestore databases ping  ` `  --database  ` = `  DATABASE  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To time the connection and ping times for a Firestore with MongoDB compatibility database `  testdb  ` :

``` text
gcloud firestore databases ping --database=testdb
```

REQUIRED FLAGS

  - `  --database  ` = `  DATABASE  `  
    The database to operate on.
    
    For example, to operate on database `  foo  ` :
    
    ``` text
    gcloud firestore databases ping --database='foo'
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

These variants are also available:

``` text
gcloud alpha firestore databases ping
```

``` text
gcloud beta firestore databases ping
```
