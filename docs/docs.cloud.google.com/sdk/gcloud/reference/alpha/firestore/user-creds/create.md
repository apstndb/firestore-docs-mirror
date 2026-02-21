NAME

gcloud alpha firestore user-creds create - creates a Cloud Firestore user creds

SYNOPSIS

`  gcloud alpha firestore user-creds create  ` `  USER_CREDS  ` `  --database  ` = `  DATABASE  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To create a user creds called test-user-creds-id under database testdb.

``` text
gcloud alpha firestore user-creds create test-user-creds-id --database=testdb
```

POSITIONAL ARGUMENTS

  - `  USER_CREDS  `  
    The user creds to operate on.
    
    For example, to operate on user creds `  creds-name-1  ` :
    
    ``` text
    gcloud alpha firestore user-creds create creds-name-1
    ```

REQUIRED FLAGS

  - `  --database  ` = `  DATABASE  `  
    The database to operate on.
    
    For example, to operate on database `  foo  ` :
    
    ``` text
    gcloud alpha firestore user-creds create --database='foo'
    ```

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run `  $ gcloud help  ` for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist. These variants are also available:

``` text
gcloud firestore user-creds create
```

``` text
gcloud beta firestore user-creds create
```
