NAME

gcloud beta firestore user-creds describe - describes a Cloud Firestore user creds

SYNOPSIS

`  gcloud beta firestore user-creds describe  ` `  USER_CREDS  ` `  --database  ` = `  DATABASE  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To describe user creds 'test-user-creds-id' under database testdb.

``` text
gcloud beta firestore user-creds describe test-user-creds-id --database='testdb'
```

POSITIONAL ARGUMENTS

  - `  USER_CREDS  `  
    The user creds to operate on.
    
    For example, to operate on user creds `  creds-name-1  ` :
    
    ``` text
    gcloud beta firestore user-creds describe creds-name-1
    ```

REQUIRED FLAGS

  - `  --database  ` = `  DATABASE  `  
    The database to operate on.
    
    For example, to operate on database `  foo  ` :
    
    ``` text
    gcloud beta firestore user-creds describe --database='foo'
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

``` text
gcloud firestore user-creds describe
```

``` text
gcloud alpha firestore user-creds describe
```
