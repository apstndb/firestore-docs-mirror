Create Client with Project ID

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)
  - [Create a Firestore database by using a server client library](/firestore/native/docs/create-database-server-client-library)
  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Get started with Cloud Firestore](https://firebase.google.com/docs/firestore/quickstart)
  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
FirestoreDb db = FirestoreDb.Create(project);
Console.WriteLine("Created Cloud Firestore client with project ID: {0}", project);
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
FirestoreOptions firestoreOptions =
    FirestoreOptions.getDefaultInstance().toBuilder()
        .setProjectId(projectId)
        .setCredentials(GoogleCredentials.getApplicationDefault())
        .build();
Firestore db = firestoreOptions.getService();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Firestore\FirestoreClient;

/**
 * Initialize Cloud Firestore with a provided project ID.
 *
 * @param string $projectId Your Google Cloud Project ID
 */
function setup_client_create_with_project_id(string $projectId): void
{
    // Create the Cloud Firestore client with a provided project ID.
    $db = new FirestoreClient([
        'projectId' => $projectId,
    ]);
    printf('Created Cloud Firestore client with project ID: %s' . PHP_EOL, $projectId);
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import firestore

# The `project` parameter is optional and represents which project the client
# will act on behalf of. If not supplied, the client falls back to the default
# project inferred from the environment.
db = firestore.Client(project="my-project-id")
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
