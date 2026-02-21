With Cloud Run functions and Eventarc, you can deploy code to handle events triggered by changes in your Firestore in Datastore mode database. This allows you to add server-side functionality without running your own servers.

## Datastore mode triggers

Eventarc supports the following Firestore in Datastore mode event triggers to let you create Cloud Run functions (2nd gen) handlers tied to Firestore in Datastore mode events:

<table>
<thead>
<tr class="header">
<th>Event Type</th>
<th>Trigger</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.created      </code></td>
<td>Triggered when an entity is written for the first time.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.updated      </code></td>
<td>Triggered when an entity already exists and has any value changed.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.deleted      </code></td>
<td>Triggered when an entity is deleted.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.written      </code></td>
<td>Triggered when <code dir="ltr" translate="no">       created      </code> , <code dir="ltr" translate="no">       updated      </code> or <code dir="ltr" translate="no">       deleted      </code> is triggered.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.created.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       created      </code> but adds authentication information.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.updated.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       updated      </code> but adds authentication information.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.deleted.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       deleted      </code> but adds authentication information.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       google.cloud.datastore.entity.v1.written.withAuthContext      </code></td>
<td>Same as <code dir="ltr" translate="no">       written      </code> but adds authentication information.</td>
</tr>
</tbody>
</table>

Datastore mode event triggers respond only to entity changes. An update to a Datastore mode entity where data is unchanged (a no-op write) does not generate an update or write event. You cannot generate events for only specific properties.

### Include authentication context in the event

