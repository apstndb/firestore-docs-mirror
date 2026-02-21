NAME

gcloud firestore operations describe - retrieves information about a Cloud Firestore admin operation

SYNOPSIS

`  gcloud firestore operations describe  ` `  NAME  ` \[ `  --database  ` = `  DATABASE  ` ; default="(default)"\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

Retrieves information about a Cloud Firestore admin operation.

EXAMPLES

To retrieve information about the `  exampleOperationId  ` operation, run:

``` text
gcloud firestore operations describe exampleOperationId
```

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to retrieve, formatted as either the full or relative resource path:
    
    ``` text
    projects/my-app-id/databases/(default)/operations/foo
    ```
    
    or:
    
    ``` text
    foo
    ```

FLAGS

  - `  --database  ` = `  DATABASE  ` ; default="(default)"  
    The database to operate on. The default value is `  (default)  ` .
    
    For example, to operate on database `  foo  ` :
    
    ``` text
    gcloud firestore operations describe --database='foo'
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

These variants are also available:

``` text
gcloud alpha firestore operations describe
```

``` text
gcloud beta firestore operations describe
```
