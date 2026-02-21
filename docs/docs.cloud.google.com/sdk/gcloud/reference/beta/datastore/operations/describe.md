NAME

gcloud beta datastore operations describe - retrieves information about a Cloud Datastore admin operation

SYNOPSIS

`  gcloud beta datastore operations describe  ` `  NAME  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`  (BETA)  ` Retrieves information about a Cloud Datastore admin operation.

EXAMPLES

To see information on the operation with id `  exampleId  ` , run:

``` text
gcloud beta datastore operations describe exampleId
```

or

``` text
gcloud beta datastore operations describe projects/your-project-id/operations/exampleId
```

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to retrieve, formatted as either the full or relative resource path:
    
    ``` text
    projects/my-app-id/operations/foo
    ```
    
    or:
    
    ``` text
    foo
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

``` text
gcloud datastore operations describe
```

``` text
gcloud alpha datastore operations describe
```
