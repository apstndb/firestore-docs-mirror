# Schedule data exports

This page describes how to schedule exports of your Firestore data. To run exports on a schedule, we recommend using Cloud Run functions and Cloud Scheduler.

**Caution:** Exporting data from Firestore will incur one read operation per document exported. However, these reads will not appear in the usage section of the console. Make sure you understand this before setting up recurring exports to avoid an unexpected bill.

## Before you begin

Before you schedule managed data exports, you must complete the following tasks:

1.  [Enable billing for your Google Cloud project.](https://cloud.google.com/billing/docs/how-to/modify-project) Only Google Cloud projects with billing enabled can use the export and import feature.
    **Note:** Firebase projects must be on the [Blaze plan](https://firebase.google.com/pricing/?authuser=0) to use the managed export and import feature. Enabling billing for the Google Cloud automatically upgrades your Firebase project to the Blaze plan.
2.  Export operations require a destination Cloud Storage bucket. [Create a Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets) in a location near [your Firestore database location](../locations#view-settings) . You cannot use a Requester Pays bucket for export operations.

## Create a Cloud Function and a Cloud Scheduler job

Follow the steps below to create a Node.js Cloud Function that initiates a Firestore data export and a Cloud Scheduler job to call that function:

##### Firebase CLI

1.  [Install the Firebase CLI](https://firebase.google.com/docs/cli) . In a new directory, initialize the CLI for Cloud Run functions:
    
    ``` text
    firebase init functions --project PROJECT_ID
    ```
    
    1.  Select **JavaScript** for the language.
    2.  Optionally, enable ESLint.
    3.  Enter `  y  ` to install dependencies.

2.  Replace the code in the `  functions/index.js  ` file with the following:
    
    ``` javascript
    const functions = require('firebase-functions');
    const firestore = require('@google-cloud/firestore');
    const client = new firestore.v1.FirestoreAdminClient();
    
    // Replace BUCKET_NAME
    const bucket = 'gs://BUCKET_NAME';
    
    exports.scheduledFirestoreExport = functions.pubsub
                                                .schedule('every 24 hours')
                                                .onRun((context) => {
    
      const projectId = process.env.GCP_PROJECT;
      const databaseName = 
        client.databasePath(projectId, '(default)');
    
      return client.exportDocuments({
        name: databaseName,
        outputUriPrefix: bucket,
        // Leave collectionIds empty to export all collections
        // or set to a list of collection IDs to export,
        // collectionIds: ['users', 'posts']
        collectionIds: []
        })
      .then(responses => {
        const response = responses[0];
        console.log(`Operation Name: ${response['name']}`);
      })
      .catch(err => {
        console.error(err);
        throw new Error('Export operation failed');
      });
    });index.js
    ```

3.  In the code above, modify the following:
    
      - Replace `  BUCKET_NAME  ` with the name of your bucket.
    
      - Replace `  YOUR_PROJECT_ID  ` with your project Id
    
      - Modify `  every 24 hours  ` to set your export schedule. Use either [AppEngine cron.yaml syntax](https://cloud.google.com/appengine/docs/standard/python/config/cronref#schedule_format) or the [unix-cron format](https://cloud.google.com/scheduler/docs/configuring/cron-job-schedules) ( `  * * * * *  ` ).
    
      - Modify `  collectionIds: []  ` to export only the specified collection groups. Leave as is to export all collection groups.
        
        **Note:** If you export all collections, any follow-up import operations must import all collections in the export data files.

4.  Deploy the scheduled function:
    
    ``` text
    firebase deploy --only functions
    ```

##### Google Cloud console

###### Create a Cloud Function

1.  Go to the **Cloud Functions** page in the Google Cloud console:

2.  Click **Write a function**

3.  Enter a function name such as `  firestore-export  `

4.  Under **Trigger** , select **Cloud Pub/Sub**

5.  Under **Topic** , select **Create new Topic** . Enter a name for the pub/sub topic, such as `  initiateFirestoreExport  ` . Take note of the topic name as you need it to create your Cloud Scheduler job.

6.  Under **Source code** , select **Inline editor** . Enter the following code under `  index.js  ` :
    
    ``` text
    const firestore = require('@google-cloud/firestore');
    const client = new firestore.v1.FirestoreAdminClient();
    // Replace BUCKET_NAME
    const bucket = 'gs://BUCKET_NAME'
    
    exports.scheduledFirestoreExport = (event, context) => {
      const databaseName = client.databasePath(
        YOUR_PROJECT_ID,
        '(default)'
      );
    
      return client
        .exportDocuments({
          name: databaseName,
          outputUriPrefix: bucket,
          // Leave collectionIds empty to export all collection groups
          // or define a list of collection group IDs:
          // collectionIds: ['users', 'posts']
          collectionIds: [],
        })
        .then(responses => {
          const response = responses[0];
          console.log(`Operation Name: ${response['name']}`);
          return response;
        })
        .catch(err => {
          console.error(err);
        });
    };
    ```
    
    In the code above, modify the following:
    
      - Replace `  BUCKET_NAME  ` with the name of your bucket.
    
      - Modify `  collectionIds: []  ` to export only the specified collection groups. Leave as is to export all collection groups.
        
        **Note:** If you export all collection groups, any follow-up import operations must import all collection groups in the export data files.

7.  Under `  package.json  ` , add the following dependency:
    
    ``` text
    {
      "dependencies": {
        "@google-cloud/firestore": "^1.3.0"
      }
    }
    ```

8.  Under **Function to execute** , enter `  scheduledFirestoreExport  ` , the name of the function in `  index.js  ` .

9.  Click **Create** to deploy the Cloud Function.

###### Create a Cloud Scheduler job

Next, create a Cloud Scheduler job that calls your Cloud Function:

1.  Go to the **Cloud Scheduler** page in the Google Cloud console:

2.  Click **Create Job** .

3.  Enter a **Name** for the job such as `  scheduledFirestoreExport  ` .

4.  Enter a **Frequency** , for example, `  every 24 hours  ` .

5.  Select a **Timezone** .

6.  Under **Target** , select **Pub/Sub** . In the **Topic** field, enter the name of the pub/sub topic you defined alongside your Cloud Function, `  initiateFirestoreExport  ` in the example above.

7.  In the **Payload** field, enter `  start export  ` . The job requires a payload defined, but the Cloud Function above does not actually use this value.

8.  Click **Create** .

At this point, you've deployed your Cloud Function and Cloud Scheduler job, but your Cloud Function still needs access permissions to execute export operations.

## Configure access permissions

Next, give the Cloud Function permission to start export operations and to write to your GCS bucket.

This Cloud Function uses your project's default service account to authenticate and authorize its export operations. When you create a project, a default service account is created for you with the following name:

``` text
PROJECT_ID@appspot.gserviceaccount.com
```

This service account requires permission to start an export operation and to write to your Cloud Storage bucket. To grant these permissions, assign the following IAM roles to the default service account:

  - `  Cloud Datastore Import Export Admin  `
    **Note:** This Datastore role also grants permissions for Firestore.
  - `  Owner  ` or `  Storage Admin  ` role on the bucket

You can use the `  gcloud  ` and `  gsutil  ` command-line tools to assign these roles.

If not already installed, you can access these tools from [Cloud Shell](https://cloud.google.com/shell/) in the Google Cloud console:  

1.  Assign the **Cloud Datastore Import Export Admin** role. Replace PROJECT\_ID , and run the following command:
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member serviceAccount:PROJECT_ID@appspot.gserviceaccount.com \
        --role roles/datastore.importExportAdmin
    ```

2.  Assign the **Storage Admin** role on your bucket. Replace PROJECT\_ID and BUCKET\_NAME , and run the following command:
    
    ``` text
    gsutil iam ch serviceAccount:PROJECT_ID@appspot.gserviceaccount.com:admin \
        gs://BUCKET_NAME
    ```

If you disable or delete your App Engine default service account, your App Engine app will lose access to your Firestore database. If you disabled your App Engine service account, you can re-enable it, see [enabling a service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts#enabling) . If you deleted your App Engine service account within the last 30 days, you can restore your service account, see [undeleting a service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts#undeleting) .

## Test your Cloud Scheduler job and Cloud Function

You can test your Cloud Scheduler job in the **Cloud Scheduler** page of the Google Cloud console.

1.  Go to the **Cloud Scheduler** page in the Google Cloud console.  

2.  In the row for your new Cloud Scheduler job, click **Run now** .
    
    After a few seconds, the Cloud Scheduler job should update the result column to **Success** and **Last run** to the current time. You may need to click **Refresh** .

The Cloud Scheduler page only confirms that the job called your Cloud Function. Open the Cloud Function page to see your function's logs.

### View the Cloud Function logs

To see if the Cloud Function successfully started an export operation, open the function's logs:

### Firebase Console

Go to the **Cloud Run functions** page in the Firebase console.

### GCP Console

Go to the **Cloud Run functions** page in the Google Cloud console.

## View export progress

You can use the `  gcloud firestore operations list  ` command to view the progress of your export operations, see [managing export and import operations](../manage-data/export-import#managing_export_and_import_operations) .

After an export operation completes, you can view the output files in your Cloud Storage bucket:
