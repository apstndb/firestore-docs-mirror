# Move data between projects

This page describes how to use the managed import and export features to move Firestore data from one project to another. This can be useful for setting up a development environment or as part of permanently migrating an app to another project. The example on this page demonstrates how to export data from a source project and then import that data into a destination project. Moving data between projects involves the following steps:

1.  Create a Cloud Storage bucket to hold the data from your source project.
2.  Export the data from your source project to the bucket.
3.  Give your destination project permission to read from the bucket.
4.  Import the data from the bucket into your destination project.

## Before you begin

Before you can use the managed export and import service, you must complete the following tasks:

1.  [Enable billing for both your source project and destination project.](https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project) Only Google Cloud projects with billing enabled can use the export and import functionality.
    
    **Note:** Firebase projects must be on the [Blaze plan](https://firebase.google.com/pricing/?authuser=0) to use the managed export and import service. Enabling billing for the Google Cloud automatically upgrades your Firebase project to the Blaze plan.

2.  Make sure your account has the necessary IAM permissions in your source project and destination project. **If you are a project owner for both projects, your account has the required permissions.** Otherwise, the following IAM roles grant the necessary permissions for Firestore export and import operations:
    
    `  Owner  ` , `  Cloud Datastore Owner  ` , or `  Cloud Datastore Import Export Admin  `
    
    **Note:** These roles grant permissions for both Datastore and Firestore.
    
    A project owner can grant one of these roles by following the steps in [Grant access](https://cloud.google.com/iam/docs/granting-changing-revoking-access#grant_access) .

3.  Set up the `  gcloud  ` command-line tool and connect to your project in one of the following ways:
    
      - Access `  gcloud  ` from the Google Cloud console using [Cloud Shell](https://cloud.google.com/shell/) .
        
        Make sure `  gcloud  ` is configured for the correct project:
        
        ``` text
        gcloud config set project [SOURCE_PROJECT_ID]
        ```
    
      - [Install and initialize the Google Cloud SDK.](https://cloud.google.com/sdk/docs/quickstarts)

4.  Set up indexes in your new project. The composite indexes should match between the source and destination projects. Indexes should be set up first to avoid having to process each document multiple times.

## Export data from the source project

Export your data by creating a Cloud Storage bucket for your Firestore export files and starting an export operation.

### Create a Cloud Storage bucket

[Create a Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets) in the same location as your Firestore database. To view your database location, see your [project location setting](../locations#project_location_setting) . You cannot use a Requester Pays bucket for export and import operations.

**If your Cloud Storage bucket is not in your source project** , you must give the source project's default service account access to the bucket. Each Google Cloud project has an automatically created default service account with the name `  PROJECT_ID @appspot.gserviceaccount.com  ` . Firestore export operations use this default service account to authorize Cloud Storage bucket operations. To give the default service account access to your source bucket, grant it the [`  Storage Admin  `](https://cloud.google.com/storage/docs/access-control/iam-roles) role.

You can grant this role with the [`  gsutil  ` tool](https://cloud.google.com/storage/docs/gsutil) available in Cloud Shell:

``` text
gsutil iam ch serviceAccount:[service-PROJECT_NUMBER]@gcp-sa-firestore.iam.gserviceaccount.com :roles/storage.admin\
gs://[BUCKET_NAME]@
```

You can also [grant this role in the Google Cloud console](https://cloud.google.com/storage/docs/access-control/using-iam-permissions#bucket-add) .

### Disable write operations (optional)

If your app continues to write to your database while you perform an export operation, you might not capture all of those writes in your export files. To export data from a consistent state, disable writes to your database by updating your security rules and halting any Admin SDK operations.

1.  Update security rules
    
    In the Firestore [**Rules** tab](https://console.firebase.google.com/project/_/firestore/rules) of the console, update your source project security rules to deny all writes. For example:
    
    ``` text
      // Deny write access to all users under any conditions
      service cloud.firestore {
        match /databases/{database}/documents {
          match /{document=**} {
            allow write: if false;
          }
          // Reads do not affect export operations
          // Add your read rules here
        }
      }
    ```

2.  Halt writes from Admin SDKs
    
    Security rules do not stop writes coming from privileged server environments created using a [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup) or a [Google Cloud Server Client Library](https://cloud.google.com/firestore/docs/quickstart-servers) . Make sure to halt write operations from your admin servers by shutting down or updating your servers.

### Begin an export operation

Use the `  gcloud firestore export  ` command to export data from your source project. You can export all your data or only specific collection groups. Replace `  [SOURCE_BUCKET]  ` with the name of your Cloud Storage bucket:

  - Export all data
    
    ``` text
    gcloud firestore export gs://[SOURCE_BUCKET] --async
    ```

  - Export specific collection groups
    
    ``` text
    gcloud firestore export gs://[SOURCE_BUCKET] --collection-ids=[COLLECTION_GROUP_ID_1],[COLLECTION_GROUP_ID_2] --async
    ```

Take note of your export operation's `  outputURIPrefix  ` as you will use this later on. By default, Firestore adds a pre-fix to your export files based on a timestamp:

``` text
outputUriPrefix: gs://[SOURCE_BUCKET]/2019-03-05T20:58:23_56418
```

As the export operation runs, you can use the `  firestore operations list  ` command to view your operation's progress:

``` text
gcloud firestore operations list
```

## Import data into the destination project

Next, give the destination project access to your Firestore data files and start an import operation.

### Give the destination project access to your data files

Before you can begin an import operation, you must make sure your destination project can access your Firestore data files.

#### Move data files to a local bucket

If your source bucket location is different from the Firestore location of your destination project, you must move your data files to a Cloud Storage bucket in the same location as your destination project.

Move your data files to another Cloud Storage bucket by following the steps in [Moving and Renaming Buckets](https://cloud.google.com/storage/docs/moving-buckets) . For all the following steps, use this new bucket as the `  [SOURCE_BUCKET]  ` .

#### Give the project service account access to your source bucket

If your source bucket is not in your destination project, then you must give the destination project's default service account access to your source bucket. The default service account is named `  [DESTINATION_PROJECT_ID] @appspot.gserviceaccount.com  ` . To give the default service account access to your source bucket, grant it the proper permissions to access the bucket.

You can grant the necessary roles with the [`  gsutil  ` tool](https://cloud.google.com/storage/docs/gsutil) available in Cloud Shell:

``` text
gsutil iam ch serviceAccount:[DESTINATION_PROJECT_ID]@appspot.gserviceaccount.com:legacyBucketReader,legacyObjectReader \
gs://[SOURCE_BUCKET]
```

You can also [grant this role in the Google Cloud console](https://cloud.google.com/storage/docs/access-control/using-iam-permissions#bucket-add) .

### Begin an import operation

Before starting the import operation, make sure `  gcloud  ` is configured for the correct project:

``` text
gcloud config set project [DESTINATION_PROJECT_ID]
```

Use the `  gcloud firestore import  ` command to import the data in your source bucket into your destination project:

``` text
gcloud firestore import gs://[SOURCE_BUCKET]/[EXPORT_PREFIX] --async
```

Where `  [EXPORT_PREFIX]  ` matches the prefix in your export operation's `  outputUriPrefix  ` . For example:

``` text
gcloud firestore import gs://[SOURCE_BUCKET]/2019-03-05T20:58:23_56418 --async
```

As the export operation runs, you can use the `  firestore operations list  ` command to view your operation's progress:

``` text
gcloud firestore operations list
```
