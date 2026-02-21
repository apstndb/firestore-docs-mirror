# Migrate traffic to Firestore

This page describes the last stage of the [migration process](/firestore/mongodb-compatibility/docs/migrate-data) where you monitor the migration and determine when to switch traffic to minimize the downtime of your application.

**Caution:** There are several critical steps in the migration process that must be orchestrated correctly **to ensure no data loss and minimize application downtime** .

These steps are:

1.  Determine whether any errors were encountered during the data transfer. Note the current [known limitations](/firestore/mongodb-compatibility/docs/migrate-data#limitations) for data types and document sizes.
2.  Determine when it is appropriate to shut down write traffic to the source database.
3.  Determine when all the data (including recent change events) was replicated to the Firestore with MongoDB compatibility database. At this point, it is safe to redirect read traffic to the new destination.
4.  After all your application workloads are consistently reading data only from Firestore, it is then safe to enable and direct the write traffic to Firestore with MongoDB compatibility database.

## Check for migration completion milestones

The instructions in this section require access to Dataflow within the Google Cloud console.

In the Google Cloud console, go to the **Dataflow** page:

### Source database is receiving all read and write traffic

After initiating both the Datastream and the Dataflow pipelines, your source database should continue to receive both read and write traffic. You can use the following milestones to determine when the migration can proceed to the next step:

  - The **Transactional write events** step of the Dataflow pipeline is no longer processing a backlog of the data and the throughput drops to a low steady state that matches with your source database's active traffic:

  - The data freshness in the Datastream **Monitoring** tab is at a minimum and is very close behind the ongoing traffic in your source database:

After the data transfer reaches this steady state, advance to the next step.

### Shut down write traffic to the source database

**Caution:** This part of the procedure will require a short period of write unavailability.

After you've determined that the Datastream stream have completed the bulk backfill, and the Dataflow template is doing transactional write at a steady speed only for live changes of the source database, you can begin the cutover process. This process will require a small amount of downtime to allow for all remaining traffic to be replicated to the target Firestore with MongoDB compatibility database.

1.  Stop all write traffic to the MongoDB-compatible source database. Depending on your application requirements and functionality, you might want to continue to allow read traffic to the source database.

2.  Monitor the Datastream throughput and logs, and the Dataflow throughput, data lag, and logs to ensure the last of the write traffic was processed.
    
    **Caution:** Wait at least 20 minutes to **ensure the last of the traffic is fetched from the source database** .

3.  [Inspect the Dead Letter Queue](/firestore/mongodb-compatibility/docs/migrate-troubleshooting#non-retryable-errors) . Determine if any documents couldn't be written to the destination database during the migration, and make a decision about whether to continue with the migration.

### Migrate read traffic to Firestore

After all pending change stream events are replicated to Firestore, both databases contain the exact same data. You can now transfer the read traffic, and then the write traffic.

If you chose to allow read traffic to the MongoDB-compatible source database in the previous step:

1.  Transfer the read traffic.
2.  Ensure that all services that were originally connected to the MongoDB-compatible source database were updated to perform reads from the Firestore with MongoDB compatibility database.

### Migrate write traffic to Firestore

After the previous step is completed, it is safe to redirect your application's write traffic directly to Firestore.

## Stop the migration pipeline

The migration is now complete. Your Datastream stream and the Dataflow job can now be stopped.

Pause the Datastream stream:

``` text
gcloud datastream streams update "$DATASTREAM_NAME" \
--location="$LOCATION" \
--state=PAUSED \
--update-mask=state
```

**Note:** If required, you can [delete the stream](/datastream/docs/delete-a-stream) after the migration completes.

To shut down the Dataflow pipeline:

1.  Listing all current jobs:
    
    ``` text
    gcloud dataflow jobs list --region="$LOCATION"
    ```
    
    The output will produce a list of Dataflow jobs.

2.  In the list of jobs, find the `  NAME  ` value that has the timestamp that you've specified in the `  DATAFLOW_START_TIME  ` [environment variable](/firestore/mongodb-compatibility/docs/migrate-configure-env-vars) .
    
    Format: `  dataflow-mongodb-to-firestore- DATAFLOW_START_TIME  ` . Example: `  dataflow-mongodb-to-firestore-20250514173638  ` .

3.  Obtain the corresponding `  JOB_ID  ` . Example: `  2025-05-14_17_36_39-10772223470853954680  ` .

4.  Run the drain command for this job ID:
    
    ``` text
    gcloud dataflow jobs drain \
    JOB_ID \
    --region="$LOCATION"
    ```
    
    Example:
    
    ``` text
    gcloud dataflow jobs drain \
    2025-05-14_17_36_39-10772223470853954680 \
    --region="$LOCATION"
    ```

## What's next

For troubleshooting tips, check [Migration troubleshooting](/firestore/mongodb-compatibility/docs/migrate-troubleshooting) .
