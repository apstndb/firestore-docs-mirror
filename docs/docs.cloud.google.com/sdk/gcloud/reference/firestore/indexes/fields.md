NAME

gcloud firestore indexes fields - manage single-field indexes for Cloud Firestore

SYNOPSIS

`  gcloud firestore indexes fields  ` `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

Changes here apply to index settings for individual fields, and won't affect any composite indexes using those fields.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run `  $ gcloud help  ` for details.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  describe  `  
    Describe the index configuration of the given field.
  - `  list  `  
    List fields with non-default index settings.
  - `  update  `  
    Update the index configuration of the given field.

NOTES

These variants are also available:

``` text
gcloud alpha firestore indexes fields
```

``` text
gcloud beta firestore indexes fields
```
