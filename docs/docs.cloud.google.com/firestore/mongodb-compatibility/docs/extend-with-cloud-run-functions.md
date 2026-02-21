# Extend Firestore with MongoDB compatibility with event triggers using Cloud Run functions

With Cloud Run functions, you can deploy code to handle events triggered by changes in your Cloud Run database. This lets you add server-side functionality without running your own servers.

This guide describes how to create triggers for Cloud Run functions from Firestore events.

You can trigger your Cloud Run functions from events in a Firestore database. When triggered, your function reads and updates a Firestore database in response to these events through the [Firestore APIs and client libraries](/firestore/docs/apis) .

The process of Firestore events triggering a Cloud Run function consists of the following steps:

1.  The service waits for changes to a particular document.

2.  When a change occurs, the service is triggered and performs its tasks.

3.  The service receives a data object with a snapshot of the affected document. For `  write  ` or `  update  ` events, the data object contains snapshots representing document state before and after the triggering event.

## Before you begin

1.  Make sure you have set up a new project for Cloud Run as described in the [setup](/run/docs/setup) page.

2.  Enable the Artifact Registry, Cloud Build, Cloud Run Admin API, Eventarc, Firestore Cloud Logging, and Pub/Sub APIs:

### Required roles

You or your administrator must grant the deployer account and the trigger identity. Optionally, grant the Pub/Sub service agent the following IAM roles.

#### Required roles for the deployer account

