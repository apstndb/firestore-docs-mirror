# Import from the source Mongo database

This page describes the first stage of the [migration process](/firestore/mongodb-compatibility/docs/migrate-data) where you use a Datastream stream to capture the contents of your MongoDB-compatible source database and transfer them into a Cloud Storage bucket.

## Create YAML configuration files for the stream

In addition to usual command-line flags, creating a stream requires two configuration files in the YAML format:

  - The `  mongo_source_config.yaml  ` file configures the selection of specific resources for migration, such as the database name. Mongo connectivity parameters such as the hostname, username, and password are all properties of the connection profile. However, the database (and any specific collections within that database) are a property of the stream.

  - The `  gcs_dst_config.yaml  ` file configures the data placement within Cloud Storage. The Cloud Storage bucket and the root path within the bucket are properties of the connection profile. However, the data format and the data placement within the Cloud Storage bucket structure are a property of the stream.

The following command examples create these files and populate them with values from the [environment variables](/firestore/mongodb-compatibility/docs/migrate-configure-env-vars) that you've set earlier. As an alternative, you can create these files in any text editor and substitute the values manually.

``` text
echo "$(cat <<EOF
includeObjects:
  databases:
  - database: ${MONGODB_DATABASE_NAME}
EOF
)" > mongo_source_config.yaml

echo "$(cat <<EOF
path: "/${GCS_BUCKET_SUB_PATH}"
avroFileFormat: {}
EOF
)" > gcs_dst_config.yaml
```

The previous example configures the full contents of $MONGODB\_DATABASE\_NAME for migration. It is also possible to limit the migration to specific collections within the database. For example, to migrate only the collections `  users  ` and `  chats  ` use the following:

``` text
includeObjects:
  databases:
  - database: ${MONGODB_DATABASE_NAME}
    collections:
      - collection: users
      - collection: chats
```

## Create a Datastream stream

Next, create a stream that connects the source and the destination:

``` text
gcloud datastream streams create "$DATASTREAM_NAME" \
--display-name="$DATASTREAM_NAME" \
--location="$LOCATION" \
--source="$SRC_CONNECTION_PROFILE_NAME" \
--destination="$DST_CONNECTION_PROFILE_NAME" \
--mongodb-source-config=./mongo_source_config.yaml \
--gcs-destination-config=./gcs_dst_config.yaml \
--backfill-all
```

For more information about monitoring the Datastream stream creation, see [Troubleshooting](/firestore/mongodb-compatibility/docs/migrate-troubleshooting) .

## Activate the Datastream stream

Finally, activate the new stream.

As the stream begins pulling data and streaming changes from the Mongo source, you can observe new directories and files created in the Cloud Storage bucket, under the path configured in the connection profile and the stream.

**Important:** At this point your MongoDB-compatible source database is **still the source of truth** for your application workloads. The database must continue to receive queries and updates until the migration [reaches a specific milestone](/firestore/mongodb-compatibility/docs/migrate-traffic) described later.

To activate the stream, run the following command:

``` text
gcloud datastream streams update "$DATASTREAM_NAME" \
--location="$LOCATION" \
--state=RUNNING \
--update-mask=state
```

## What's next

Proceed to [Write data into the destination database](/firestore/mongodb-compatibility/docs/migrate-write-to-destination) .
