# Use customer-managed encryption keys (CMEK)

This page describes how to perform tasks related to [customer-managed encryption keys (CMEK) for Firestore](/firestore/native/docs/cmek) . For more information about CMEK in general, including when and why to enable it, see the [Cloud KMS documentation](https://cloud.google.com/kms/docs/cmek) .

**Note:** For information about access to this release, see the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA) .

## Prepare your CMEK keys

Before you can create a CMEK-protected Firestore database, you must complete the following steps:

1.  [Request access to the Firestore CMEK feature](#request-cmek-access) .
2.  [Create (or retrieve) a Firestore service agent](#create-service-agent) .
3.  [Create a CMEK key](#create-key) .
4.  [Configure IAM settings for that key](#set-iam) .

Complete these steps for each project that will contain CMEK-protected Firestore databases. If you later create a new CMEK key, you must configure IAM settings for that key.

**Note:** The `  gcloud  ` commands on this page show placeholders for two Google Cloud projects: the project that contains Firestore databases, `  FIRESTORE_PROJECT  ` , and the project that contains your CMEK key(s), `  KMS_PROJECT  ` . However, you can use the same project for your Firestore databases and CMEK keys.

### Request access

Before you create a Firestore service agent, request access to the CMEK feature by filling in [this form](https://docs.google.com/forms/d/e/1FAIpQLSfKs8wJf4IXu1NizvfyU2vT59JDbdPvkehMVZ2ab5l_aDLIIA/viewform?resourcekey=0-O15dlRFvA0JIDmh6VFUEcA) .

### Create a Firestore service agent

Before you create a CMEK key, you must have a Firestore [service agent](https://cloud.google.com/iam/docs/service-agents) , which is a type of Google-managed service account that Firestore uses to access the key.

Run the [services identity create](https://cloud.google.com/sdk/gcloud/reference/beta/services/identity/create) command to create the service agent that Firestore uses to access the CMEK key on your behalf. This command creates the service account if it does not already exist, then displays it.

``` text
gcloud beta services identity create \
    --service=firestore.googleapis.com \
    --project FIRESTORE_PROJECT
```

Replace `  FIRESTORE_PROJECT  ` with the project you plan to use for your Firestore databases.

The command displays the service agent ID, which is formatted like an email address. Record the output email string, because you'll use it in a later step.

``` text
Service identity created:
service-xxx@gcp-sa-firestore.iam.gserviceaccount.com
```

### Create a key

You can use a key created directly in Cloud KMS or an externally managed key that you make available with [Cloud External Key Manager](https://cloud.google.com/kms/docs/ekm) .

The Cloud KMS [key location](https://cloud.google.com/kms/docs/locations) must be the same as the location of the Firestore database that it will be used with.

  - For [regional database locations](/firestore/native/docs/locations#location-r) , use the same location name for key ring, key, and database because the location names have a one-to-one mapping.
    
    For example, if you want to create a CMEK-protected database in `  us-west1  ` , create a key ring and key in `  us-west1  ` .

  - For [multi-region database locations](/firestore/native/docs/locations#location-r) , use the location name of the [KMS multi-region location](https://cloud.google.com/kms/docs/locations) :
    
      - Use the Cloud KMS `  us  ` multi-region location for the Firestore `  nam5  ` multi-region location.
      - Use the Cloud KMS `  europe  ` multi-region location for the Firestore `  eur3  ` multi-region location.

In the Google Cloud project where you want to manage your keys, complete the following:

1.  [Enable the Cloud KMS API](https://console.cloud.google.com/flows/enableapi?apiid=cloudkms.googleapis.com&redirect=https://console.cloud.google.com) .

2.  Create a key ring and a key using one of the following options:
    
      - [Create the key ring and key directly in Cloud KMS](https://cloud.google.com/kms/docs/creating-keys) .
      - Use an externally managed key. [Create the external key](https://cloud.google.com/kms/docs/ekm-internet#create_external_key) and then [create an Cloud EKM key](https://cloud.google.com/kms/docs/ekm-internet#create_ekm_key) to make the key available through Cloud KMS.

### Configure IAM settings for the key

### Console

To grant an Cloud KMS role to your service agent, do the following. You are also able to grant permission at the key or key-ring level if you want lower granularity.

1.  In the Google Cloud console, go to the **IAM** page.

2.  Click **Add** .

3.  Enter the email-formatted ID for your Firestore service agent.

4.  Select the **Cloud KMS CryptoKey Encrypter/Decrypter** role.

5.  Click **Save** .

### gcloud

Grant the `  cloudkms.cryptoKeyEncrypterDecrypter  ` role to your service agent:

``` text
gcloud kms keys add-iam-policy-binding KMS_KEY \
--keyring KMS_KEYRING\
--location KMS_LOCATION \
--member serviceAccount:SERVICE_AGENT_EMAIL \
--role roles/cloudkms.cryptoKeyEncrypterDecrypter \
--project KMS_PROJECT
```

Replace the following:

  - `  KMS_KEY  ` with the name that you assigned to the key
  - `  KMS_KEYRING  ` with the KMS key ring that contains the key
  - `  KMS_LOCATION  ` with the region that contains the key ring
  - `  SERVICE_AGENT_EMAIL  ` with the email-formatted identifier for the service agent that you are granting access to
  - `  KMS_PROJECT  ` with the project that contains the key

The terminal should display a response similar to the following:

``` text
Updated IAM policy for key KMS_KEY.
bindings:
- members:
- serviceAccount:
service-{project-number}@gcp-sa-firestore.iam.gserviceaccount.com
role: roles/cloudkms.cryptoKeyEncrypterDecrypter
```

## Create a CMEK-enabled database

After your CMEK keys are created and configured, you can create a CMEK-protected database. Existing Firestore databases that are protected by Google default encryption can't be converted to use CMEK.

You can choose an encryption type and key only when you create a CMEK-enabled database.

### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click **Create Database** .

3.  Select your database mode. Click **Continue** .

4.  On the **Configure your database** page, enter a database ID.

5.  Select a location.

6.  Click **Show Encryption Options** , and then select **Cloud KMS key** .

7.  Select or enter the resource name for the CMEK key that you want to use for the database.
    
    **Note:** You can't add or change the CMEK key later.

8.  The list of keys is limited to the current Google Cloud project and the database location that you selected. To use a key from a different Google Cloud project, click **Switch Project** or **Enter Key Manually** .

9.  If you are prompted to grant key permission to the Firestore service account, click **Grant** . To create a CMEK database, your Firestore service account must be granted the `  cloudkms.cryptoKeyEncrypterDecrypter  ` role.

10. Select security rules for mobile and web clients.

11. Click **Create Database** .

Once the database is created, you can verify that the database is CMEK-enabled by viewing **Database details** :

  - If your database is protected by CMEK, the **Encryption type** field shows as **Customer-managed** and the **Encryption key** field lists the corresponding Cloud KMS and the key version that is used to protect this database.
  - If your database is not protected by CMEK, the **Encryption type** field shows as **Google-managed** .

### gcloud

Before you create a CMEK-enabled database with Google Cloud CLI, install the latest version and authorize the gcloud CLI. For more information, see [Install the gcloud CLI](https://cloud.google.com/sdk/docs/install) .

``` text
gcloud firestore databases create --location=FIRESTORE_DATABASE_LOCATION \
      --database=DATABASE_ID \
      --kms-key-name=KMS_KEY_NAME \
      --project=FIRESTORE_PROJECT
```

Replace the following:

  - `  FIRESTORE_DATABASE_LOCATION  ` with the Firestore location for the database

  - `  DATABASE_ID  ` with an ID for the database

  - `  KMS_KEY_NAME  ` with the name you assigned to the key. Use the full resource name for the key in the following format:
    
    `  projects/ KMS_PROJECT /locations/ KMS_LOCATION /keyRings/ KMS_KEYRING_ID /cryptoKeys/ KMS_KEY_ID  `

  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database

### REST API

HTTP request:

POST https://firestore.googleapis.com/v1/projects/{FIRESTORE\_PROJECT}/databases

In the request body configure CMEK in the `  cmek_config.kms_key_name  ` field.

Set to the full resource ID of a Cloud KMS key. Only a key in the same location as this database is allowed.

This value should be the Cloud KMS key resource ID in the format of `  projects/{KMS_PROJECT}/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}  `

For more information about other fields, see the [`  database create  ` page](/firestore/native/docs/reference/rest/v1/projects.databases/create) .

Example request:

``` text
curl -X POST 'https://firestore.googleapis.com/v1/projects/FIRESTORE_PROJECT/databases?databaseId={DATABASE_ID}' \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-type: application/json" \
-d '{
  "type":"FIRESTORE_NATIVE",
  "locationId":"{FIRESTORE_DATABASE_LOCATION}",
  "cmekConfig": {
    "kmsKeyName":"projects/KMS_PROJECT/locations/KMS_LOCATION/keyRings/KMS_KEYRING_ID/cryptoKeys/KMS_KEY_ID"
  }
}'
```

### Firebase CLI

To create a CMEK-enabled database, use the **KMS Key Name** field. If you don't specify the `  --kms-key-name  ` parameter, Firestore creates a non-CMEK database by default.

``` text
firebase firestore:databases:create DATABASE_ID
--location LOCATION
--kms-key-name projects/KMS_PROJECT/locations/KMS_LOCATION/keyRings/KMS_KEYRING_ID/cryptoKeys/KMS_KEY_ID
--project FIRESTORE_PROJECT
```

Replace the following:

  - `  DATABASE_ID  ` with the ID of your database
  - `  LOCATION  ` with the location of your database
  - `  KMS_PROJECT  ` with the project that contains your CMEK key
  - `  KMS_LOCATION  ` with the location that contains your CMEK key and key ring
  - `  KMS_KEYRING_ID  ` with the ID of your CMEK key ring
  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database

Confirm that your Firestore database is protected with Firebase CLI:

``` text
firebase firestore:databases:get DATABASE_ID --project FIRESTORE_PROJECT
```

The following CMEK information appears in the response message:

  - The **KMS Key Name** field provides the full key resource name that is used to encrypt your Firestore CMEK database.
  - The **Active Key Versions** field provides a list of all [key versions](https://cloud.google.com/kms/docs/resource-hierarchy#key_versions) currently used by this CMEK database. During [key rotation](https://cloud.google.com/kms/docs/key-rotation) , you can have multiple active key versions.

### Terraform

To create a CMEK-enabled database, use the `  google_firestore_database  ` resource. For more information and examples, see [`  google_firestore_database  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/firestore_database) .

``` text
resource "google_firestore_database" "database" {
  project     = "FIRESTORE_PROJECT"
  name        = "DATABASE_ID"
  location_id = "FIRESTORE_DATABASE_LOCATION"
  type        = "DATABASE_TYPE"

  cmek_config {
    kms_key_name = "KMS_KEY_NAME"
  }
}
```

Replace the following:

  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database

  - `  DATABASE_ID  ` with an ID for the database

  - `  FIRESTORE_DATABASE_LOCATION  ` with the Firestore location for the database

  - `  DATABASE_TYPE  ` with either `  FIRESTORE_NATIVE  ` for Native mode or `  DATASTORE_MODE  ` for Datastore mode.

  - `  KMS_KEY_NAME  ` with the name you assigned to the key. Use the full resource name for the key in the format of:
    
    `  projects/ KMS_PROJECT /locations/ KMS_LOCATION /keyRings/ KMS_KEYRING_ID /cryptoKeys/ KMS_KEY_ID  `

### Access a CMEK-protected database

All the read, write, and query operations sent to a CMEK-protected database should function the same as with a Google default encrypted database. For example, you don't need to provide a key for each request.

## Restore a CMEK-protected database

Before you restore CMEK-protected database from a backup:

  - Decide if you want to restore the database to CMEK encryption, to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), or to the same encryption as the backup.

  - Prepare the key (primary-version) and the key version that you used to encrypt the backup. Enable both the key and the key version.

### gcloud

### Restore a CMEK-protected database to CMEK encryption

To restore to CMEK encryption, run the [gcloud firestore databases restore](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/restore) command with the optional `  encryption-type  ` and `  kms-key-name  ` flags to configure the encryption type for the restored database. If you don't specify the encryption type, the restored database will use the same encryption configuration as the backup.

``` text
  gcloud firestore databases restore
  --encryption-type=customer-managed-encryption
  --kms-key-name=KMS_KEY_NAME
```

Replace `  KMS_KEY_NAME  ` with the name that you assigned to the key. Use the full resource name for the key in the following format:

`  projects/ KMS_PROJECT /locations/ KMS_LOCATION /keyRings/ KMS_KEYRING_ID /cryptoKeys/ KMS_KEY_ID  `

### Restore a CMEK-protected database to default encryption

To restore to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), set the `  encryption-type  ` flag in the following way:

``` text
  gcloud firestore databases restore
  --encryption-type=google-default-encryption
```

### Restore a CMEK-protected database to the same encryption type as the backup

To restore to the same encryption type as the backup, set the `  encryption-type  ` flag in the following way:

``` text
  gcloud firestore databases restore --encryption-type=use-source-encryption
```

### Firebase CLI

### Restore a CMEK-protected database to CMEK encryption

To restore to CMEK encryption, use the optional `  encryption-type  ` and `  kms-key-name  ` flag. If you don't specify the encryption type, the restored database will use the same encryption configuration as the backup.

``` text
firebase firestore:databases:restore \
--database DATABASE_ID \
--backup 'projects/FIRESTORE_PROJECT/locations/FIRESTORE_LOCATION/backups/BACKUP_ID' \
--encryption-type CUSTOMER_MANAGED_ENCRYPTION \
--kms-key-name projects/KMS_PROJECT/locations/KMS_LOCATION/keyRings/KMS_KEYRING_ID/cryptoKeys/KMS_KEY_ID \
--project FIRESTORE_PROJECT
```

Replace the following:

  - `  DATABASE_ID  ` with the ID of your database
  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database
  - `  FIRESTORE_LOCATION  ` with the location of your Firestore database
  - `  BACKUP_ID  ` with the ID of your backup
  - `  KMS_PROJECT  ` with the project that contains your CMEK key
  - `  KMS_LOCATION  ` with the location that contains your CMEK key and key ring
  - `  KMS_KEYRING_ID  ` with the ID of your CMEK key ring

Confirm that your restored Firestore database is CMEK-encrypted:

``` text
firebase firestore:databases:get DATABASE_ID --project FIRESTORE_PROJECT
```

### Restore a CMEK-protected database to default encryption

To restore to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), set the `  encryption-type  ` flag in the following way:

``` text
firebase firestore:databases:restore \
--database DATABASE_ID \
--backup 'projects/FIRESTORE_PROJECT/locations/FIRESTORE_LOCATION/backups/BACKUP_ID' \
--encryption-type GOOGLE_DEFAULT_ENCRYPTION \
--project FIRESTORE_PROJECT
```

Replace the following:

  - `  DATABASE_ID  ` with the ID of your database
  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database
  - `  FIRESTORE_LOCATION  ` with the location of your Firestore database
  - `  BACKUP_ID  ` with the ID of your backup

### Restore a CMEK-protected database to the same encryption type as the backup

To restore to the same encryption type as the backup, set the `  encryption-type  ` flag in the following way:

``` text
firebase firestore:databases:restore \
--database DATABASE_IDD \
--backup 'projects/FIRESTORE_PROJECT/locations/FIRESTORE_LOCATION/backups/BACKUP_ID' \
--encryption-type USE_SOURCE_ENCRYPTION
```

Replace the following:

  - `  DATABASE_ID  ` with the ID of your database
  - `  FIRESTORE_PROJECT  ` with the project to use for your Firestore database
  - `  FIRESTORE_LOCATION  ` with the location of your Firestore database
  - `  BACKUP_ID  ` with the ID of your backup

## Clone a CMEK-protected database

Before you clone a CMEK-protected database:

  - Decide if you want to clone the database to CMEK encryption, to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), or to the same encryption as the source database.

  - Prepare the key (primary-version) and the key version that you used to encrypt the source database. Enable both the key and the key version.

### gcloud

### Clone a CMEK-protected database to CMEK encryption

To clone to CMEK encryption, run the [gcloud firestore databases clone](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/clone) command with the optional `  encryption-type  ` and `  kms-key-name  ` flags to configure the encryption type for the cloned database. If you don't specify the encryption type, the cloned database will use the same encryption configuration as the source database.

``` text
gcloud firestore databases clone \
--encryption-type=customer-managed-encryption \
--kms-key-name=KMS_KEY_NAME
```

Replace `  KMS_KEY_NAME  ` with the name that you assigned to the key. Use the full resource name for the key in the following format:

``` text
projects/KMS_PROJECT/locations/KMS_LOCATION/keyRings/KMS_KEYRING_ID/cryptoKeys/KMS_KEY_ID
```

### Clone a CMEK-protected database to default encryption

To clone to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), set the `  encryption-type  ` flag in the following way:

``` text
gcloud firestore databases clone \
--encryption-type=google-default-encryption
```

### Clone a CMEK-protected database to the same encryption type as the source database

To clone to the same encryption type as the source database, set the `  encryption-type  ` flag in the following way:

``` text
gcloud firestore databases clone \
--encryption-type=use-source-encryption
```

This is also the default behavior if `  --encryption-type  ` is unspecified.

### Firebase CLI

### Clone a CMEK-protected database to CMEK encryption

To clone to CMEK encryption, run the `  firebase firestore:databases:clone  ` command with the optional `  encryption-type  ` and `  kms-key-name  ` flags to configure the encryption type for the cloned database. If you don't specify the encryption type, the cloned database will use the same encryption configuration as the source database.

``` text
firebase firestore:databases:clone \
SOURCE_DATABASE \
DESTINATION_DATABASE \
--encryption-type=CUSTOMER_MANAGED_ENCRYPTION \
--kms-key-name=KMS_KEY_NAME
```

Replace `  KMS_KEY_NAME  ` with the name that you assigned to the key. Use the full resource name for the key in the following format:

``` text
projects/KMS_PROJECT/locations/KMS_LOCATION/keyRings/KMS_KEYRING_ID/cryptoKeys/KMS_KEY_ID
```

### Clone a CMEK-protected database to default encryption

To clone to [Google's default encryption](https://cloud.google.com/security/encryption/default-encryption#googles_default_encryption) (non-CMEK), set the `  encryption-type  ` flag in the following way:

``` text
firebase firestore:databases:clone \
SOURCE_DATABASE \
DESTINATION_DATABASE \
--encryption-type=GOOGLE_DEFAULT_ENCRYPTION
```

### Clone a CMEK-protected database to the same encryption type as the source database

To clone to the same encryption type as the source database, set the `  encryption-type  ` flag in the following way:

``` text
firebase firestore:databases:clone \
SOURCE_DATABASE \
DESTINATION_DATABASE \
--encryption-type=USE_SOURCE_ENCRYPTION
```

This is also the default behavior if `  --encryption-type  ` is unspecified.

## View the key in use

### gcloud

You can use the [databases describe](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/describe) gcloud CLI command to confirm database CMEK configuration:

``` text
gcloud firestore databases describe --database=DATABASE_ID --project=FIRESTORE_PROJECT
```

You should see CMEK information in the `  cmekConfig  ` field in the response similar to the following:

``` text
      cmekConfig:
          activeKeyVersion:
          - projects/PROJECT_ID/locations/us/keyRings/KEYRING_NAME/cryptoKeys/KEY_NAME/cryptoKeyVersions/1
          kmsKeyName: projects/PROJECT_ID/locations/us/keyRings/KEYRING_NAME/cryptoKeys/KEY_NAME
        locationId: nam5
        name: projects/PROJECT_ID/databases/DATABASE_ID
```

The response includes the following information:

  - `  kmsKeyName  ` : the full key resource name of the key that's used to encrypt your CMEK-protected database.
  - `  activeKeyVersion  ` : a list of all [key versions](https://cloud.google.com/kms/docs/resource-hierarchy#key_versions) currently in use by the CMEK-protected database. During [key rotation](https://cloud.google.com/kms/docs/key-rotation) , you can have multiple active key versions. Both the old key version and new key version need to be available during key rotation. Don't disable the old key version until it no longer appears in the `  activeKeyVersion  ` field.

### REST API

HTTP request:

``` text
GET https://firestore.googleapis.com/v1/{name=projects/FIRESTORE_PROJECT/databases/DATABASE_ID}
```

In the request body configure CMEK in the `  cmek_config.kms_key_name  ` field. Set to the full resource ID of a Cloud KMS key. Only a key in the same location as this database is allowed.

This value should be the Cloud KMS key resource ID in the format of `  projects/{KMS_PROJECT}/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}  `

For more information about other fields, see the [`  database create  ` page](/firestore/native/docs/reference/rest/v1/projects.databases/create) .

Example request and response:

``` text
curl 'https://firestore.googleapis.com/v1/projects/FIRESTORE_PROJECT/databases/{DATABASE_ID}' \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-type: application/json"

—----------------------------------------- Response —--------------------------------------------
{
  "name": "projects/FIRESTORE_PROJECT/databases/{DATABASE_ID}",
  "locationId": "{FIRESTORE_DATABASE_LOCATION}",
  "type": "FIRESTORE_NATIVE",
  "cmekConfig": {
    "kmsKeyName": "projects/{KMS_PROJECT}/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}",
    "activeKeyVersion": [
      "projects/{KMS_PROJECT}/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}/cryptoKeyVersions/1"
    ]
  },
  ……
}
```

## Disable a key

To disable a key associated with a database, complete the following:

1.  [View the key versions in use for a database](#view-key) .
2.  [Disable these key versions in use](https://cloud.google.com/kms/docs/enable-disable#disable) .
3.  Wait for the change to take effect and check if the data is no longer accessible. Changes typically take effect within minutes, but can take up to 3 hours.

When a key used by a database is disabled, expect to receive a `  FAILED_PRECONDITION  ` exception with additional details in the error message, for example:

``` text
{
  "error": {
    "code": 400,
    "message": "The customer-managed encryption key required by the requested resource is not accessible. Error reason:  generic::permission_denied: Permission 'cloudkms.cryptoKeyVersions.useToEncrypt' denied on resource 'projects/FIRESTORE_PROJECT/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}' (or it may not exist).",
    "status": "FAILED_PRECONDITION",
    "details": [
      {
        "@type": "type.googleapis.com/google.rpc.DebugInfo",
        "detail": "The customer-managed encryption key required by the requested resource is not accessible. Error reason:  generic::permission_denied: Permission 'cloudkms.cryptoKeyVersions.useToEncrypt' denied on resource 'projects/FIRESTORE_PROJECT/locations/{KMS_LOCATION}/keyRings/{KMS_KEYRING_ID}/cryptoKeys/{KMS_KEY_ID}' (or it may not exist)"
      }
    ]
  }
}
```

## Enable a key

To re-enable a key associated with a database, complete the following:

1.  [View the key versions in use for a database](#view-key)
2.  [Enable these key versions in use](https://cloud.google.com/kms/docs/enable-disable#enable)
3.  Wait for the change to take effect and check if the data is no longer accessible. Changes typically take effect within minutes, but can take up to 3 hours.

## View audit logs for a Cloud KMS key

Before you enable Cloud KMS Data Access audit logs, you should be familiar with [Cloud Audit Logs](https://cloud.google.com/logging/docs/audit) .

[Cloud KMS Data Access audit logs](https://cloud.google.com/kms/docs/audit-logging) show you when Firestore or any other products that are configured to use your CMEK key make encrypt/decrypt calls to Cloud KMS. Firestore does not issue an encrypt/decrypt call on every data request, but instead maintains a poller that checks the key periodically. The polling results appear in the audit logs.

You can set up and interact with the audit logs in the [Google Cloud console](https://cloud.google.com/logging/docs/audit/configure-data-access#config-console) :

1.  Make sure that [logging is enabled](https://cloud.google.com/logging/docs/audit/configure-data-access#config-console-enable) for the Cloud KMS API in your project.

2.  Go to **Cloud Logging** in the Google Cloud console.

3.  Limit the log entries to your Cloud KMS key by adding the following lines to the Query builder:
    
    ``` text
    resource.type="cloudkms_cryptokey"
    resource.labels.key_ring_id = KMS_KEYRING
    resource.labels.crypto_key_id = KMS_KEY
    resource.labels.location=KMS_LOCATION
    ```
    
    Replace the following:
    
      - `  KMS_KEY  ` with the name of the CMEK key
      - `  KMS_KEYRING  ` with the KMS key ring that contains the key
      - `  KMS_LOCATION  ` with the location of the key and key ring
    
    The log shows a couple log entries about every five minutes per database. The log entries look similar to these examples:
    
    ``` text
    Info 2021-03-20 08:02:24.869 EDT Cloudkms.googleapis.com Decrypt projects/cloud-kms-project/locations/us-central1/keyRings/firestore-keys/cryptoKeys/my-cmek-key service-123456789123@gcp-sa-firestore.iam.gserviceaccount.com
    audit_log, method: "Decrypt", principal_email: "service-1234567891011@gcp-sa-firestore.iam.gserviceaccount.com"
    
    Info 2021-03-20 08:02:24.913 EDT Cloudkms.googleapis.com Encrypt projects/cloud-kms-project/locations/us-central1/keyRings/firestore-keys/cryptoKeys/my-cmek-key service-123456789123@gcp-sa-firestore.iam.gserviceaccount.com
    audit_log, method: "Encrypt", principal_email: "service-123456789123@gcp-sa-firestore.iam.gserviceaccount.com"
    ```

See [Understanding audit logs](https://cloud.google.com/logging/docs/audit/understanding-audit-logs) for details about interpreting audit logs.

## Configure a CMEK organization policy

To specify encryption compliance requirements for Firestore databases in your organization, use a [CMEK organization policy constraint](https://cloud.google.com/kms/docs/cmek-org-policy) .

### Require CMEK protection

Configure `  constraints/gcp.restrictNonCmekServices  ` to require CMEK for Firestore database creation. Set the constraint to `  deny  ` and add `  firestore.googleapis.com  ` to the deny list, for example:

``` text
 gcloud resource-manager org-policies deny gcp.restrictNonCmekServices  is:firestore.googleapis.com --project=FIRESTORE_PROJECT
```

Replace `  FIRESTORE_PROJECT  ` with the project to restrict.

To learn more about configuring organization policies, see [Creating and editing policies](https://cloud.google.com/resource-manager/docs/organization-policy/creating-managing-policies#creating_and_editing_policies) .

After the policy takes effect, you receive a `  FAILED_PRECONDITION  ` exception and error message if you try to create a non-CMEK database under the affected project. For example, an exception looks like:

``` text
{
  "error": {
    "code": 400,
    "message": "Constraint 'constraints/gcp.restrictNonCmekServices' violated for 'projects/FIRESTORE_PROJECT' attempting to perform the operation 'google.firestore.admin.v1.FirestoreAdmin.CreateDatabase' with violated value 'firestore.googleapis.com'. See https://cloud.google.com/resource-manager/docs/organization-policy/org-policy-constraints for more information.",
    "status": "FAILED_PRECONDITION",
    "details": [
      {
        "@type": "type.googleapis.com/google.rpc.PreconditionFailure",
        "violations": [
          {
            "type": "constraints/gcp.restrictNonCmekServices",
            "subject": "orgpolicy:projects/FIRESTORE_PROJECT",
            "description": "Constraint 'constraints/gcp.restrictNonCmekServices' violated for 'projects/FIRESTORE_PROJECT' attempting to perform the operation 'google.firestore.admin.v1.FirestoreAdmin.CreateDatabase' with violated value 'firestore.googleapis.com'. See https://cloud.google.com/resource-manager/docs/organization-policy/org-policy-constraints for more information."
          }
        ]
```

### Limit the use of keys for CMEK

To limit which Cloud KMS keys are used for CMEK protection, configure the `  constraints/gcp.restrictCmekCryptoKeyProjects  ` constraint.

As a list constraint, the accepted values are resource hierarchy indicators (for example, `  projects/PROJECT_ID  ` , `  under:folders/FOLDER_ID  ` , and `  under:organizations/ORGANIZATION_ID  ` ). Use this constraint by configuring a list of resource hierarchy indicators and setting the constraint to **Allow** . This configuration restricts supported services so that CMEK keys can be chosen only from the listed projects, folders, and organizations. Requests to create CMEK-protected resources in configured services don't succeed without a Firestore key from one of the allowed resources.

The following example allows only keys from the ALLOWED\_KEY\_PROJECT\_ID for CMEK-protected databases in the specified project:

``` text
gcloud resource-manager org-policies allow gcp.restrictCmekCryptoKeyProjects \
under:projects/ALLOWED_KEY_PROJECT_ID \
--project=FIRESTORE_PROJECT
```

After the policy takes effect, you receive a `  FAILED_PRECONDITION  ` exception and an error message if you violate the constraint. An exception looks like the following:

``` text
{
  "error": {
    "code": 400,
    "message": "Constraint 'constraints/gcp.restrictCmekCryptoKeyProjects' violated for 'projects/FIRESTORE_PROJECT' attempting to perform the operation 'google.firestore.admin.v1.FirestoreAdmin.CreateDatabase' with violated value 'projects/{NOT_ALLOWED_KEY_PROJECT}'. See https://cloud.google.com/resource-manager/docs/organization-policy/org-policy-constraints for more information.",
    "status": "FAILED_PRECONDITION",
    "details": [
      {
        "@type": "type.googleapis.com/google.rpc.PreconditionFailure",
        "violations": [
          {
            "type": "constraints/gcp.restrictCmekCryptoKeyProjects",
            "subject": "orgpolicy:projects/FIRESTORE_PROJECT",
            "description": "Constraint 'constraints/gcp.restrictCmekCryptoKeyProjects' violated for 'projects/FIRESTORE_PROJECT' attempting to perform the operation 'google.firestore.admin.v1.FirestoreAdmin.CreateDatabase' with violated value 'projects/{NOT_ALLOWED_KEY_PROJECT}'. See https://cloud.google.com/resource-manager/docs/organization-policy/org-policy-constraints for more information."
          }
        ]
      }
    ]
  }
}
```

## What's next

  - [Read the overview of Firestore and CMEK](/firestore/native/docs/cmek)
