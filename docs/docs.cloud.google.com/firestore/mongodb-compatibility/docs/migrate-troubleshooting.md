# Migration troubleshooting

This section provides tips on troubleshooting common issues that can arise when creating and managing Datastream and Dataflow pipelines.

## Troubleshooting a Datastream connection profile

The migration procedure requires you to create two Datastream connection profiles: one for reading data from the source MongoDB-compatible database and another for writing the data into a Cloud Storage bucket.

These steps use the `  gcloud datastream connection-profiles create  ` command. When you create a Datastream connection profile with this command, it returns metadata that is similar to the following example:

``` text
metadata:
  '@type': type.googleapis.com/google.cloud.datastream.v1.OperationMetadata
  apiVersion: v1
  createTime: '2025-05-15T21:49:05.022509533Z'
  requestedCancellation: false
  target: projects/PROJECT_ID/locations/LOCATION/connectionProfiles/SRC_CONNECTION_PROFILE_NAME
  verb: create
name: projects/PROJECT_ID/locations/LOCATION/operations/operation-1747345744961-63533a26d9ee6-b2386fbf-204c28d6
```

You can use the highlighted identifier starting with `  operation-  ` to retrieve the status of the given Datastream operation. For the output example above, the following gcloud CLI command retrieves details about the connection profile creation request:

``` text
gcloud datastream operations describe \
operation-1747345744961-63533a26d9ee6-b2386fbf-204c28d6 \
--location="$LOCATION"
```

You can examine Datastream connection profiles and other Datastream artifacts in Google Cloud console.

In the Google Cloud console, go to the **Datastream** page:

## Troubleshooting a Datastream stream

When you create a Datastream stream with the `  gcloud datastream streams create  ` command, it returns metadata that is similar to the following example:

``` text
metadata:
  '@type': type.googleapis.com/google.cloud.datastream.v1.OperationMetadata
  apiVersion: v1
  createTime: '2025-05-14T19:31:20.209503095Z'
  requestedCancellation: false
  target: projects/PROJECT_ID/locations/LOCATION/streams/DATASTREAM_NAME
  verb: create
  name: projects/PROJECT_ID/locations/LOCATION/operations/operation-1747251080085-6351d97f63eb8-43204f78-35c87474
```

You can use the highlighted identifier starting with `  operation-  ` to retrieve the status of the given Datastream operation. For the output example above, the following gcloud CLI command retrieves details about the stream creation request:

``` text
gcloud datastream operations describe \
operation-1747345744961-63533a26d9ee6-b2386fbf-204c28d6 \
--location="$LOCATION"
```

To look up the status of an existing stream, use:

``` text
gcloud datastream streams describe $DATASTREAM_NAME --location=$LOCATION
```

You can examine Datastream streams and other Datastream artifacts in Google Cloud console.

In the Google Cloud console, go to the **Datastream** page:

## Troubleshooting the Dataflow pipeline

You can monitor the Dataflow pipeline execution in Google Cloud console.

In the Google Cloud console, go to the **Dataflow** page:

### Troubleshooting retryable errors

Retryable errors are transient errors that will eventually succeed. Common retryable errors are:

  - Network or connectivity issues
  - Transaction contention
  - Closed connections due to load balancing

Documents that couldn't be written to the destination because of errors will be stored in the Cloud Storage bucket, in the location specified by the `  deadLetterQueueDirectory  ` parameter of the Dataflow template. Retryable errors will by default be retried up to the number of times specified by the `  dlqMaxRetryCount  ` parameter.

The Dead Letter Queue (DLQ) can be directly inspected from Cloud Storage by navigating to the path specified in the DLQ\_LOCATION [environment variable](/firestore/mongodb-compatibility/docs/migrate-configure-env-vars) . The path will contain a hierarchy of timestamped folders, containing json records of documents and updates that couldn't be written to the Firestore with MongoDB compatibility database.

Assuming that the Dead Letter Queue only contains documents that failed because of retryable errors, you can attempt to drain the queue by running the Dataflow template in a mode that only operates on this queue. To do so, set the `  runMode  ` parameter to `  retryDLQ  ` , as shown in the following example:

