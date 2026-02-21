# Create connection profiles

This page describes the preparation part of the [migration process](/firestore/mongodb-compatibility/docs/migrate-data) where you create Datastream connection profiles that will be used later from importing data from the MongoDB-compatible source database to the Cloud Storage bucket.

At this stage, you do the following:

1.  Create a Cloud Storage connection profile for the Cloud Storage bucket that you've created earlier.
2.  Create a connection profile for the MongoDB-compatible source database.

## Sign in to gcloud CLI

The migration procedure described in the subsequent sections uses the gcloud CLI to configure and actuate the migration steps. Begin by logging into Google Cloud and selecting the project that will host the migration pipeline.

``` text
gcloud auth login
gcloud config set project "$PROJECT_ID"
```

## Create a connection profile for the source database

### MongoDB on Compute Engine

Run the following command to create a Datastream connection profile to the MongoDB database hosted on Compute Engine.

Omit the `  --mongodb-replica-set  ` flag from the following command when connecting to a sharded cluster.

``` text
gcloud datastream connection-profiles create "$SRC_CONNECTION_PROFILE_NAME" \
--display-name="$SRC_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--mongodb-username="$MONGODB_USERNAME" \
--mongodb-password="$MONGODB_PASSWORD" \
--mongodb-host-addresses="$MONGODB_IP_ADDRESS" \
--mongodb-replica-set="$REPLICA_SET" \
--private-connection="$PRIVATE_CONNECTION_NAME" \
--mongodb-standard-connection-format \
--type=mongodb \
--mongodb-direct-connection
```

### MongoDB over SSH

This example assumes you have already [configured SSH connectivity](/firestore/mongodb-compatibility/docs/migrate-configure-env-vars#mongodb-over-ssh) to your private network, either directly to the machine hosting the MongoDB compatible server, or through a [Bastion](https://cloud.google.com/solutions/connecting-securely#bastion) host.

Run the following command to create a Datastream connection profile to the MongoDB database hosted on Compute Engine.

Omit the `  --mongodb-replica-set  ` flag from the following command when connecting to a sharded cluster.

If you want to connect with an SSH password, pass the `  --forward-ssh-password  ` flag instead of the `  --forward-ssh-private-key  ` flag.

``` text
gcloud datastream connection-profiles create "$SRC_CONNECTION_PROFILE_NAME" \
--display-name="$SRC_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--mongodb-username="$MONGODB_USERNAME" \
--mongodb-password="$MONGODB_PASSWORD" \
--mongodb-host-addresses="$MONGODB_IP_ADDRESS" \
--mongodb-replica-set="$REPLICA_SET" \
--forward-ssh-hostname="$BASTION_IP_ADDRESS" \
--forward-ssh-port="$BASTION_SSH_PORT" \
--forward-ssh-username="$BASTION_SSH_USERNAME" \
--forward-ssh-private-key="$BASTION_SSH_PRIVATE_KEY" \
--mongodb-standard-connection-format \
--type=mongodb \
--mongodb-direct-connection
```

### Amazon DocumentDB

This example assumes you have obtained the parameters and certificates required for [Amazon DocumentDB connectivity](/firestore/mongodb-compatibility/docs/migrate-configure-env-vars#amazon-documentdb) .

Prior to creating a connection profile, explicitly enable change streams in the Amazon DocumentDB database. See the [Amazon DocumentDB Change Streams](https://docs.aws.amazon.com/documentdb/latest/developerguide/change_streams.html) guide for instructions on enabling this feature.

Run the following command to create a Datastream connection profile to your DocumentDB database:

``` text
gcloud datastream connection-profiles create "$SRC_CONNECTION_PROFILE_NAME" \
--display-name="$SRC_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--mongodb-username="$MONGODB_USERNAME" \
--mongodb-password="$MONGODB_PASSWORD" \
--mongodb-host-addresses="$MONGODB_HOST_ADDRESS" \
--mongodb-replica-set="$REPLICA_SET" \
--forward-ssh-hostname="$BASTION_IP_ADDRESS" \
--forward-ssh-port="$BASTION_SSH_PORT" \
--forward-ssh-username="$BASTION_SSH_USERNAME" \
--forward-ssh-private-key="$BASTION_SSH_PRIVATE_KEY" \
--mongodb-ca-certificate="$DOCUMENT_DB_CA_CERTIFICATE" \
--mongodb-tls \
--mongodb-standard-connection-format \
--type=mongodb \
--mongodb-direct-connection
```

### Azure Cosmos DB

Explicitly enable change streams for MongoDB in Azure Cosmos DB's API to enable initiating Datastream streams.

This step requires [installing Azure CLI](/firestore/mongodb-compatibility/docs/migrate-configure-resources#install-source-specific-tools) .

``` text
az resource patch --ids "/subscriptions/subscription_id/resourceGroups/resource_group_name/providers/Microsoft.DocumentDB/mongoClusters/vCore_cluster_name" \
--api-version 2024-10-01-preview \
--properties "{\"previewFeatures\": [ \"ChangeStreams\"]}"
```

Replace subscription\_id , resource\_group\_name , and vCore\_cluster\_name with values corresponding to your Azure Cosmos DB deployment.

Run the following command to create a Datastream connection profile to the source Azure Cosmos DB.

This example assumes that the source is accessible through a public DNS or IP address that can be expressed in the [MongoDB SRV connection format](https://www.mongodb.com/docs/manual/reference/connection-string/) . The instructions also assume the Azure Cosmos DB server uses a combination of a username and password for authentication.

``` text
gcloud datastream connection-profiles create "$SRC_CONNECTION_PROFILE_NAME" \
--display-name="$SRC_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--mongodb-username="$MONGODB_USERNAME" \
--mongodb-password="$MONGODB_PASSWORD" \
--mongodb-host-addresses="$MONGODB_HOST_ADDRESS" \
--mongodb-srv-connection-format \
--type=mongodb \
--static-ip-connectivity \
--labels=skip_all_validations=true
```

### MongoDB Atlas

Run the following command to create a Datastream connection profile to the source MongoDB Atlas database.

This example assumes that the source is accessible through a public DNS or IP address that can be expressed in the [MongoDB SRV connection format](https://www.mongodb.com/docs/manual/reference/connection-string/) . The instructions also assume that MongoDB Atlas server uses a combination of a username and password for authentication.

``` text
gcloud datastream connection-profiles create "$SRC_CONNECTION_PROFILE_NAME" \
--display-name="$SRC_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--mongodb-username="$MONGODB_USERNAME" \
--mongodb-password="$MONGODB_PASSWORD" \
--mongodb-host-addresses="$MONGODB_HOST_ADDRESS" \
--mongodb-srv-connection-format \
--type=mongodb \
--static-ip-connectivity
```

For more information about monitoring the connection profile creation, see [Troubleshooting](/firestore/mongodb-compatibility/docs/migrate-troubleshooting) .

## Create a Cloud Storage connection profile

Configure the Datastream connection profile for the Cloud Storage destination, which is the bucket that you've created earlier.

``` text
gcloud datastream connection-profiles create "$DST_CONNECTION_PROFILE_NAME" \
--display-name="$DST_CONNECTION_PROFILE_NAME" \
--location="$LOCATION" \
--type=google-cloud-storage \
--bucket="$GCS_BUCKET_NAME" \
--root-path="/$GCS_BUCKET_ROOT_PATH"
```

For more information about monitoring the connection profile creation, see [Troubleshooting](/firestore/mongodb-compatibility/docs/migrate-troubleshooting) .

## What's next

Proceed to [Import from the source database](/firestore/mongodb-compatibility/docs/migrate-import-from-source) .
