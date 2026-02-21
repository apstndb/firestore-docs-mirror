NAME

gcloud datastore operations delete - delete a completed Cloud Datastore admin operation

SYNOPSIS

`  gcloud datastore operations delete  ` `  NAME  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

Delete a completed Cloud Datastore admin operation.

EXAMPLES

To delete the completed operation with id `  exampleId  ` , run:

``` text
gcloud datastore operations delete exampleId
```

or

``` text
gcloud datastore operations delete projects/your-project-id/operations/exampleId
```

POSITIONAL ARGUMENTS

  - `  NAME  `  
    The unique name of the Operation to delete, formatted as either the full or relative resource path:
    
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

These variants are also available:

``` text
gcloud alpha datastore operations delete
```

``` text
gcloud beta datastore operations delete
```
