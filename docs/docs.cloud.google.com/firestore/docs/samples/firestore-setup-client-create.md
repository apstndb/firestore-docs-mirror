Creating a Firestore client

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)
  - [Create a Firestore database by using a server client library](/firestore/native/docs/create-database-server-client-library)
  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Get started with Cloud Firestore](https://firebase.google.com/docs/firestore/quickstart)
  - [Getting data](/firestore/native/docs/query-data/get-data)

## Code sample

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "flag"
 "fmt"
 "log"

 "google.golang.org/api/iterator"

 "cloud.google.com/go/firestore"
)

func createClient(ctx context.Context) *firestore.Client {
 // Sets your Google Cloud Platform project ID.
 projectID := "YOUR_PROJECT_ID"

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Failed to create client: %v", err)
 }
 // Close client when done with
 // defer client.Close()
 return client
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Option 1: Initialize a Firestore client with a specific `projectId` and
//           authorization credential.
FirestoreOptions firestoreOptions =
    FirestoreOptions.getDefaultInstance().toBuilder()
        .setProjectId(projectId)
        .setCredentials(GoogleCredentials.getApplicationDefault())
        .build();
Firestore db = firestoreOptions.getService();

// Option 2: Initialize a Firestore client with default values inferred from
//           your environment.
Firestore db = FirestoreOptions.getDefaultInstance().getService();
```

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const admin = require('firebase-admin');

initializeApp({
  // The `projectId` parameter is optional and represents which project the
  // client will act on behalf of. If not supplied, it falls back to the default
  // project inferred from the environment.
  projectId: 'my-project-id',
});
const db = getFirestore();
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Firestore\FirestoreClient;

/**
 * Initialize Cloud Firestore with default project ID.
 */
function setup_client_create(string $projectId = null)
{
    // Create the Cloud Firestore client
    if (empty($projectId)) {
        // The `projectId` parameter is optional and represents which project the
        // client will act on behalf of. If not supplied, the client falls back to
        // the default project inferred from the environment.
        $db = new FirestoreClient();
        printf('Created Cloud Firestore client with default project ID.' . PHP_EOL);
    } else {
        $db = new FirestoreClient([
            'projectId' => $projectId,
        ]);
        printf('Created Cloud Firestore client with project ID: %s' . PHP_EOL, $projectId);
    }
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

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/firestore"

# The `project_id` parameter is optional and represents which project the
# client will act on behalf of. If not supplied, the client falls back to the
# default project inferred from the environment.
firestore = Google::Cloud::Firestore.new project_id: project_id

puts "Created Cloud Firestore client with given project ID."
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