To get the permissions that you need to trigger from Firestore events, ask your administrator to grant you the following IAM roles on your project:

  - [Cloud Build Editor](/iam/docs/roles-permissions/cloudbuild#cloudbuild.builds.editor) ( `  roles/cloudbuild.builds.editor  ` )
  - [Cloud Run Admin](/iam/docs/roles-permissions/run#run.admin) ( `  roles/run.admin  ` )
  - [Datastore Owner](/iam/docs/roles-permissions/firestore#datastore.owner) ( `  roles/datastore.owner  ` )
  - [Eventarc Admin](/iam/docs/roles-permissions/eventarc#eventarc.admin) ( `  roles/eventarc.admin  ` )
  - [Logs View Accessor](/iam/docs/roles-permissions/logging#logging.viewAccessor) ( `  roles/logging.viewAccessor  ` )
  - [Project IAM Admin](/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `  roles/resourcemanager.projectIamAdmin  ` )
  - [Service Account Admin](/iam/docs/roles-permissions/iam#iam.serviceAccountAdmin) ( `  roles/iam.serviceAccountAdmin  ` )
  - [Service Account User](/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `  roles/iam.serviceAccountUser  ` )
  - [Service Usage Admin](/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageAdmin) ( `  roles/serviceusage.serviceUsageAdmin  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

Note that by default, [Cloud Build permissions include permissions to upload and download Artifact Registry artifacts](/artifact-registry/docs/access-control#gcp) .

#### Required roles for the trigger identity

1.  Make note of the [Compute Engine default service account](/iam/docs/service-account-types#default) as you will you attach it to an Eventarc trigger to represent the identity of the trigger for testing purposes. This service account is automatically created after enabling or using a Google Cloud service that uses Compute Engine, and with the following email format:
    
    ``` text
    PROJECT_NUMBER-compute@developer.gserviceaccount.com
    ```
    
    Replace `  PROJECT_NUMBER  ` with your Google Cloud project number. You can find your project number on the [Welcome](https://console.cloud.google.com/welcome) page of the Google Cloud console or by running the following command:
    
    ``` text
    gcloud projects describe PROJECT_ID --format='value(projectNumber)'
    ```
    
    For production environments, we strongly recommend [creating a new service account](/iam/docs/service-accounts-create) and granting it one or more IAM roles that contain the [minimum permissions required](/iam/docs/best-practices-service-accounts#limit-service-account-privileges) and follow the principle of [least privilege](/iam/docs/using-iam-securely#least_privilege) .
    
    **Note:**
    
    The [`  iam.automaticIamGrantsForDefaultServiceAccounts  ` organization policy constraint](/resource-manager/docs/organization-policy/restricting-service-accounts#disable_service_account_default_grants) prevents the Editor role from being automatically granted to default service accounts. If you created your organization after May 3, 2024, this constraint is enforced by default.
    
    We strongly recommend that you enforce this constraint to disable the automatic role grant. If you disable the automatic role grant, you must decide which roles to grant to the default service accounts, and then [grant these roles](/iam/docs/granting-changing-revoking-access) yourself.
    
    If the default service account already has the Editor role, we recommend that you replace the Editor role with less permissive roles.To safely modify the service account's roles, use [Policy Simulator](/policy-intelligence/docs/simulate-iam-policies) to see the impact of the change, and then [grant and revoke the appropriate roles](/iam/docs/granting-changing-revoking-access) .

2.  By default, Cloud Run services are only callable by Project Owners, Project Editors, and Cloud Run Admins and Invokers. You can [control access on a per-service basis](/run/docs/securing/managing-access#control-service-or-job-access) ; however, for testing purposes, grant the [Cloud Run Invoker role](/iam/docs/roles-permissions/run#run.invoker) ( `  run.invoker  ` ) on the Google Cloud project to the Compute Engine service account. This grants the role on all Cloud Run services and jobs in a project.
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member=serviceAccount:PROJECT_NUMBER-compute@developer.gserviceaccount.com \
        --role=roles/run.invoker
    ```
    
    Note that if you create a trigger for an authenticated Cloud Run service without granting the Cloud Run Invoker role, the trigger is created successfully and is active. However, the trigger will not work as expected and a message similar to the following appears in the logs:
    
    `  The request was not authenticated. Either allow unauthenticated invocations or set the proper Authorization header.  `

3.  Grant the [Eventarc Event Receiver role](/iam/docs/roles-permissions/eventarc#eventarc.eventReceiver) ( `  roles/eventarc.eventReceiver  ` ) on the project to the Compute Engine default service account so that the Eventarc trigger can receive events from event providers.
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member=serviceAccount:PROJECT_NUMBER-compute@developer.gserviceaccount.com \
        --role=roles/eventarc.eventReceiver
    ```

#### Optional role for the Pub/Sub service agent

  - If you enabled the Cloud Pub/Sub service agent on or before April 8, 2021, to support authenticated Pub/Sub push requests, grant the [Service Account Token Creator role](/iam/docs/roles-permissions/iam#iam.serviceAccountTokenCreator) ( `  roles/iam.serviceAccountTokenCreator  ` ) to the service agent. Otherwise, this role is granted by default:
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member=serviceAccount:service-PROJECT_NUMBER@gcp-sa-pubsub.iam.gserviceaccount.com \
        --role=roles/iam.serviceAccountTokenCreator
    ```

## Set up your Firestore database

Before you deploy your service, you must create a Firestore database:

1.  Go to the [Firestore page](https://console.cloud.google.com/firestore/databases) .

2.  Click **Create a Firestore database** .

3.  In the **Name your database** field, enter a *Database ID* , such as `  firestore-db  ` .

4.  Select Enterprise Edition

5.  In **Location type** , select **Region** and choose the region for where your database is to reside. This choice is permanent.

6.  Click **Create database** .

The Cloud Run data model consists of collections that contain documents. A document contains a set of key-value pairs.

## Write a Firestore-triggered function

To write a function that responds to Firestore events, prepare to specify the following during deployment:

  - [a trigger event type](#event_types)
  - [a trigger event filter to select the documents associated with the function](#trigger_event_filters)
  - [the function code to run](#function_code)

### Event types

Firestore supports `  create  ` , `  update  ` , `  delete  ` , and `  write  ` events. The `  write  ` event encompasses all modifications to a document.

<table>
<thead>
<tr class="header">
<th>Event type</th>
<th>Trigger</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.created      </code> (default)</td>
<td>Triggered when a document is written to for the first time.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.updated      </code></td>
<td>Triggered when a document already exists and has any value changed.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.deleted      </code></td>
<td>Triggered when a document with data is deleted.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.written      </code></td>
<td>Triggered when a document is created, updated or deleted.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.created.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       created      </code> but adds authentication information.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.updated.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       updated      </code> but adds authentication information.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.deleted.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       deleted      </code> but adds authentication information.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.firestore.document.v1.written.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       written      </code> but adds authentication information.</td>
</tr>
</tbody>
</table>

**Note:** You set triggers at the document level. It is not possible to create a trigger activated by changes to a specific field or collection.

Wildcards are written in triggers using curly braces. For example:

`  projects/ YOUR_PROJECT_ID /databases/ YOUR_DATABASE_ID /documents/collection/{document_wildcard}  `

### Trigger event filters

To trigger your service, specify a document path to listen to. The document path must be in the same Google Cloud project as the service.

Here are a few examples of valid document paths:

  - `  users/marie  ` : Monitors a single document, `  /users/marie  ` .

  - `  users/{username}  ` : Monitors all user documents. Wildcards are used to monitor all documents in the collection.

#### Wildcards and parameters

If you don't know the specific document you want to monitor, use a `  {wildcard}  ` instead of the document ID:

  - `  users/{username}  ` listens for changes to all user documents.

In this example, when any field on any document in `  users  ` is changed, it matches a wildcard called `  {username}  ` .

Wildcard matches are extracted from document paths. You can define as many wildcards as you like to substitute explicit collection or document IDs. You can use up to *one* multi-segment wildcard like `  {username=**}  ` .

### Function code

See [examples](#examples) for how to use Firestore events to trigger a Cloud Run function.

#### Include the proto dependencies in your source

You must include the [Cloud Run `  data.proto  `](https://github.com/googleapis/google-cloudevents/blob/main/proto/google/events/cloud/firestore/v1/data.proto) file in the source directory for your function. This file imports the following protos which you must also include in your source directory:

  - [`  google/protobuf/struct.proto  `](https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/struct.proto)
  - [`  google/protobuf/timestamp.proto  `](https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/timestamp.proto)
  - [`  google/type/latlng.proto  `](https://github.com/googleapis/googleapis/blob/master/google/type/latlng.proto)

Use the same directory structure for the dependencies. For example, place `  struct.proto  ` within `  google/protobuf  ` .

These files are required to decode event data. If your function source does not include these files, it returns an error when it runs.

#### Event attributes

Each event includes [data attributes](/eventarc/docs/workflows/cloudevents#payload-format) that include information about the event such as the time the event triggered. Cloud Run adds additional data about the database and document involved in the event. You can access these attributes as follows:

##### Java

``` text
logger.info("Function triggered by event on: " + event.getSource());
logger.info("Event type: " + event.getType());
logger.info("Event time " + event.getTime());
logger.info("Event project: " + event.getExtension("project"));
logger.info("Event location: " + event.getExtension("location"));
logger.info("Database name: " + event.getExtension("database"));
logger.info("Database document: " + event.getExtension("document"));
// For withAuthContext events
logger.info("Auth information: " + event.getExtension("authid"));
logger.info("Auth information: " + event.getExtension("authtype"));
```

##### Node.js

``` text
console.log(`Function triggered by event on: ${cloudEvent.source}`);
console.log(`Event type: ${cloudEvent.type}`);
console.log(`Event time: ${cloudEvent.time}`);
console.log(`Event project: ${cloudEvent.project}`);
console.log(`Event location: ${cloudEvent.location}`);
console.log(`Database name: ${cloudEvent.database}`);
console.log(`Document name: ${cloudEvent.document}`);
// For withAuthContext events
console.log(`Auth information: ${cloudEvent.authid}`);
console.log(`Auth information: ${cloudEvent.authtype}`);
```

##### Python

``` text
print(f"Function triggered by change to: {cloud_event['source']}")
print(f"Event type: {cloud_event['type']}")
print(f"Event time: {cloud_event['time']}")
print(f"Event project: {cloud_event['project']}")
print(f"Location: {cloud_event['location']}")
print(f"Database name: {cloud_event['database']}")
print(f"Document: {cloud_event['document']}")
// For withAuthContext events
print(f"Auth information: {cloud_event['authid']}")
print(f"Auth information: {cloud_event['authtype']}")
```

## Event structures

This trigger invokes your service with an event similar to:

``` text
{
    "oldValue": { // Update and Delete operations only
        A Document object containing a pre-operation document snapshot
    },
    "updateMask": { // Update operations only
        A DocumentMask object that lists changed fields.
    },
    "value": {
        // A Document object containing a post-operation document snapshot
    }
}
```

Each `  Document  ` object contains one or more `  Value  ` objects. See the [`  Value  ` documentation](/firestore/docs/reference/rest/v1/Value) for type references.

## Create triggers for functions

Click the tab for instructions using the tool of your choice.

### Console

When you use the Google Cloud console to create a function, you can also add a trigger to your function. Follow these steps to create a trigger for your function:

1.  In the Google Cloud console, go to Cloud Run:

2.  Click **Write a function** , and enter the function details. For more information about configuring functions during deployment, see [Deploy functions](/run/docs/deploy-functions#console) .

3.  In the **Trigger** section, click **Add trigger** .

4.  Select **Firestore trigger** .

5.  In the **Eventarc trigger** pane, modify the trigger details as follows:
    
    1.  Enter a name for the trigger in the **Trigger name** field, or use the default name.
    
    2.  Select a **Trigger type** from the list:
        
          - **Google Sources** to specify triggers for Pub/Sub, Cloud Storage, Firestore, and other Google event providers.
        
          - **Third-party** to integrate with non-Google providers that offer an Eventarc source. For more information, see [Third-party events in Eventarc](/eventarc/docs/third-parties/third-parties-overview) .
    
    3.  Select **Firestore** from the **Event provider** list, to select a product that provides the type of event for triggering your function. For the list of event providers, see [Event providers and destinations](/eventarc/docs/event-providers-targets) .
    
    4.  Select **type=google.cloud.firestore.document.v1.created** from the **Event type** list. Your trigger configuration varies depending on the supported event type. For more information, see [Event types](/eventarc/docs/event-types) .
    
    5.  In the Filters section, select a database, operation and attribute values, or use the default selections.
    
    6.  If the **Region** field is enabled, select a [location](/eventarc/docs/overview#trigger-location) for the Eventarc trigger. In general, the location of an Eventarc trigger should match the location of the Google Cloud resource that you want to monitor for events. In most scenarios, you should also deploy your function in the same region. See [Understand Eventarc locations](/eventarc/docs/understand-locations) for more details about Eventarc trigger locations.
    
    7.  In the **Service account** field, select a service account. Eventarc triggers are linked to service accounts to use as an identity when invoking your function. Your Eventarc trigger's service account must have the permission to invoke your function. By default, Cloud Run uses the [Compute Engine default service account](/compute/docs/access/service-accounts#default_service_account) .
    
    8.  Optionally, specify the **Service URL path** to send the incoming request to. This is the relative path on the destination service to which the events for the trigger should be sent. For example: `  /  ` , `  /route  ` , `  route  ` , and `  route/subroute  ` .

6.  Once you've completed the required fields, click **Save trigger** .

7.  Click **Create** .

8.  In the **Source** tab, edit the source code if needed, then select **Save and redeploy** .

### gcloud

When you create a function using the gcloud CLI, you must first [deploy](/run/docs/deploy-functions) your function, and then create a trigger. Follow these steps to create a trigger for your function:

1.  Run the following command in the directory that contains the sample code to deploy your function:
    
    ``` text
    gcloud run deploy FUNCTION \
            --source . \
            --function FUNCTION_ENTRYPOINT \
            --base-image BASE_IMAGE_ID \
            --region REGION
    ```
    
    Replace:
    
      - FUNCTION with the name of the function you are deploying. You can omit this parameter entirely, but you will be prompted for the name if you omit it.
    
      - FUNCTION\_ENTRYPOINT with the entry point to your function in your source code. This is the code Cloud Run executes when your function runs. The value of this flag must be a function name or fully-qualified class name that exists in your source code.
    
      - BASE\_IMAGE\_ID with the base image environment for your function. For more details about base images and the packages included in each image, see [Runtimes base images](/run/docs/configuring/services/runtime-base-images#how_to_obtain_base_images) .
    
      - REGION with the Google Cloud [region](/run/docs/locations) where you want to deploy your function. For example, `  europe-west1  ` .

2.  Run the following command to create a trigger that filters events:
    
    ``` text
    gcloud eventarc triggers create TRIGGER_NAME  \
        --location=EVENTARC_TRIGGER_LOCATION \
        --destination-run-service=FUNCTION  \
        --destination-run-region=REGION \
        --event-filters="type=google.cloud.firestore.document.v1.created" \
        --service-account=PROJECT_NUMBER-compute@developer.gserviceaccount.com
    ```
    
    Replace:
    
      - TRIGGER\_NAME with the name for your trigger.
    
      - EVENTARC\_TRIGGER\_LOCATION with the location for the Eventarc trigger. In general, the location of an Eventarc trigger should match the location of the Google Cloud resource that you want to monitor for events. In most scenarios, you should also deploy your function in the same region. For more information, see [Eventarc locations](/eventarc/docs/locations) .
    
      - FUNCTION with the name of the function you are deploying.
    
      - REGION with the Cloud Run [region](/run/docs/locations) of the function.
    
      - PROJECT\_NUMBER with your Google Cloud project number. Eventarc triggers are linked to service accounts to use as an identity when invoking your function. Your Eventarc trigger's service account must have the permission to invoke your function. By default, Cloud Run uses the Default compute service account.
    
    Each `  event-filters  ` flag specifies a type of event, with the function triggering only when an event meets all of the criteria specified in its `  event-filters  ` flags. Each trigger must have an `  event-filters  ` flag specifying a supported [event type](/eventarc/docs/reference/supported-events#directly-from-a-google-cloud-source) , such as a new document written to Firestore or a file uploaded to Cloud Storage. You can't change the event filter type after creation. To change the event filter type, you must create a new trigger and delete the old one. Optionally, you can repeat the `  --event-filters  ` flag with a supported filter in the form `  ATTRIBUTE=VALUE  ` to add more filters.

### Terraform

To create an Eventarc trigger for a Cloud Run function, see [Create a trigger using Terraform](/eventarc/docs/creating-triggers-terraform) .

## Examples

The following examples describe how to use Firestore events to trigger a Cloud Run function.

### Example 1: Hello Firestore function

The following sample prints the fields of a triggering Firestore event:

### Node.js

``` javascript
/**
 * Cloud Event Function triggered by a change to a Firestore document.
 */
const functions = require('@google-cloud/functions-framework');
const protobuf = require('protobufjs');

functions.cloudEvent('helloFirestore', async cloudEvent => {
  console.log(`Function triggered by event on: ${cloudEvent.source}`);
  console.log(`Event type: ${cloudEvent.type}`);

  console.log('Loading protos...');
  const root = await protobuf.load('data.proto');
  const DocumentEventData = root.lookupType(
    'google.events.cloud.firestore.v1.DocumentEventData'
  );

  console.log('Decoding data...');
  const firestoreReceived = DocumentEventData.decode(cloudEvent.data);

  console.log('\nOld value:');
  console.log(JSON.stringify(firestoreReceived.oldValue, null, 2));

  console.log('\nNew value:');
  console.log(JSON.stringify(firestoreReceived.value, null, 2));
});
```

### Python

``` python
from cloudevents.http import CloudEvent
import functions_framework
from google.events.cloud import firestore


@functions_framework.cloud_event
def hello_firestore(cloud_event: CloudEvent) -> None:
    """Triggers by a change to a Firestore document.

    Args:
        cloud_event: cloud event with information on the firestore event trigger
    """
    firestore_payload = firestore.DocumentEventData()
    firestore_payload._pb.ParseFromString(cloud_event.data)

    print(f"Function triggered by change to: {cloud_event['source']}")

    print("\nOld value:")
    print(firestore_payload.old_value)

    print("\nNew value:")
    print(firestore_payload.value)
```

### Go

``` go
// Package hellofirestore contains a Cloud Event Function triggered by a Cloud Firestore event.
package hellofirestore

import (
 "context"
 "fmt"

 "github.com/GoogleCloudPlatform/functions-framework-go/functions"
 "github.com/cloudevents/sdk-go/v2/event"
 "github.com/googleapis/google-cloudevents-go/cloud/firestoredata"
 "google.golang.org/protobuf/proto"
)

func init() {
 functions.CloudEvent("helloFirestore", HelloFirestore)
}

// HelloFirestore is triggered by a change to a Firestore document.
func HelloFirestore(ctx context.Context, event event.Event) error {
 var data firestoredata.DocumentEventData

 // If you omit `DiscardUnknown`, protojson.Unmarshal returns an error
 // when encountering a new or unknown field.
 options := proto.UnmarshalOptions{
     DiscardUnknown: true,
 }
 err := options.Unmarshal(event.Data(), &data)

 if err != nil {
     return fmt.Errorf("proto.Unmarshal: %w", err)
 }

 fmt.Printf("Function triggered by change to: %v\n", event.Source())
 fmt.Printf("Old value: %+v\n", data.GetOldValue())
 fmt.Printf("New value: %+v\n", data.GetValue())
 return nil
}
```

### Java

``` java
import com.google.cloud.functions.CloudEventsFunction;
import com.google.events.cloud.firestore.v1.DocumentEventData;
import com.google.protobuf.InvalidProtocolBufferException;
import io.cloudevents.CloudEvent;
import java.util.logging.Logger;

public class FirebaseFirestore implements CloudEventsFunction {
  private static final Logger logger = Logger.getLogger(FirebaseFirestore.class.getName());

  @Override
  public void accept(CloudEvent event) throws InvalidProtocolBufferException {
    DocumentEventData firestoreEventData = DocumentEventData
        .parseFrom(event.getData().toBytes());

    logger.info("Function triggered by event on: " + event.getSource());
    logger.info("Event type: " + event.getType());

    logger.info("Old value:");
    logger.info(firestoreEventData.getOldValue().toString());

    logger.info("New value:");
    logger.info(firestoreEventData.getValue().toString());
  }
}
```

### C\#

``` csharp
using CloudNative.CloudEvents;
using Google.Cloud.Functions.Framework;
using Google.Events.Protobuf.Cloud.Firestore.V1;
using Microsoft.Extensions.Logging;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Threading.Tasks;

namespace FirebaseFirestore;

public class Function : ICloudEventFunction<DocumentEventData>
{
    private readonly ILogger _logger;

    public Function(ILogger<Function> logger) =>
        _logger = logger;

    public Task HandleAsync(CloudEvent cloudEvent, DocumentEventData data, CancellationToken cancellationToken)
    {
        _logger.LogInformation("Function triggered by event on {subject}", cloudEvent.Subject);
        _logger.LogInformation("Event type: {type}", cloudEvent.Type);
        MaybeLogDocument("Old value", data.OldValue);
        MaybeLogDocument("New value", data.Value);

        // In this example, we don't need to perform any asynchronous operations, so the
        // method doesn't need to be declared async.
        return Task.CompletedTask;
    }

    /// <summary>
    /// Logs the names and values of the fields in a document in a very simplistic way.
    /// </summary>
    private void MaybeLogDocument(string message, Document document)
    {
        if (document is null)
        {
            return;
        }

        // ConvertFields converts the Firestore representation into a .NET-friendly
        // representation.
        IReadOnlyDictionary<string, object> fields = document.ConvertFields();
        var fieldNamesAndTypes = fields
            .OrderBy(pair => pair.Key)
            .Select(pair => $"{pair.Key}: {pair.Value}");
        _logger.LogInformation(message + ": {fields}", string.Join(", ", fieldNamesAndTypes));
    }
}
```

#### Deploy the function

To deploy the `  Hello Firestore  ` function, run the following command:

If you haven't already done so, set up your [Firestore database](/run/docs/triggering/firestore-triggers#set_up_your_database) .

To deploy the function, see [Create triggers for functions](#trigger-functions) .

#### Test the function

To test the `  Hello Firestore  ` function, set up a collection called `  users  ` in your [Firestore database](/run/docs/triggering/firestore-triggers#set_up_your_database) :

1.  In the Google Cloud console, go to the Firestore databases page:

2.  In the **View actions** menu next to **Collections** , click **Create collection** ..

3.  Specify `  users  ` as the collection ID.

4.  To start adding the collection's first document, under **Add its first document** accept the auto-generated **Document ID** .

5.  Add at least one field for the document, specifying a name and value. For example, in **Field name** , enter `  username  ` , and in **Field value** , enter `  rowan  ` .

6.  When you're done, click **Save** .
    
    This action creates a new document, thereby triggering your function.

7.  To confirm that your function was triggered, click the linked name of the function in the Google Cloud console [Cloud Run Overview page](https://console.cloud.google.com/run) to open the **Service details** page.

8.  Select the **Logs** tab and look for this string:

<!-- end list -->

``` text
Function triggered by change to: //firestore.googleapis.com/projects/your-project-id/databases/(default)'
```

### Example 2: Convert to Uppercase function

The following example retrieves the value added by the user, converts the string at that location to uppercase, and replaces the value with the uppercase string:

### Node.js

Use [protobufjs](https://www.npmjs.com/package/protobufjs) to decode the event data. Include the `  google.events.cloud.firestore.v1  ` [`  data.proto  `](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/tree/main/functions/v2/firebase/firestore/helloFirestore) in your source.

``` javascript
const functions = require('@google-cloud/functions-framework');
const Firestore = require('@google-cloud/firestore');
const protobuf = require('protobufjs');

const firestore = new Firestore({
  projectId: process.env.GOOGLE_CLOUD_PROJECT,
});

// Converts strings added to /messages/{pushId}/original to uppercase
functions.cloudEvent('makeUpperCase', async cloudEvent => {
  console.log('Loading protos...');
  const root = await protobuf.load('data.proto');
  const DocumentEventData = root.lookupType(
    'google.events.cloud.firestore.v1.DocumentEventData'
  );

  console.log('Decoding data...');
  const firestoreReceived = DocumentEventData.decode(cloudEvent.data);

  const resource = firestoreReceived.value.name;
  const affectedDoc = firestore.doc(resource.split('/documents/')[1]);

  const curValue = firestoreReceived.value.fields.original.stringValue;
  const newValue = curValue.toUpperCase();

  if (curValue === newValue) {
    // Value is already upper-case
    // Don't perform a(nother) write to avoid infinite loops
    console.log('Value is already upper-case.');
    return;
  }

  console.log(`Replacing value: ${curValue} --> ${newValue}`);
  affectedDoc.set({
    original: newValue,
  });
});
```

### Python

``` python
from cloudevents.http import CloudEvent
import functions_framework
from google.cloud import firestore
from google.events.cloud import firestore as firestoredata

client = firestore.Client()


# Converts strings added to /messages/{pushId}/original to uppercase
@functions_framework.cloud_event
def make_upper_case(cloud_event: CloudEvent) -> None:
    firestore_payload = firestoredata.DocumentEventData()
    firestore_payload._pb.ParseFromString(cloud_event.data)

    path_parts = firestore_payload.value.name.split("/")
    separator_idx = path_parts.index("documents")
    collection_path = path_parts[separator_idx + 1]
    document_path = "/".join(path_parts[(separator_idx + 2) :])

    print(f"Collection path: {collection_path}")
    print(f"Document path: {document_path}")

    affected_doc = client.collection(collection_path).document(document_path)

    cur_value = firestore_payload.value.fields["original"].string_value
    new_value = cur_value.upper()

    if cur_value != new_value:
        print(f"Replacing value: {cur_value} --> {new_value}")
        affected_doc.set({"original": new_value})
    else:
        # Value is already upper-case
        # Don't perform a second write (which can trigger an infinite loop)
        print("Value is already upper-case.")
```

### Go

``` go
// Package upper contains a Firestore Cloud Function.
package upper

import (
 "context"
 "errors"
 "fmt"
 "log"
 "os"
 "strings"

 "cloud.google.com/go/firestore"
 firebase "firebase.google.com/go/v4"
 "github.com/GoogleCloudPlatform/functions-framework-go/functions"
 "github.com/cloudevents/sdk-go/v2/event"
 "github.com/googleapis/google-cloudevents-go/cloud/firestoredata"
 "google.golang.org/protobuf/proto"
)

// set the GOOGLE_CLOUD_PROJECT environment variable when deploying.
var projectID = os.Getenv("GOOGLE_CLOUD_PROJECT")

// client is a Firestore client, reused between function invocations.
var client *firestore.Client

func init() {
 // Use the application default credentials.
 conf := &firebase.Config{ProjectID: projectID}

 // Use context.Background() because the app/client should persist across
 // invocations.
 ctx := context.Background()

 app, err := firebase.NewApp(ctx, conf)
 if err != nil {
     log.Fatalf("firebase.NewApp: %v", err)
 }

 client, err = app.Firestore(ctx)
 if err != nil {
     log.Fatalf("app.Firestore: %v", err)
 }

 // Register cloud event function
 functions.CloudEvent("MakeUpperCase", MakeUpperCase)
}

// MakeUpperCase is triggered by a change to a Firestore document. It updates
// the `original` value of the document to upper case.
func MakeUpperCase(ctx context.Context, e event.Event) error {
 var data firestoredata.DocumentEventData

 // If you omit `DiscardUnknown`, protojson.Unmarshal returns an error
 // when encountering a new or unknown field.
 options := proto.UnmarshalOptions{
     DiscardUnknown: true,
 }
 err := options.Unmarshal(e.Data(), &data)

 if err != nil {
     return fmt.Errorf("proto.Unmarshal: %w", err)
 }

 if data.GetValue() == nil {
     return errors.New("Invalid message: 'Value' not present")
 }

 fullPath := strings.Split(data.GetValue().GetName(), "/documents/")[1]
 pathParts := strings.Split(fullPath, "/")
 collection := pathParts[0]
 doc := strings.Join(pathParts[1:], "/")

 var originalStringValue string
 if v, ok := data.GetValue().GetFields()["original"]; ok {
     originalStringValue = v.GetStringValue()
 } else {
     return errors.New("Document did not contain field \"original\"")
 }

 newValue := strings.ToUpper(originalStringValue)
 if originalStringValue == newValue {
     log.Printf("%q is already upper case: skipping", originalStringValue)
     return nil
 }
 log.Printf("Replacing value: %q -> %q", originalStringValue, newValue)

 newDocumentEntry := map[string]string{"original": newValue}
 _, err = client.Collection(collection).Doc(doc).Set(ctx, newDocumentEntry)
 if err != nil {
     return fmt.Errorf("Set: %w", err)
 }
 return nil
}
```

### Java

``` java
import com.google.cloud.firestore.Firestore;
import com.google.cloud.firestore.FirestoreOptions;
import com.google.cloud.firestore.SetOptions;
import com.google.cloud.functions.CloudEventsFunction;
import com.google.events.cloud.firestore.v1.DocumentEventData;
import com.google.events.cloud.firestore.v1.Value;
import com.google.protobuf.InvalidProtocolBufferException;
import io.cloudevents.CloudEvent;
import java.util.Map;
import java.util.concurrent.ExecutionException;
import java.util.logging.Logger;

public class FirebaseFirestoreReactive implements CloudEventsFunction {
  private static final Logger logger = Logger.getLogger(FirebaseFirestoreReactive.class.getName());
  private final Firestore firestore;

  private static final String FIELD_KEY = "original";
  private static final String APPLICATION_PROTOBUF = "application/protobuf";

  public FirebaseFirestoreReactive() {
    this(FirestoreOptions.getDefaultInstance().getService());
  }

  public FirebaseFirestoreReactive(Firestore firestore) {
    this.firestore = firestore;
  }

  @Override
  public void accept(CloudEvent event)
      throws InvalidProtocolBufferException, InterruptedException, ExecutionException {
    if (event.getData() == null) {
      logger.warning("No data found in event!");
      return;
    }

    if (!event.getDataContentType().equals(APPLICATION_PROTOBUF)) {
      logger.warning(String.format("Found unexpected content type %s, expected %s",
          event.getDataContentType(),
          APPLICATION_PROTOBUF));
      return;
    }

    DocumentEventData firestoreEventData = DocumentEventData
        .parseFrom(event.getData().toBytes());

    // Get the fields from the post-operation document snapshot
    // https://firebase.google.com/docs/firestore/reference/rest/v1/projects.databases.documents#Document
    Map<String, Value> fields = firestoreEventData.getValue().getFieldsMap();
    if (!fields.containsKey(FIELD_KEY)) {
      logger.warning("Document does not contain original field");
      return;
    }
    String currValue = fields.get(FIELD_KEY).getStringValue();
    String newValue = currValue.toUpperCase();

    if (currValue.equals(newValue)) {
      logger.info("Value is already upper-case");
      return;
    }

    // Retrieve the document name from the resource path:
    // projects/{project_id}/databases/{database_id}/documents/{document_path}
    String affectedDoc = firestoreEventData.getValue()
        .getName()
        .split("/documents/")[1]
        .replace("\"", "");

    logger.info(String.format("Replacing values: %s --> %s", currValue, newValue));

    // Wait for the async call to complete
    this.firestore
        .document(affectedDoc)
        .set(Map.of(FIELD_KEY, newValue), SetOptions.merge())
        .get();
  }
}
```

### C\#

``` csharp
using CloudNative.CloudEvents;
using Google.Cloud.Firestore;
using Google.Cloud.Functions.Framework;
using Google.Cloud.Functions.Hosting;
using Google.Events.Protobuf.Cloud.Firestore.V1;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;

namespace FirestoreReactive;

public class Startup : FunctionsStartup
{
    public override void ConfigureServices(WebHostBuilderContext context, IServiceCollection services) =>
        services.AddSingleton(FirestoreDb.Create());
}

// Register the startup class to provide the Firestore dependency.
[FunctionsStartup(typeof(Startup))]
public class Function : ICloudEventFunction<DocumentEventData>
{
    private readonly ILogger _logger;
    private readonly FirestoreDb _firestoreDb;

    public Function(ILogger<Function> logger, FirestoreDb firestoreDb) =>
        (_logger, _firestoreDb) = (logger, firestoreDb);

    public async Task HandleAsync(CloudEvent cloudEvent, DocumentEventData data, CancellationToken cancellationToken)
    {
        // Get the recently-written value. This expression will result in a null value
        // if any of the following is true:
        // - The event doesn't contain a "new" document
        // - The value doesn't contain a field called "original"
        // - The "original" field isn't a string
        string currentValue = data.Value?.ConvertFields().GetValueOrDefault("original") as string;
        if (currentValue is null)
        {
            _logger.LogWarning($"Event did not contain a suitable document");
            return;
        }

        string newValue = currentValue.ToUpperInvariant();
        if (newValue == currentValue)
        {
            _logger.LogInformation("Value is already upper-cased; no replacement necessary");
            return;
        }

        // The CloudEvent subject is "documents/x/y/...".
        // The Firestore SDK FirestoreDb.Document method expects a reference relative to
        // "documents" (so just the "x/y/..." part). This may be simplified over time.
        if (cloudEvent.Subject is null || !cloudEvent.Subject.StartsWith("documents/"))
        {
            _logger.LogWarning("CloudEvent subject is not a document reference.");
            return;
        }
        string documentPath = cloudEvent.Subject.Substring("documents/".Length);

        _logger.LogInformation("Replacing '{current}' with '{new}' in '{path}'", currentValue, newValue, documentPath);
        await _firestoreDb.Document(documentPath).UpdateAsync("original", newValue, cancellationToken: cancellationToken);
    }
}
```

**Note:** Updating the function-triggering Firestore document might create subsequent `  updated  ` events, which might cascade into an infinite loop within your function. To solve this problem, use trigger types that ignore updates (such as `  created  ` ), or configure your function to only write to Firestore if the underlying value has changed.

#### Deploy the function

To deploy the `  Convert to Uppercase  ` function, run the following command:

If you haven't already done so, set up your [Firestore database](/run/docs/triggering/firestore-triggers#set_up_your_database) .

To deploy the function, see [Create triggers for functions](#trigger-functions) .

#### Test the function

To test the `  Convert to Uppercase  ` function you just deployed, set up a collection called `  messages  ` in your [Firestore database](/run/docs/triggering/firestore-triggers#set_up_your_database) :

1.  In the Google Cloud console, go to the Firestore databases page:

2.  In the **View actions** menu next to **Collections** , click **Create collection** .

3.  Specify `  messages  ` as the collection ID.

4.  To start adding the collection's first document, under **Add its first document** accept the auto-generated **Document ID** .

5.  To trigger your deployed function, add a document where the **Field name** is `  original  ` and the **Field value** is `  minka  ` .

6.  When you save the document, you can see the lowercase word in the value field convert to uppercase.
    
    If you subsequently edit the field value to contain lowercase letters, that triggers the function again, converting all lowercase letters to uppercase.

## Limitations for functions

  - Ordering is not guaranteed. Rapid changes can trigger function invocations in an unexpected order.
  - Events are delivered at least once, but a single event might result in multiple function invocations. Avoid depending on exactly-once mechanics, and write [idempotent functions](/blog/products/serverless/cloud-functions-pro-tips-building-idempotent-functions) .
  - A trigger is associated with a single database. You can't create a trigger that matches multiple databases.
  - Deleting a database doesn't automatically delete any triggers for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](/eventarc/docs/managing-triggers#trigger-delete) .