To include additional authentication information about the event, use an event trigger with the `  withAuthContext  ` extension. This extension adds additional information about the principal that triggered the event. It adds the `  authtype  ` and `  authid  ` attributes in addition to the information returned in the base event. See the [`  authcontext  `](https://github.com/cloudevents/spec/blob/main/cloudevents/extensions/authcontext.md) reference for more information about attribute values.

## Write an entity-triggered function

To write a function that responds to Firestore in Datastore mode events, prepare to specify the following during deployment:

  - a trigger event type
  - a trigger event filter to select the entities associated with the function
  - the function code to run

### Trigger event filters

When you specify an event filter, you can specify either an exact entity match or a path pattern. Use a path pattern to match multiple entities with the wildcards `  *  ` or `  **  ` .

For example, you can specify an exact entity match to respond to changes to the following entity:

``` text
users/marie
```

Use wildcards, `  *  ` or `  **  ` , to respond to changes in entities that match a pattern. The `  *  ` wildcard matches a single segment, and the `  **  ` multi-segment wildcard matches zero or more segments in the pattern.

For single segment matches ( `  *  ` ) you can also use a named capture group, such as `  users/{userId}  ` .

The following table demonstrates valid path patterns:

<table>
<thead>
<tr class="header">
<th>Pattern</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       users/*      </code> or <code dir="ltr" translate="no">       users/{userId}      </code></td>
<td>Matches all entities of kind <code dir="ltr" translate="no">       users      </code> . Does not match descendant entities level like <code dir="ltr" translate="no">       /users/marie/messages/33e2IxYBD9enzS50SJ68      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       users/**      </code></td>
<td>Matches all entities of kind <code dir="ltr" translate="no">       users      </code> and all descendant entities like <code dir="ltr" translate="no">       /users/marie/messages/33e2IxYBD9enzS50SJ68      </code></td>
</tr>
</tbody>
</table>

To learn more about path patterns, see [Eventarc path patterns](/eventarc/docs/path-patterns) .

Your trigger must *always* point to an entity, even if you're using a wildcard. See the following examples:

  - `  users/{userId=*}/{messages=*}  ` is not valid because `  {messages=*}  ` is a kind ID.

  - `  users/{userId=*}/{messages}/{messageId=*}  ` *is* valid because `  {messageId=*}  ` always points to an entity.

### Character escaping

The section describes situations that require you to escape characters in kind IDs and entity IDs. Escaping a character lets the event filter correctly interpret the ID.

  - If a kind ID or entity ID includes a `  ~  ` or `  /  ` character, you must escape the ID in your event filter. To escape an ID, use the format `  __esc ENCODED_ID __  ` . Replace ENCODED\_ID with a kind ID or entity ID that has all `  ~  ` and `  /  ` characters replaced by their encoding IDs, which are the following:
    
      - `  ~  ` : `  ~0  `
      - `  /  ` : `  ~1  `
    
    For example, the kind ID `  user/profile  ` becomes `  __escusers~1profile__  ` . An example path pattern with this kind ID is `  __escusers~1profile__/{userId}  `

  - If you use the kind ID or entity ID of either `  .  ` or `  ..  ` in your event filter, you must escape the ID as follows:
    
      - `  .  ` : `  __esc~2__  `
      - `  ..  ` : `  __esc~2~2__  `
    
    You need to escape the `  .  ` character only if the ID is exactly `  .  ` or `  ..  ` . For example, the kind ID `  customers.info  ` does not require escaping.

  - If your kind or entity ID is a numeric value instead of a string value, you must escape the ID with `  __id NUMERIC_VALUE __  ` . For example, the path pattern for an entity of kind `  111  ` and entity ID `  222  ` is `  __id111__/__id222__  ` .

  - If you migrated from [Legacy Cloud Datastore](/datastore/docs/upgrade-to-firestore) to Firestore in Datastore mode, your database might contain legacy IDs in a non-UTF8 encoding. You must escape these IDs with `  __bytes BASE64_ENCODING __  ` . Replace BASE64\_ENCODING with the base-64 encoding of the ID. For example, the path pattern `  Task/{task}  ` with escaping for non-UTF8 kind ID `  Task  ` becomes `  __bytesVGFzaw==__/{task}  ` .

## Example functions

The following sample demonstrates how to receive Datastore mode events. To work with the data involved in an event, look at the `  value  ` and `  old_value  ` fields.

  - `  value  ` : An `  EntityResult  ` object that contains a **post-operation** entity snapshot. This field is not populated for delete events.
  - `  old_value  ` : An `  EntityResult  ` object that contains a **pre-operation** entity snapshot. This field is only populated for update and delete events.

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.functions.CloudEventsFunction;
import com.google.events.cloud.datastore.v1.EntityEventData;
import com.google.protobuf.InvalidProtocolBufferException;
import io.cloudevents.CloudEvent;
import java.util.logging.Logger;

public class Datastore implements CloudEventsFunction {
  private static final Logger logger = Logger.getLogger(Datastore.class.getName());

  @Override
  public void accept(CloudEvent event) throws InvalidProtocolBufferException {
    EntityEventData datastoreEventData = EntityEventData.parseFrom(event.getData().toBytes());

    logger.info("Function triggered by event on: " + event.getSource());
    logger.info("Event type: " + event.getType());

    logger.info("Old value:");
    logger.info(datastoreEventData.getOldValue().toString());

    logger.info("New value:");
    logger.info(datastoreEventData.getValue().toString());
  }
}
```

### Include the proto dependencies in your source

You must include the [Datastore mode `  data.proto  `](https://github.com/googleapis/google-cloudevents/blob/main/proto/google/events/cloud/datastore/v1/data.proto) file in the source directory for your function. This file imports the following protos which you must also include in your source directory:

  - [`  google/protobuf/struct.proto  `](https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/struct.proto)
  - [`  google/protobuf/timestamp.proto  `](https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/timestamp.proto)
  - [`  google/type/latlng.proto  `](https://github.com/googleapis/googleapis/blob/master/google/type/latlng.proto)

Use the same directory structure for the dependencies. For example, place `  struct.proto  ` within `  google/protobuf  ` .

These files are required to decode event data. If your function source does not include these files, it returns an error when it runs.

### Event attributes

Each event includes [data attributes](/eventarc/docs/workflows/cloudevents#payload-format) that include information about the event such as the time the event triggered. Firestore in Datastore mode adds additional data about the database and entity involved in the event. You can access these attributes as follows:

##### Java

``` text
logger.info("Event time " + event.getTime());
logger.info("Event project: " + event.getExtension("project"));
logger.info("Event location: " + event.getExtension("location"));
logger.info("Database name: " + event.getExtension("database"));
logger.info("Database namespace: " + event.getExtension("namespace"));
logger.info("Database entity: " + event.getExtension("entity"));
// For withAuthContext events
logger.info("Auth information: " + event.getExtension("authid"));
logger.info("Auth information: " + event.getExtension("authtype"));
```

## Deploy a function

Users deploying Cloud Run functions must have the [Cloud Run functions Developer](/functions/docs/reference/iam/roles#cloudfunctions.developer) IAM role or a role that includes the same permissions. See also [Additional configuration for deployment](/functions/docs/reference/iam/roles#additional-configuration) .

You can deploy a function using either the gcloud CLI or the Google Cloud console. The example below demonstrates deployment with the gcloud CLI. For details on deployment with the Google Cloud console, see [Deploy Cloud Run functions](/functions/docs/deploy#console) .

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  gcloud functions deploy  `](/sdk/gcloud/reference/functions/deploy) command to deploy a function:
    
    ``` bash
    gcloud functions deploy FUNCTION_NAME \
    --gen2 \
    --region=FUNCTION_LOCATION \
    --trigger-location=TRIGGER_LOCATION \
    --runtime=RUNTIME \
    --source=SOURCE_LOCATION \
    --entry-point=CODE_ENTRYPOINT \
    --trigger-event-filters="type=EVENT_FILTER_TYPE" \
    --trigger-event-filters="database=DATABASE" \
    --trigger-event-filters="namespace=NAMESPACE" \
    --trigger-event-filters-path-pattern="entity=ENTITY_OR_PATH" \
    ```
    
    The first argument, FUNCTION\_NAME , is a name for your deployed function. The function name must start with a letter followed by up to 62 letters, numbers, hyphens, or underscores, and must end with a letter or a number. Replace FUNCTION\_NAME with a valid function name. Then, add the following flags:
    
      - The [`  --gen2  `](/sdk/gcloud/reference/functions/deploy#--gen2) flag specifies that you want to deploy to Cloud Run functions (2nd gen). Omitting this flag results in deployment to Cloud Run functions (1st gen).
    
      - The [`  --region= FUNCTION_LOCATION  `](/sdk/gcloud/reference/functions/deploy#--region) flag specifies the region in which to deploy your function.
        
        To maximize proximity, set FUNCTION\_LOCATION to a region near your Firestore database. If your Firestore database is in a multi-region location, set the value to `  us-central1  ` for databases in `  nam5  ` and to `  europe-west4  ` for databases in `  eur3  ` . For regional Firestore locations, set to the same region.
    
      - The [`  --trigger-location= TRIGGER_LOCATION  `](/sdk/gcloud/reference/functions/deploy?_gl#--trigger-location) flag specifies the location of the trigger. You must set TRIGGER\_LOCATION to the location of your Datastore mode database.
    
      - The [`  --runtime= RUNTIME  `](/sdk/gcloud/reference/functions/deploy#--runtime) flag specifies which language runtime your function uses. Cloud Run functions supports several runtimes. See [Runtimes](/functions/docs/concepts/exec#runtimes) for more information. Set RUNTIME to a supported runtime.
    
      - The [`  --source= SOURCE_LOCATION  `](/sdk/gcloud/reference/functions/deploy#--source) flag specifies the location of your function source code. See the following for details:
        
          - [Deploy from your local machine](/functions/docs/deploy#from-local-machine)
          - [Deploy from Cloud Storage](/functions/docs/deploy#from-cloud-storage)
          - [Deploy from a source repository](/functions/docs/deploy#from-source-repo)
        
        Set SOURCE\_LOCATION to the location of your function source code.
    
      - The [`  --entry-point= CODE_ENTRYPOINT  `](/sdk/gcloud/reference/functions/deploy#--entry-point) flag specifies the entry point to your function in your source code. This is the code that your function executes when it runs. You must set CODE\_ENTRYPOINT to a function name or fully-qualified class name that exists in your source code. See [Function entry point](/functions/docs/writing#entry-point) for more information.
    
      - The [`  --trigger-event-filters  `](/sdk/gcloud/reference/functions/deploy#--trigger-event-filters) flags define the event filter which includes trigger type and the entity or path that triggers the events. Set the following attribute values to define your event filter:
        
          - `  type= EVENT_FILTER_TYPE  ` : Firestore supports the following event types:
            
              - `  google.cloud.datastore.entity.v1.created  ` : event is sent when an entity is written for the first time.
              - `  google.cloud.datastore.entity.v1.updated  ` : event is sent when an entity already exists and has any value changed.
              - `  google.cloud.datastore.entity.v1.deleted  ` : event is sent when an entity is deleted.
              - `  google.cloud.datastore.entity.v1.written  ` : event is sent when an entity is created, updated, or deleted.
              - `  google.cloud.datastore.entity.v1.created.withAuthContext  ` : event is sent when a document is written to for the first time and the event includes additional authentication information
              - `  google.cloud.datastore.entity.v1.updated.withAuthContext  ` : event is sent when a document already exists and has any value changed. Includes additional authentication information
              - `  google.cloud.datastore.entity.v1.deleted.withAuthContext  ` : event is sent when a document is deleted. Includes additional authentication information
              - `  google.cloud.datastore.entity.v1.written.withAuthContext  ` : event is sent when a document is created, updated, or deleted and event. Includes additional authentication information
            
            Set EVENT\_FILTER\_TYPE to one of these event types.
        
          - `  database= DATABASE  ` : the Firestore database. For the default database name, set DATABASE to `  (default)  ` .
        
          - `  namespace= NAMESPACE  ` : the database [namespace](/datastore/docs/concepts/multitenancy) . For the default database name, set NAMESPACE to `  (default)  ` . Remove the flag to match any namespace.
            
            **Note:** Set exactly to `  (default)  ` for the default namespace. This is a non-canonical resource name used only for Eventarc. Do not set to `  [default]  ` as shown in the Google Cloud console.
        
          - `  entity= ENTITY_OR_PATH  ` : the database path that triggers events when data is created, updated, or deleted. Accepted values for ENTITY\_OR\_PATH are:
            
              - Equal; for example, `  --trigger-event-filters="entity='users/marie'"  `
              - Path pattern; for example, `  --trigger-event-filters-path-pattern="entity='users/*'"  ` . For more information, see [Understand path patterns](/eventarc/docs/path-patterns) .
        
        You can optionally specify additional [configuration](/functions/docs/configuring) , [networking](/functions/docs/networking/network-settings) , and [security](/functions/docs/securing) options when you deploy a function.
        
        For a complete reference on the deployment command and its flags, see the [`  gcloud functions deploy  `](/sdk/gcloud/reference/functions/deploy) documentation.

### Example deployments

The following examples demonstrate deployments with the Google Cloud CLI.

Deploy a function for a database in the `  us-west2  ` region:

``` text
gcloud functions deploy gcfv2-trigger-datastore-node \
--gen2 \
--region=us-west2 \
--trigger-location=us-west2 \
--runtime=nodejs18 \
--source=gs://example_bucket-1/datastoreEventFunction.zip \
--entry-point=makeUpperCase \
--trigger-event-filters=type=google.cloud.datastore.entity.v1.written \
--trigger-event-filters=database='(default)' \
--trigger-event-filters-path-pattern="entity='messages/{pushId}'"
```

Deploy a function for a database in the `  nam5  ` multi-region:

``` text
gcloud functions deploy gcfv2-trigger-datastore-python \
--gen2 \
--region=us-central1 \
--trigger-location=nam5 \
--runtime=python311 \
--source=gs://example_bucket-1/datastoreEventFunction.zip \
--entry-point=make_upper_case \
--trigger-event-filters=type=google.cloud.datastore.entity.v1.written.withAuthContext \
--trigger-event-filters=database='(default)' \
--trigger-event-filters-path-pattern="entity='messages/{pushId}'"
```

## Limitations

Note the following limitations for Firestore triggers for Cloud Run functions:

  - Cloud Run functions (1st gen) prerequisites an existing "(default)" database in Firestore native mode. It does not support Firestore named databases or Datastore mode. Please use Cloud Run functions (2nd gen) to configure events in such cases.
  - Cross project setup with Cloud Run functions and Firestore trigger is a limitation. To setup Firestore trigger Cloud Run functions must be in the same project.
  - Ordering is not guaranteed. Rapid changes can trigger function invocations in an unexpected order.
  - Events are delivered at least once, but a single event may result in multiple function invocations. Avoid depending on exactly-once mechanics, and write [idempotent functions](https://cloud.google.com/blog/products/serverless/cloud-functions-pro-tips-building-idempotent-functions) .
  - [Firestore in Datastore mode](https://cloud.google.com/firestore/docs/firestore-or-datastore) requires Cloud Run functions (2nd gen). Cloud Run functions (1st gen) does not support Datastore mode.
  - A trigger is associated with a single database. You cannot create a trigger that matches multiple databases.
  - Deleting a database does not automatically delete any triggers for that database. The trigger stops delivering events but continues to exist until you [delete the trigger](https://cloud.google.com/eventarc/docs/managing-triggers#trigger-delete) .
  - If a matched event exceeds the [maximum request size](https://cloud.google.com/functions/quotas#resource_limits) , the event might not be delivered to Cloud Run functions (1st gen).
      - Events not delivered because of request size are logged in [platform logs](https://cloud.google.com/logging/docs/api/platform-logs) and count towards the log usage for the project.
      - You can find these logs in the Logs Explorer with the message "Event cannot deliver to Cloud function due to size exceeding the limit for 1st gen..." of `  error  ` severity. You can find the function name under the `  functionName  ` field. If the `  receiveTimestamp  ` field is still within an hour from now, you can infer the actual event content by reading the document in question with a snapshot before and after the timestamp.
      - To avoid such cadence, you can:
          - Migrate and upgrade to Cloud Run functions (2nd gen)
          - Downsize the document
          - Delete the Cloud Run functions in question
      - You can turn off the logging itself using [exclusions](https://cloud.google.com/logging/docs/routing/overview#exclusions) but note that the offending events will still not be delivered.

### Eventarc and Firestore in Datastore mode locations

Eventarc does not support multi-regions for Firestore event triggers, but you can still create triggers for Firestore databases in multi-region locations. Eventarc maps Firestore multi-region locations to the following Eventarc regions:

<table>
<thead>
<tr class="header">
<th>Firestore multi-region</th>
<th>Eventarc region</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       nam5      </code></td>
<td><code dir="ltr" translate="no">       us-central1      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       eur3      </code></td>
<td><code dir="ltr" translate="no">       europe-west4      </code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn about [event-driven architectures](/eventarc/docs/event-driven-architectures) .
  - See [code samples for Datastore mode](/datastore/docs/samples) .
