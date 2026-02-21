# Write data to the Firestore database

This page describes the second stage of the [migration process](/firestore/mongodb-compatibility/docs/migrate-data) where you set up a Dataflow pipeline and begin a concurrent data move from the Cloud Storage bucket into your destination Firestore with MongoDB compatibility database. This operation will run concurrently with the Datastream stream.

## Start the Dataflow pipeline

The following command starts a new, uniquely named, Dataflow pipeline.

**Note:** The start timestamp of the job is captured in the `  DATAFLOW_START_TIME  ` environment variable. Make a note of this timestamp: it will appear as part of the job name in the Dataflow console. Also note that the Dataflow template does not support wildcard expressions for Cloud Storage paths.

The following formats are acceptable:

  - `  inputFilePattern=gs://bucket-name/migration/attempt_1/  `
  - `  inputFilePattern=gs://bucket-name/migration/  `
  - `  inputFilePattern=gs://bucket-name/  `

Not supported:

  - `  inputFilePattern=gs://bucket-name/**/*  `

<!-- end list -->

``` text
DATAFLOW_START_TIME="$(date +'%Y%m%d%H%M%S')"

gcloud dataflow flex-template run "dataflow-mongodb-to-firestore-$DATAFLOW_START_TIME" \
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
useShadowTablesForBackfill=true,\
runMode=regular,\
directoryWatchDurationInMinutes=20,\
streamName=$DATASTREAM_NAME,\
stagingLocation=$STAGING_LOCATION,\
autoscalingAlgorithm=THROUGHPUT_BASED,\
maxNumWorkers=$MAX_WORKERS,\
workerMachineType=$WORKER_TYPE
```

**Note:** To ensure correct sequencing of document updates and deletions, the Dataflow job creates shadow collections in your destination database. For example, if your source database contains a collection named `  users  ` , the destination Firestore database will have both `  shadow_users  ` and `  users  ` collections after the migration completes. You can delete the contents of the shadow collection after migrating. The naming prefix for the shadow collection is controlled by the `  shadowCollectionPrefix  ` Dataflow template parameter.

For more information about monitoring the Dataflow pipeline, see [Troubleshooting](/firestore/mongodb-compatibility/docs/migrate-troubleshooting) .

## What's next

Proceed to [Migrate traffic to Firestore](/firestore/mongodb-compatibility/docs/migrate-traffic) .