``` text
DLQ_START_TIME="$(date +'%Y%m%d%H%M%S')"

gcloud dataflow flex-template run "dataflow-mongodb-to-firestore-$DLQ_START_TIME" \
--template-file-gcs-location gs://dataflow-templates-us-central1/latest/flex/Cloud_Datastream_MongoDB_to_Firestore \
--region $LOCATION \
--num-workers $NUM_WORKERS \
--temp-location $TEMP_OUTPUT_LOCATION \
--additional-user-labels "" \
--parameters inputFilePattern=$INPUT_FILE_LOCATION,\
inputFileFormat=avro,\
fileReadConcurrency=10,\
connectionUri=$FIRESTORE_CONNECTION_URI,\
databaseName=$FIRESTORE_DATABASE_NAME,\
shadowCollectionPrefix=shadow_,\
batchSize=500,\
deadLetterQueueDirectory=$DLQ_LOCATION,\
dlqRetryMinutes=10,\
dlqMaxRetryCount=500,\
processBackfillFirst=false,\
runMode=retryDLQ,\
directoryWatchDurationInMinutes=10,\
streamName=$DATASTREAM_NAME,\
stagingLocation=$STAGING_LOCATION,\
autoscalingAlgorithm=THROUGHPUT_BASED,\
maxNumWorkers=$MAX_WORKERS,\
workerMachineType=$WORKER_TYPE
```

## Troubleshooting non-retryable errors

Common non-retryable errors are:

  - Unsupported BSON types
  - Unsupported BSON types used as `  _id  `
  - Unsupported 0L as `  _id  `
  - Document sizes larger than Firestore's 4MB limit

Non-retryable errors will be stored in the Cloud Storage bucket, in the location specified by the `  deadLetterQueueDirectory  ` parameter of the Dataflow template.

### Examining the Dead Letter Queue (DLQ)

After all processing has stopped, which means that no active traffic is being processed and no errored events are being retried, the errored events are persisted to Cloud Storage.

You can verify that processing has stopped by [inspecting Transactional write events](/firestore/mongodb-compatibility/docs/migrate-traffic#receiving-traffic) and confirming no processing throughput and that no new log entries are being generated.

You can inspect the DLQ directly from Cloud Storage:

1.  Navigate the Cloud Storage location specified in the DLQ\_LOCATION environment variable.

2.  In the tree of nested folders constructed according to the timestamps, expand the folders to see the latest content in the queue. The files could have been sharded and look like the following example:

3.  Inspect each file to view the documents and updates that weren't applied to the destination database. Each message will contain a payload of the original event and the exception that occurred.
    
    There is a very low possibility that there could be retryable errors present, especially if a low value for the `  dlqMaxRetryCount  ` parameter was used, but generally events that end up in the DLQ will be non-retryable for the previously described reasons.

4.  Choose to either abort the migration and resume application traffic to the source database, addressing the Firestore data constraints in the source database and rerunning the entire migration process, or you can address the data problems with each DLQ event and retry the processing of these events.

For each row in each DLQ file you can:

  - Convert the unsupported data types to an alternative data type by editing the document payload. The document payload will be in the canonical extended JSON format. Express the new data type in canonical extended JSON format.

  - Reassign 0L document `  _id  ` to a new Long or to a different data type such as String. Reassigning to a different data type may require application logic changes if the existing code expectations are that the `  _id  ` 's are all Longs.

  - Documents that exceed the Firestore's 4MB limit can be separated into smaller documents or their contents can be compressed. However, this would require changes to the application logic to handle the data.

  - Ignore the event by deleting the row from the DLQ file.

In order to modify the DLQ files, you will have to download the .json file(s) locally, modify the contents, and re-upload back to the same Cloud Storage location, overwriting the original file. If all documents referenced in the file can be safely excluded from the migration, then the entire file can be deleted.

After you've made the modifications to the DLQ files, you can rerun these events through the migration Dataflow template in the `  retryDLQ  ` mode.

The following command starts a new Dataflow pipeline which will only process the items in the Dead Letter Queue:

``` text
DLQ_START_TIME="$(date +'%Y%m%d%H%M%S')"

gcloud dataflow flex-template run "dataflow-mongodb-to-firestore-$DLQ_START_TIME" \
--template-file-gcs-location gs://dataflow-templates-us-central1/latest/flex/Cloud_Datastream_MongoDB_to_Firestore \
--region $LOCATION \
--num-workers $NUM_WORKERS \
--temp-location $TEMP_OUTPUT_LOCATION \
--additional-user-labels "" \
--parameters inputFilePattern=$INPUT_FILE_LOCATION,\
inputFileFormat=avro,\
fileReadConcurrency=10,\
connectionUri=$FIRESTORE_CONNECTION_URI,\
databaseName=$FIRESTORE_DATABASE_NAME,\
shadowCollectionPrefix=shadow_,\
batchSize=500,\
deadLetterQueueDirectory=$DLQ_LOCATION,\
dlqRetryMinutes=10,\
dlqMaxRetryCount=500,\
processBackfillFirst=false,\
runMode=retryDLQ,\
directoryWatchDurationInMinutes=10,\
streamName=$DATASTREAM_NAME,\
stagingLocation=$STAGING_LOCATION,\
autoscalingAlgorithm=THROUGHPUT_BASED,\
maxNumWorkers=$MAX_WORKERS,\
workerMachineType=$WORKER_TYPE
```

## What's next

  - Back to [Migrate to Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/migrate-data) .
