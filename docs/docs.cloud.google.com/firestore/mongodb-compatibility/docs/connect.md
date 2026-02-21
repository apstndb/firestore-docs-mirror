# Authenticate and connect to a database

## Connection requirements

The following are required for Firestore with MongoDB compatibility clients:

  - Drivers must connect in `  load balanced  ` mode. This prevents the drivers from trying to understand the exact server topology they are connecting to.
  - Drivers must connect with SSL enabled.
  - Drivers must disable retryable writes. Firestore with MongoDB compatibility doesn't support retryable writes. You don't need to disable retryable reads as they are supported.

## Retrieve the connection string

The database connection string depends on the UID of the database, the location of database, and the authentication mechanism. The following instructions describe how the connection string is formed.

**Note:** A database has both a database ID and UID. The database ID is the resource name you set when you create a database. The UID is a system-generated UUID4 for the database.

The exact connection string depends on the authentication mechanism, but the base connection string uses the following format:

``` text
mongodb://UID.LOCATION.firestore.goog:443/DATABASE_ID?loadBalanced=true&tls=true&retryWrites=false
```

You can obtain the base connection string in one of the following ways:

##### Console

1.  In the Google Cloud console, go to the **Databases** page.

2.  In the list of databases, click the database ID of the relevant database.

3.  The **Explorer** panel displays the base connection string. Copy and use this connection string to connect to your database.

##### gcloud

Use `  gcloud firestore database describe  ` to retrieve the UID and location information:

``` text
gcloud firestore databases describe \
--database=DATABASE_ID \
--format='yaml(locationId, uid)'
```

Replace DATABASE\_ID with the database ID.

The output includes the location and UID of the database. Use this information to construct the base connection string.

