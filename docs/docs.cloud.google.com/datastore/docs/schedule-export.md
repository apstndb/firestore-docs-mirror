This page describes how to schedule exports of your Firestore in Datastore mode data. To run exports on a schedule, we recommend using Cloud Run functions and Cloud Scheduler. Create a Cloud Function that initiates exports and use Cloud Scheduler to run your function.

## Before you begin

Before you schedule data exports, you must complete the following tasks:

1.  [Enable billing for your Google Cloud project.](/billing/docs/how-to/modify-project) Only Google Cloud projects with billing enabled can use the export and import feature.
2.  [Create a Cloud Storage bucket](/storage/docs/creating-buckets) in a location near [your Datastore mode database location](/datastore/docs/locations#view-settings) . Export operations require a destination Cloud Storage bucket. You cannot use a Requester Pays bucket for export operations.

## Create a Cloud Function and Cloud Scheduler job

Follow the steps below to create a Cloud Function that initiates data exports and a Cloud Scheduler job to call that function:

### Create a `     datastore_export    ` Cloud Function

1.  Go to the **Cloud Functions** page in the Google Cloud console:

2.  Click **Create Function**

3.  Enter a function name such as `  datastoreExport  `

4.  Under **Trigger** , select **Cloud Pub/Sub** . Cloud Scheduler uses your pub/sub topic to call your function.

5.  In the **Topic** field, select **Create a topic** . Enter a name for the pub/sub topic such as `  startDatastoreExport  ` . Take note of the topic name as you need it to create your Cloud Scheduler job.

6.  Under **Source code** , select **Inline editor** .

7.  In the **Runtime** dropdown, select **Python 3.7** .

8.  Enter the following code for `  main.py  ` :
    
    ``` python
    # Copyright 2021 Google LLC All Rights Reserved.
    #
    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at
    #
    #     http://www.apache.org/licenses/LICENSE-2.0
    #
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.
    
    import base64
    import json
    import os
    
    from google.cloud import datastore_admin_v1
    
    project_id = os.environ.get("GCP_PROJECT")
    client = datastore_admin_v1.DatastoreAdminClient()
    
    
    def datastore_export(event, context):
        """Triggers a Datastore export from a Cloud Scheduler job.
    
        Args:
            event (dict): event[data] must contain a json object encoded in
                base-64. Cloud Scheduler encodes payloads in base-64 by default.
                Object must include a 'bucket' value and can include 'kinds'
                and 'namespaceIds' values.
            context (google.cloud.functions.Context): The Cloud Functions event
                metadata.
        """
        if "data" in event:
            # Triggered via Cloud Scheduler, decode the inner data field of the json payload.
            json_data = json.loads(base64.b64decode(event["data"]).decode("utf-8"))
        else:
            # Otherwise, for instance if triggered via the Cloud Console on a Cloud Function, the event is the data.
            json_data = event
    
        bucket = json_data["bucket"]
        entity_filter = datastore_admin_v1.EntityFilter()
    
        if "kinds" in json_data:
            entity_filter.kinds = json_data["kinds"]
    
        if "namespaceIds" in json_data:
            entity_filter.namespace_ids = json_data["namespaceIds"]
    
        export_request = datastore_admin_v1.ExportEntitiesRequest(
            project_id=project_id, output_url_prefix=bucket, entity_filter=entity_filter
        )
        operation = client.export_entities(request=export_request)
        response = operation.result()
        print(response)
    ```

9.  In `  requirements.txt  ` , add the following dependency:
    
    ``` text
    google-cloud-datastore==2.23.0
    ```

10. Under **Entry point** , enter `  datastore_export  ` , the name of the function in `  main.py  ` .

11. Click **Deploy** to deploy the Cloud Function.

### Configure access permissions

Next, give the Cloud Function permission to start export operations and write to your Cloud Storage bucket.

This Cloud Function uses your project's default service account to authenticate and authorize its export operations. When you create a project, a default service account is created for you with the following name:

``` text
project_id@appspot.gserviceaccount.com
```

This service account needs permission to start export operations and to write to your Cloud Storage bucket. To grant these permissions, assign the following IAM roles to the default service account:

  - `  Cloud Datastore Import Export Admin  `
  - `  Storage Object User  ` role on the bucket

You can use the Google Cloud CLI to assign these roles. You can access this tool from [Cloud Shell](/shell) in the Google Cloud console:  

1.  Assign the **Cloud Datastore Import Export Admin** role. Replace project\_id , and run the following command:
    
    ``` text
    gcloud projects add-iam-policy-binding project_id \
        --member serviceAccount:project_id@appspot.gserviceaccount.com \
        --role roles/datastore.importExportAdmin
    ```

2.  Assign the **Storage Object User** role on your bucket. Replace bucket\_name and project\_id , and run the following command:
    
    ``` text
    gcloud storage buckets add-iam-policy-binding gs://bucket_name \
        --member=serviceAccount:project_id@appspot.gserviceaccount.com \
        --role=roles/storage.objectUser
    ```

### Create a Cloud Scheduler job

Next, create a Cloud Scheduler job that calls the `  datastore_export  ` Cloud Function:

1.  Go to the **Cloud Scheduler** page in the Google Cloud console:

2.  Click **Create Job** .

3.  Enter a **Name** for the job such as `  scheduledDatastoreExport  ` .

4.  Enter a **Frequency** in [unix-cron format](/scheduler/docs/configuring/cron-job-schedules) .

5.  Select a **Timezone** .

6.  Under **Target** , select **Pub/Sub** . In the **Topic** field, enter the name of the pub/sub topic you defined alongside your Cloud Function, `  startDatastoreExport  ` in the example above.

7.  In the **Payload** field, enter a JSON object to configure the export operation. The `  datastore_export  ` Cloud Function requires a `  bucket  ` value. You can optionally include `  kinds  ` or `  namespaceIDs  ` values to set an entity filter, for example:
    
    ### Export all entities
    
    ``` text
    {
    "bucket": "gs://bucket_name"
    }
    ```
    
    ### Export with entity filter
    
      - Export entities of kind `  User  ` or `  Task  ` from all namespaces:
        
        ``` text
        {
        "bucket": "gs://bucket_name",
        "kinds": ["User", "Task"]
        }
        ```
    
      - Export entities of kind `  User  ` or `  Task  ` from the default and `  Testers  ` namespaces. Use an empty string ( `  ""  ` ) to specify the default namespace:
        
        ``` text
        {
        "bucket": "gs://bucket_name",
        "kinds": ["User", "Task"],
        "namespaceIds": ["", "Testers"]
        }
        ```
    
      - Export entities of any kind from the default and `  Testers  ` namespaces. Use an empty string ( `  ""  ` ) to specify the default namespace:
        
        ``` text
        {
        "bucket": "gs://bucket_name",
        "namespaceIds": ["", "Testers"]
        }
        ```
    
    Where `  bucket_name  ` is the name of your Cloud Storage bucket.

8.  Click **Create** .

## Test your scheduled exports

To test your Cloud Function and Cloud Scheduler job, run your Cloud Scheduler job in the **Cloud Scheduler** page of the Google Cloud console. If successful, this initiates a real export operation.

1.  Go to the **Cloud Scheduler** page in the Google Cloud console.  

2.  In the row for your new Cloud Scheduler job, click **Run now** .
    
    After a few seconds, click **Refresh** . The Cloud Scheduler job should update the result column to **Success** and **Last run** to the current time.

The Cloud Scheduler page confirms only that the job sent a message to the pub/sub topic. To see if your export request succeeded, view the logs of your Cloud Function.

### View the Cloud Function logs

To see if the Cloud Function successfully started an export operation, see the **Logs Explorer** page in the Google Cloud console.

The log for the Cloud Function reports errors and successful export initiations.

### View export progress

You can use the `  gcloud datastore operations list  ` command to view the progress of your export operations, see [listing all long-running operations](/datastore/docs/export-import-entities#listing_all_long-running_operations) .

After an export operation completes, you can view the output files in your Cloud Storage bucket. The managed export service uses a timestamp to organize your export operations:
