# Configure environment variables

This page describes the preparation part of the [migration process](/firestore/mongodb-compatibility/docs/migrate-data) where you configure environment variables in your local environment. From this environment, you will later execute the commands that configure and actuate the migration process. Each of these commands will use one or more environment variables that you set at this stage.

At this stage, you do the following:

1.  Set environment variables that are common to all supported MongoDB-compatible sources.

2.  Set environment variables that are specific to the type of the MongoDB-compatible source database and to how it is deployed.

### Set common environment variables

The following template helps to set up environment variables that are common to all supported MongoDB-compatible sources. You will add extra variables that are specific to your MongoDB source later.

The template configures the following set of environment variables:

  - **General parameters** that are applicable to the entire migration procedure.
  - **Datastream connection parameters** that are used to create and manage [Datastream connection profiles](/datastream/docs/create-connection-profiles) .
  - **Datastream data placement parameters** for managing data placement in the Cloud Storage bucket during the migration.
  - **Dataflow template parameters** for managing the pipeline that will copy data from the Cloud Storage bucket into your Firestore with MongoDB compatibility database.
  - **Additional Dataflow template parameters** these parameters are derived from other parameters that you specify and you don't need to set them.
  - **Firestore connection parameters** for establishing a connection to your destination Firestore with MongoDB compatibility database.

Set the following variables before proceeding with other commands in this guide:

``` text
# General parameters
PROJECT_ID="PROJECT_ID"
LOCATION="LOCATION"

# Datastream connection parameters
SRC_CONNECTION_PROFILE_NAME="SRC_CONNECTION_PROFILE_NAME"
DST_CONNECTION_PROFILE_NAME="DST_CONNECTION_PROFILE_NAME"
DATASTREAM_NAME="DATASTREAM_NAME"

# Datastream data placement parameters
GCS_BUCKET_NAME="GCS_BUCKET_NAME"
GCS_BUCKET_ROOT_PATH="GCS_BUCKET_ROOT_PATH"
GCS_BUCKET_SUB_PATH="GCS_BUCKET_SUB_PATH"

# Dataflow template parameters
GCS_BUCKET_TEMPLATE_PATH="GCS_BUCKET_TEMPLATE_PATH"
NUM_WORKERS=NUM_WORKERS
MAX_WORKERS=MAX_WORKERS
WORKER_TYPE="WORKER_TYPE"

# Additional Dataflow template parameters: these are initialized
# from parameters above and don't require further customization
INPUT_FILE_LOCATION="gs://${GCS_BUCKET_NAME}/${GCS_BUCKET_ROOT_PATH}/${GCS_BUCKET_SUB_PATH}/"
TEMP_OUTPUT_LOCATION="gs://${GCS_BUCKET_NAME}/${GCS_BUCKET_ROOT_PATH}/tmp"
DLQ_LOCATION="gs://${GCS_BUCKET_NAME}/${GCS_BUCKET_ROOT_PATH}/dql"
STAGING_LOCATION="gs://${GCS_BUCKET_NAME}/${GCS_BUCKET_ROOT_PATH}/staging"

# Firestore connection parameters
FIRESTORE_CONNECTION_URI="FIRESTORE_CONNECTION_URI"
FIRESTORE_DATABASE_NAME="FIRESTORE_DATABASE_NAME"
```

Replace the following:

  - General parameters:
    
      - PROJECT\_ID : a [Project ID](/resource-manager/docs/creating-managing-projects) of the Google Cloud project where the migration pipeline will run. Example: `  example-project  ` .
        
        It's possible to use a destination Firestore with MongoDB compatibility database that is located in another project. However, this guide assumes that all relevant resources are located in the same project.
    
      - LOCATION : [a region](/firestore/mongodb-compatibility/docs/locations) where the migration pipeline will run. Examples: `  nam5  ` , `  us-central1  ` .
        
        We recommed to use the same region as the destination Firestore with MongoDB compatibility database.

  - Datastream connection parameters:
    
      - SRC\_CONNECTION\_PROFILE\_NAME : a human-readable name for the [Datastream connection profile](/datastream/docs/create-connection-profiles) of the MongoDB-compatible source database. Example: `  source-mongo-profile  ` .
        
        You create a connection profile with this name later.
    
      - DST\_CONNECTION\_PROFILE\_NAME : a human-readable name for the [Datastream connection profile](/datastream/docs/create-connection-profiles) for the destination Cloud Storage bucket. Example: `  destination-gcs-profile  ` .
        
        You create a destination connection profile with this name later.
    
      - DATASTREAM\_NAME : A human-readable name of a [Datastream stream](/datastream/docs/create-a-stream) that will transfer the data from the MongoDB-compatible source database into Cloud Storage. Example: `  mongo-to-gcs-stream  ` .
        
        You create this stream later.

  - Datastream data placement parameters:
    
    **Note:** Wildcards are not supported in the Cloud Storage paths.
    
      - GCS\_BUCKET\_NAME : the name of the Cloud Storage bucket that you've [created earlier](/firestore/mongodb-compatibility/docs/migrate-configure-resources#create-bucket) . Example: `  mongo-migration-bucket  ` .
        
        This value is used to create a destination connection profile later.
    
      - GCS\_BUCKET\_ROOT\_PATH : The name of the top-level directory in the Cloud Storage bucket for placing the intermediate data during the migration. Example: `  mongo-migration-root  ` .
        
        This value is used to create a destination connection profile later.
    
      - GCS\_BUCKET\_TEMPLATE\_PATH : A sub-path in the GCS\_BUCKET\_ROOT\_PATH directory for a given Datastream instance.
        
        The same destination connection profile can be used for multiple exports to Cloud Storage. However **you must designate a unique sub-path** for each migration. Example: `  mongo-migration-data-0  ` .
        
        This value is used to create a stream later.

  - Dataflow template parameters:
    
      - GCS\_BUCKET\_TEMPLATE\_PATH : A sub-path in the GCS\_BUCKET\_ROOT\_PATH directory where a [Dataflow template](/dataflow/docs/concepts/dataflow-templates) will be staged. Example: `  mongo-migration-template-path  ` .
    
      - NUM\_WORKERS : The starting number of workers to run the Dataflow template with. Example: `  2  ` .
    
      - MAX\_WORKERS : The maximum number of workers to run the Dataflow template with. Example: `  8  ` .
    
      - WORKER\_TYPE : The Compute Engine instance type to use for the Dataflow job. The recommended machine type is [`  e2-highmem-8  `](/compute/docs/general-purpose-machines#e2-high-mem) .

  - Firestore connection parameters:
    
      - FIRESTORE\_DATABASE\_NAME : The name of the Firestore with MongoDB compatibility database where you migrate the data. Example: `  firestore-database-name  ` .
    
      - FIRESTORE\_CONNECTION\_URI : The [connection URI string](/firestore/mongodb-compatibility/docs/create-and-query-database#create-database) for the Firestore with MongoDB compatibility database.
        
        Example: `  mongodb://USERNAME:PASSWORD@CONNECTION_STRING:443/ FIRESTORE_DATABASE_NAME ?loadBalanced=true&authMechanism=SCRAM-SHA-256&tls=true&retryWrites=false  ` .

### Set environment variables specific to the source database type

The following templates help to set up environment variables that are specific to the type of the MongoDB-compatible source database and to how it is deployed.

### MongoDB on Compute Engine

The following variables are specific for MongoDB source databases located in a self-managed cluster (Compute Engine). Set them before proceeding with other commands in this guide:

``` text
# Google Compute Engine VM MongoDB Parameters
MONGODB_USERNAME="MONGODB_USERNAME"
MONGODB_PASSWORD="MONGODB_PASSWORD"
MONGODB_IP_ADDRESS="MONGODB_IP_ADDRESS"
REPLICA_SET="REPLICA_SET"
MONGODB_DATABASE_NAME="MONGODB_DATABASE_NAME"
PRIVATE_CONNECTION_NAME="PRIVATE_CONNECTION_NAME"
```

Replace the following:

  - MONGODB\_USERNAME : The username of the MongoDB-compatible source database. Example: `  mongouser  ` .

  - MONGODB\_PASSWORD : The password of the MongoDB-compatible source database. Example: `  mongopassword  ` .

  - MONGODB\_IP\_ADDRESS : specify the internal IP address, along with the port number, of the VM that hosts your MongoDB server. Example: `  10.0.0.1:27017  ` .
    
      - For deployments that are not sharded, but configured with [replica sets](https://www.mongodb.com/docs/manual/replication) , the IP address of any replica in the set is valid. However, we recommend to use one of the secondary replicas.
    
      - For [sharded clusters](https://www.mongodb.com/docs/manual/sharding) , specify the address of one of your *mongos* servers.

  - (Only for clusters with replica sets that aren't sharded) REPLICA\_SET : Specify the name of the replica set that must be used for the migration process. Example: `  rs0  ` .

  - MONGODB\_DATABASE\_NAME : The name of the MongoDB-compatible source database. Example: `  source_db  ` .

  - PRIVATE\_CONNECTION\_NAME : The ID of the private connectivity configuration that [you've created earlier](/firestore/mongodb-compatibility/docs/migrate-configure-resources#source-specific-configuration) . Example: `  pc_name  ` .

### MongoDB over SSH

If you are managing a private MongoDB deployment outside of Compute Engine, Datastream supports connecting to your source database over a forward-SSH tunnel. For more information, see [SSH tunnels](/datastream/docs/network-connectivity-options#sshtunnel) .

The following variables are specific for connecting to MongoDB source databases over a forward-SSH tunnel. Set them before proceeding with other commands in this guide:

``` text
# MongoDB over an SSH Tunnel Parameters
MONGODB_USERNAME="MONGODB_USERNAME"
MONGODB_PASSWORD="MONGODB_PASSWORD"
MONGODB_IP_ADDRESS="MONGODB_IP_ADDRESS"
REPLICA_SET="REPLICA_SET"
MONGODB_DATABASE_NAME="MONGODB_DATABASE_NAME"
BASTION_IP_ADDRESS="BASTION_IP_ADDRESS"
BASTION_SSH_PORT="BASTION_SSH_PORT"
BASTION_SSH_USERNAME="BASTION_SSH_USERNAME"
BASTION_SSH_PRIVATE_KEY="BASTION_SSH_PRIVATE_KEY"
```

Replace the following:

  - MONGODB\_USERNAME : The username of the MongoDB-compatible source database. Example: `  mongouser  ` .

  - MONGODB\_PASSWORD : The password of the MongoDB-compatible source database. Example: `  mongopassword  ` .

  - MONGODB\_IP\_ADDRESS : specify the internal IP address, along with the port number, of the VM that hosts your MongoDB server. Example: `  10.0.0.1:27017  ` .
    
      - For deployments that are not sharded, but configured with [replica sets](https://www.mongodb.com/docs/manual/replication) , the IP address of any replica in the set is valid. However, we recommend to use one of the secondary replicas.
    
      - For [sharded clusters](https://www.mongodb.com/docs/manual/sharding) , specify the address of one of your *mongos* servers.

  - (Only for clusters with replica sets that aren't sharded) REPLICA\_SET : Specify the name of the replica set that must be used for the migration process. Example: `  rs0  ` .

  - MONGODB\_DATABASE\_NAME : The name of the MongoDB-compatible source database. Example: `  source_db  ` .

  - BASTION\_IP\_ADDRESS : the address of the host on your network that can accept an SSH connection. This can be the MongoDB server itself, or a designated [Bastion](https://cloud.google.com/solutions/connecting-securely#bastion) host that allows SSH access from a public network, and also provides internal connectivity to the actual MongoDB server. Example: `  30.0.0.1  ` .

  - BASTION\_SSH\_PORT : The SSH port on the host. Example: `  22  ` .

  - BASTION\_SSH\_USERNAME : Username for the ssh connection.

  - BASTION\_SSH\_PRIVATE\_KEY : The full payload of the SSH private key. For example, for an RSA key, this payload would include the `  -----BEGIN RSA PRIVATE KEY-----  ` header and the `  -----END RSA PRIVATE KEY-----  ` footer. Example: `  BASTION_SSH_PRIVATE_KEY=$(cat ~/.ssh/private_key)  `
    
    **Note:** Datastream also accepts an SSH password. This alternative is described in the [Connection Profile](/firestore/mongodb-compatibility/docs/migrate-create-connection-profiles#connection-profile-source) section.

### Amazon DocumentDB

Ensure that you have the private SSH key for the Amazon EC2 instance that will provide the connection to the DocumentDB cluster. Also ensure that you have downloaded the region-specific Certificate Bundle as described in the [Resource Configuration](/firestore/mongodb-compatibility/docs/migrate-configure-resources#source-specific-configuration) section, and extracted and validated a specific certificate.

The following variables are specific for connecting to DocumentDB source databases over a forward-SSH tunnel. Set them before proceeding with other commands in this guide:

``` text
# DocumentDB over an EC2 SSH Tunnel Parameters
MONGODB_USERNAME="MONGODB_USERNAME"
MONGODB_PASSWORD="MONGODB_PASSWORD"
MONGODB_HOST_ADDRESS="MONGODB_HOST_ADDRESS"
REPLICA_SET="REPLICA_SET"
MONGODB_DATABASE_NAME="MONGODB_DATABASE_NAME"
BASTION_IP_ADDRESS="BASTION_IP_ADDRESS"
BASTION_SSH_PORT="BASTION_SSH_PORT"
BASTION_SSH_USERNAME="BASTION_SSH_USERNAME"
BASTION_SSH_PRIVATE_KEY="BASTION_SSH_PRIVATE_KEY"
DOCUMENT_DB_CA_CERTIFICATE="DOCUMENT_DB_CA_CERTIFICATE"
```

Replace the following:

  - MONGODB\_USERNAME : The username of the DocumentDB source database. Example: `  mongouser  ` .

  - MONGODB\_PASSWORD : The password of the DocumentDB source database. Example: `  mongopassword  ` .

  - MONGODB\_HOST\_ADDRESS : The address of the DocumentDB cluster. Example: `  mydocumentdb.cluster-abcd.us-east-2.docdb.amazonaws.com:27017  ` .

  - REPLICA\_SET : Specify the name of the replica set that must be used for the migration process. Example: `  rs0  ` .

  - MONGODB\_DATABASE\_NAME : The name of the DocumentDB source database. Example: `  source_db  ` .

  - BASTION\_IP\_ADDRESS : the external IP address of the EC2 instance that allows SSH access from a public network, and also provides internal connectivity to the DocumentDB cluster within your Amazon VPC. Example: `  30.0.0.1  ` .

  - BASTION\_SSH\_PORT : The SSH port on the host. Example: `  22  ` .

  - BASTION\_SSH\_USERNAME : Username for the ssh connection.

  - BASTION\_SSH\_PRIVATE\_KEY : The full payload of the SSH private key. For example, for an RSA key, this payload would include the `  -----BEGIN RSA PRIVATE KEY-----  ` header and the `  -----END RSA PRIVATE KEY-----  ` footer. Example: `  BASTION_SSH_PRIVATE_KEY=$(cat ~/ec2_bastion_host.pem)  `

  - DOCUMENT\_DB\_CA\_CERTIFICATE : The full payload of the DocumentDB CA Certificate. This payload should include the `  -----BEGIN CERTIFICATE-----  ` header and the `  -----END CERTIFICATE-----  ` footer and must only include a single certificate. Example: `  BASTION_SSH_PRIVATE_KEY=$(cat ~/us-east-1.pem)  `

### Azure Cosmos DB

The following variables are specific for Azure Cosmos DB source databases. Set them before proceeding with other commands in this guide:

``` text
# Azure Cosmos DB Parameters
MONGODB_USERNAME="MONGODB_USERNAME"
MONGODB_PASSWORD="MONGODB_PASSWORD"
MONGODB_HOST_ADDRESS="MONGODB_HOST_ADDRESS"
MONGODB_DATABASE_NAME="MONGODB_DATABASE_NAME"
```

Replace the following:

  - MONGODB\_USERNAME : The username of the MongoDB-compatible source database. Example: `  mongouser  ` .
  - MONGODB\_PASSWORD : The password of the MongoDB-compatible source database. Example: `  mongopassword  ` .
  - MONGODB\_HOST\_ADDRESS : The hostname of the MongoDB-compatible source database. The value must conform to the [MongoDB SRV connection format](https://www.mongodb.com/docs/manual/reference/connection-string) . Example: `  host.cosmos.azure.example.com  ` .
  - MONGODB\_DATABASE\_NAME : The name of the MongoDB-compatible source database. Example: `  source_db  ` .

### MongoDB Atlas

The following variables are specific for MongoDB Atlas source databases. Set them before proceeding with other commands in this guide:

``` text
# MongoDB Atlas Parameters
MONGODB_USERNAME="MONGODB_USERNAME"
MONGODB_PASSWORD="MONGODB_PASSWORD"
MONGODB_HOST_ADDRESS="MONGODB_HOST"
MONGODB_DATABASE_NAME="MONGODB_DATABASE_NAME"
```

Replace the following:

  - MONGODB\_USERNAME : The username of the MongoDB-compatible source database. Example: `  mongouser  ` .
  - MONGODB\_PASSWORD : The password of the MongoDB-compatible source database. Example: `  mongopassword  ` .
  - MONGODB\_HOST\_ADDRESS : The hostname of the MongoDB-compatible source database. The value must conform to the [MongoDB SRV connection format](https://www.mongodb.com/docs/manual/reference/connection-string) . Example: `  host.mongodb.example.com  ` .
  - MONGODB\_DATABASE\_NAME : The name of the MongoDB-compatible source database. Example: `  source_db  ` .

## What's next

Proceed to [Create connection profiles](/firestore/mongodb-compatibility/docs/migrate-create-connection-profiles) .