Use the base connection string and one of the following methods to authenticate and connect to your database:

  - [Username and password (SCRAM)](#scram)
  - [Compute Engine service account](#gce-vm)
  - [Cloud Run service account](#cloud-run)
  - [Google Auth Library](#connect_with_the_google_auth_library)

## Connect with Username and password (SCRAM)

Follow these steps to create a user credential for your database and connect to your database.

### Before you begin

To get the permissions that you need to create a user, ask your administrator to grant you the [userCredsAdmin](/iam/docs/roles-permissions/firestore#datastore.userCredsAdmin) ( `  roles/datastore.userCredsAdmin  ` ) IAM role on your database. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Create a user and connect to a database

To create a user for your Firestore with MongoDB compatibility database, use one of the following method:

##### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select a database from the list of databases.

3.  In the navigation menu, click **Security** .

4.  Click **Add User** .

5.  Enter a **Username** .

6.  Select a role for the new user.

7.  Click **Add** .
    
    The new user's password will be displayed in the confirmation dialog.
    
    **Caution:** The password is displayed once and is not retrievable. Store this password for future use.

##### gcloud CLI

1.  To authenticate with SCRAM, you must first create a user credential. Use the `  gcloud firestore user-creds  ` command:
    
    ``` text
    gcloud firestore user-creds create USERNAME --database=DATABASE_ID
    ```
    
    Replace the following:
    
      - USERNAME : the username to create.
      - DATABASE\_ID : the database ID.
    
    The output of this command includes the user's password.
    
    **Caution:** The password is displayed once and is not retrievable. Store this password for future use.
    
    The output resembles the following:
    
    ``` text
    name: projects/PROJECT_NAME/databases/DATABASE_ID/userCreds/USERNAME
    resourceIdentity:
      principal: principal://firestore.googleapis.com/projects/PROJECT_NUMBER/name/databases/DATABASE_ID/userCreds/USERNAME
    securePassword: PASSWORD
    ```

2.  By default, this new user credential does not have any permissions. For read and write access to the database, add the `  roles/datastore.user  ` role for this specific database:
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_NAME \
    --member='principal://firestore.googleapis.com/projects/PROJECT_NUMBER/name/databases/DATABASE_ID/userCreds/USERNAME' \
    --role=roles/datastore.user \
    --condition='expression=resource.name == "projects/PROJECT_NAME/databases/DATABASE_ID",title="CONDITION_TITLE"'
    ```
    
    Replace the following:
    
      - PROJECT\_NAME : the name of your project.
      - PROJECT\_NUMBER : the [project number](/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - DATABASE\_ID : the database ID.
      - USERNAME : the username you previously created.
      - CONDITION\_TITLE : a title for this condition. This condition [restricts access to only this database](/firestore/mongodb-compatibility/docs/create-databases#configure_per-database_access_permissions) .

##### Java

This section provides a code example for creating user credentials and configuring the IAM policy using Java administrative client libraries. The sample uses the [Firestore Admin Client](https://cloud.google.com/java/docs/reference/google-cloud-firestore/latest/com.google.cloud.firestore.v1.FirestoreAdminClient) library for creating a username and password, and the [Google Cloud Resource Manager](https://cloud.google.com/java/docs/reference/google-cloud-resourcemanager/latest/overview) library for configuring IAM.

For Maven builds, you can use the following coordinates:

``` text
com.google.cloud:google-cloud-firestore-admin:3.33.1
com.google.cloud:google-cloud-resourcemanager:1.76.0
```

Provision user credentials and an IAM policy:

``` text
import com.google.cloud.firestore.v1.FirestoreAdminClient;
import com.google.cloud.resourcemanager.v3.ProjectName;
import com.google.cloud.resourcemanager.v3.ProjectsClient;
import com.google.firestore.admin.v1.CreateUserCredsRequest;
import com.google.firestore.admin.v1.GetUserCredsRequest;
import com.google.firestore.admin.v1.UserCreds;
import com.google.iam.v1.Binding;
import com.google.iam.v1.GetIamPolicyRequest;
import com.google.iam.v1.GetPolicyOptions;
import com.google.iam.v1.Policy;
import com.google.iam.v1.SetIamPolicyRequest;
import com.google.protobuf.FieldMask;
import com.google.type.Expr;

public class FirestoreUserCredsExample {
  /**
   * Provision user credentials and configure an IAM policy to allow SCRAM authentication into the
   * specified Firestore with Mongo Compatibility database.
   */
  private static void provisionFirestoreUserCredsAndIAM(
      String projectId, String databaseId, String userName) throws Exception {
    UserCreds userCreds = createUserCreds(projectId, databaseId, userName);

    // Note the password returned in the UserCreds proto - it cannot be retrieved again
    // after the initial call to the createUserCreds API.
    System.out.printf(
        "Created credentials for username: %s:\nIAM principal: %s\nPassword: [%s]\n",
        userName, userCreds.getResourceIdentity().getPrincipal(), userCreds.getSecurePassword());

    // Provision an IAM binding for the principal associated with these user credentials.
    updateIamPolicyForUserCreds(projectId, databaseId, userName, userCreds);

    // Emit the password again.
    System.out.printf(
        "Successfully configured IAM policy for database: %s, username: %s\n",
        databaseId, userName);
    System.out.printf("Please make a note of the password: [%s]\n", userCreds.getSecurePassword());
  }

  /** Provision new user credentials using the FirestoreAdminClient. */
  private static UserCreds createUserCreds(String projectId, String databaseId, String userName)
      throws Exception {
    FirestoreAdminClient firestoreAdminClient = FirestoreAdminClient.create();
    return firestoreAdminClient.createUserCreds(
        CreateUserCredsRequest.newBuilder()
            .setParent(String.format("projects/%s/databases/%s", projectId, databaseId))
            .setUserCredsId(userName)
            .build());
  }

  /** Update the IAM policy using the Resource Manager ProjectsClient. */
  private static void updateIamPolicyForUserCreds(
      String projectId, String databaseId, String userName, UserCreds userCreds) throws Exception {
    try (ProjectsClient projectsClient = ProjectsClient.create()) {
      ProjectName projectName = ProjectName.of(projectId);

      // Get the current IAM policy.
      Policy currentPolicy =
          projectsClient.getIamPolicy(
              GetIamPolicyRequest.newBuilder()
                  .setResource(projectName.toString())
                  .setOptions(GetPolicyOptions.newBuilder().setRequestedPolicyVersion(3).build())
                  .build());

      String role = "roles/datastore.user";
      String title = String.format("Conditional IAM binding for %s", userName);
      String expression =
          String.format("resource.name == \"projects/%s/databases/%s\"", projectId, databaseId);

      // Construct an updated IAM policy with an additional binding for the user credentials.
      Policy.Builder policyBuilder = currentPolicy.toBuilder();
      Binding newBinding =
          Binding.newBuilder()
              .setRole(role)
              .setCondition(Expr.newBuilder().setTitle(title).setExpression(expression).build())
              .addMembers(userCreds.getResourceIdentity().getPrincipal())
              .build();
      policyBuilder.addBindings(newBinding);

      // Update the policy
      SetIamPolicyRequest request =
          SetIamPolicyRequest.newBuilder()
              .setResource(projectName.toString())
              .setPolicy(policyBuilder.build())
              .setUpdateMask(FieldMask.newBuilder().addPaths("bindings").addPaths("etag").build())
              .build();
      System.out.println(request);

      Policy updatedPolicy = projectsClient.setIamPolicy(request);
      System.out.println("Policy updated successfully: " + updatedPolicy);
    }
  }
}
```

##### Python

This section provides a code example for creating user credentials and configuring the IAM policy using Python administrative client libraries. The sample uses the [Google Cloud Firestore API client library](https://pypi.org/project/google-cloud-firestore/) library for creating a username and password, and the [Google Cloud Iam API client library](https://pypi.org/project/google-cloud-iam/) and the [Google Cloud Resource Manager API client library](https://pypi.org/project/google-cloud-resource-manager/) for configuring IAM.

The required Python libraries can be installed with the pip tool:

``` text
pip install google-cloud-iam
pip install google-cloud-firestore
pip install google-cloud-resource-manager
```

Provision user credentials and an IAM policy:

``` text
from google.cloud import resourcemanager_v3
from google.cloud.firestore_admin_v1 import FirestoreAdminClient
from google.cloud.firestore_admin_v1 import types
from google.iam.v1 import iam_policy_pb2
from google.iam.v1 import policy_pb2
from google.type import expr_pb2


def create_user_creds(project_id: str, database_id: str, user_name: str):
  """Provision new user credentials using the FirestoreAdminClient."""
  client = FirestoreAdminClient()
  request = types.CreateUserCredsRequest(
      parent=f'projects/{project_id}/databases/{database_id}',
      user_creds_id=user_name,
  )
  response = client.create_user_creds(request)
  return response


def update_iam_policy_for_user_creds(
    project_id: str, database_id: str, user_name: str, user_creds
):
  """Update the IAM policy using the Resource Manager ProjectsClient."""
  client = resourcemanager_v3.ProjectsClient()
  request = iam_policy_pb2.GetIamPolicyRequest()
  request.resource = f'projects/{project_id}'
  request.options.requested_policy_version = 3

  # Get the current IAM policy
  current_policy = client.get_iam_policy(request)

  # Construct an updated IAM policy with an additional binding
  # for the user credentials.
  updated_policy = policy_pb2.Policy()
  binding = policy_pb2.Binding()
  iam_condition = expr_pb2.Expr()

  iam_condition.title = f'Conditional IAM binding for {user_name}'
  iam_condition.expression = (
      f'resource.name == "projects/{project_id}/databases/{database_id}"'
  )

  binding.role = 'roles/datastore.user'
  binding.condition.CopyFrom(iam_condition)
  binding.members.append(user_creds.resource_identity.principal)
  updated_policy.bindings.append(binding)

  # Update the policy
  updated_policy.MergeFrom(current_policy)
  set_policy_request = iam_policy_pb2.SetIamPolicyRequest()
  set_policy_request.resource = f'projects/{project_id}'
  set_policy_request.policy.CopyFrom(updated_policy)

  final_policy = client.set_iam_policy(set_policy_request)
  print(f'Policy updated successfully {final_policy}')


def provision_firestore_user_creds_and_iam(
    project_id: str, database_id: str, user_name: str
):
  """Provision user credentials and configure an IAM policy."""
  user_creds = create_user_creds(project_id, database_id, user_name)

  # Note the password returned in the UserCreds proto - it cannot be
  # retrieved again after the initial call to the create_user_creds API.
  print(f'Created credentials for username: {user_name}')
  print(f'IAM principal: {user_creds.resource_identity.principal}')
  print(f'Password: [{user_creds.secure_password}]')

  # Provision an IAM binding for the principal associated with
  # these user credentials.
  update_iam_policy_for_user_creds(
      project_id, database_id, user_name, user_creds
  )

  # Emit the password again
  print(
      f'Successfully configured IAM policy for database: {database_id},'
      f' username: {user_name}'
  )
  print(f'Please make a note of the password: [{user_creds.secure_password}]')
```

Use the following connection string to connect to your database with SCRAM:

``` text
mongodb://USERNAME:PASSWORD@UID.LOCATION.firestore.goog:443/DATABASE_ID?loadBalanced=true&authMechanism=SCRAM-SHA-256&tls=true&retryWrites=false
```

Replace the following:

  - USERNAME : the username.
  - PASSWORD : the password you generated for this user.
  - UID : the UID of the database. For example: f116f93a-519c-208a-9a72-3ef6c9a1f081
  - LOCATION : the location of the database.
  - DATABASE\_ID : the database ID.

## Connect with the Google Auth Library

The following code sample registers an OIDC callback handler uses the Google Cloud [standard OAuth library](https://github.com/googleapis/google-auth-library-java) .

This library lets you use a number of different types of authentication (Application Default Credentials, Workload Identity Federation).

This requires [adding the auth library as a dependency](https://github.com/googleapis/google-auth-library-java?tab=readme-ov-file#importing-the-auth-library) :

``` text
// Maven
<dependency>
  <groupId>com.google.auth</groupId>
  <artifactId>google-auth-library-oauth2-http</artifactId>
  <version>1.19.0</version>
</dependency>

// Gradle
implementation 'com.google.auth:google-auth-library-oauth2-http:1.19.0'
```

The following code sample demonstrates how to connect:

``` text
val db = MongoClients.create(
    clientSettings(
      "DATABASE_UID",
      "LOCATION"
    ).build()
  ).getDatabase("DATABASE_ID")


/**
 * Creates a connection to a Firestore with MongoDB Compatibility database.
 * @param databaseUid The uid of the database to connect to as a string. For example: f116f93a-519c-208a-9a72-3ef6c9a1f081
 * @param locationId The location of the database to connect to, for example: nam5, us-central1, us-east4 etc...
 * @param environment Determines whether to try and fetch an authentication credential from the
 * Compute Engine VM metadata service or whether to call gcloud.
 */
private static MongoClientSettings.Builder clientSettings(
  String databaseUid: String
  String locationId:String
): MongoClientSettings.Builder {
  MongoCredential credential =
    MongoCredential.createOidcCredential(null)
      .withMechanismProperty(
        MongoCredential.OIDC_CALLBACK_KEY,
        new MongoCredential.OidcCallback() {
          @Override
          MongoCredential.OidcCallbackResult onRequest(
MongoCredential.OidcCallbackContext context) {
     // Customize this credential builder for additional credential types.
     GoogleCredentials credentials = GoogleCredentials.getApplicationDefault();
            return new MongoCredential.OidcCallbackResult(
         credentials.getAccessToken().getTokenValue(),
         Duration.between(Instant.now(),
credentials.getAccessToken().getExpirationTime().toInstant()));
          }
        },
      );
  return MongoClientSettings.builder()
    .hosts(listOf(ServerAddress(
        "$databaseUid.$locationId.firestore.goog", 443)))
    .credential(credential)
    .applyToClusterSettings(builder ->
         builder.mode(ClusterConnectionMode.LOAD_BALANCED))
    ).applyToSslSettings(ssl -> ssl.enabled(true)).retryWrites(false);
}
```

Replace the following:

  - DATABASE\_UID : the UID of the database. For example: f116f93a-519c-208a-9a72-3ef6c9a1f081
  - LOCATION : the location of your database.
  - DATABASE\_ID the database ID.

## Connect from a Google Cloud compute environment

This section describes connecting to Firestore with MongoDB compatibility from a Google Cloud compute environment, such as Compute Engine or a Cloud Run service or job.

### Connect from a Compute Engine VM

You can authenticate and connect to your database using a Compute Engine service account. To do this, create an IAM policy for the Google Cloud project that contains your database.

#### Before you begin

Configure a user-managed service account for your VM:

  - To configure service account during VM creation, see [Create a VM that uses a user-managed service account](https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances) .
  - To configure service account on an existing VM, see [Change the attached service account](https://cloud.google.com/compute/docs/instances/change-service-account) .

See the instructions in the [Configure credentials](#configure-creds) sections to complete the IAM policy configuration for your Compute Engine service account.

### Connect from Cloud Run

You can authenticate and connect to your database using a Cloud Run service account. To do this, create an IAM policy for the Google Cloud project that contains your database.

#### Before you begin

  - To configure the service account for Cloud Run, see [Configure service identity](https://cloud.google.com/run/docs/configuring/services/service-identity#configure-service-identity)
  - To determine the service account that is already associated with your Cloud Run service, see [gcloud run services describe](https://cloud.google.com/sdk/gcloud/reference/run/services/describe)

See the instructions in the [Configure credentials](#configure-creds) sections to complete the IAM policy configuration for your Cloud Run service account.

### Configure credentials

To grant the service account the `  roles/datastore.user  ` role for read and write to Firestore, run the following command:

``` text
gcloud projects add-iam-policy-binding PROJECT_NAME --member="serviceAccount:SERVICE_ACCOUNT_EMAIL" --role=roles/datastore.user
```

Replace the following:

  - PROJECT\_NAME : the name of your project.
  - SERVICE\_ACCOUNT\_EMAIL : the email address for the service account that you created.

### Construct the connection string

Use the following format to construct the connection string:

``` text
mongodb://DATABASE_UID.LOCATION.firestore.goog:443/DATABASE_ID?loadBalanced=true&tls=true&retryWrites=false&authMechanism=MONGODB-OIDC&authMechanismProperties=ENVIRONMENT:gcp,TOKEN_RESOURCE:FIRESTORE
```

Replace the following:

  - DATABASE\_UID : the UID of the database. For example: f116f93a-519c-208a-9a72-3ef6c9a1f081
  - LOCATION : the location of your database.
  - DATABASE\_ID the database ID.

For more information on retrieving the UID and location, see [Retrieve the connection string](#connection_string) .

## Connect with a temporary access token

You can use a temporary Google Cloud access token to run diagnostic tools such as `  mongosh  ` . You can use [`  gcloud auth print-access-token  `](https://cloud.google.com/sdk/gcloud/reference/auth/print-access-token) to authenticate with a short-term access token. This token is valid for one hour.

For example, use the following command to connect to your database with `  mongosh  ` :

``` text
mongosh --tls \
      --username access_token --password $(gcloud auth print-access-token) \
      'mongodb://UID.LOCATION.firestore.goog:443/DATABASE_ID?loadBalanced=true&authMechanism=PLAIN&authSource=$external&retryWrites=false'
```

Replace the following:

  - DATABASE\_UID : the UID of the database. For example: f116f93a-519c-208a-9a72-3ef6c9a1f081
  - LOCATION : the database location
  - DATABASE\_ID : a database ID
