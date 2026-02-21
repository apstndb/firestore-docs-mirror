Build a service by using various CRUD methods.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
// Create an authorized Datastore service using Application Default Credentials.
_db = DatastoreDb.Create(projectId);
// Create a Key factory to construct keys associated with this project.
_keyFactory = _db.CreateKeyFactory("Task");
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/datastore"
)

func createClient(projectID string) (*datastore.Client, error) {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }
 // Note: call the following from main() to ensure the client
 // properly frees all resources.
 // defer client.Close()
 return client, nil
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Create an authorized Datastore service using Application Default Credentials.
private final Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

// Create a Key factory to construct keys associated with this project.
private final KeyFactory keyFactory = datastore.newKeyFactory().setKind("Task");
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// By default, the client will authenticate using the service account file
// specified by the GOOGLE_APPLICATION_CREDENTIALS environment variable and use
// the project specified by the GCLOUD_PROJECT environment variable. See
// https://googlecloudplatform.github.io/google-cloud-node/#/docs/datastore/latest/guides/authentication
const {Datastore} = require('@google-cloud/datastore');

// Creates a client
const datastore = new Datastore();
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Create a Cloud Datastore client.
 *
 * @param string $projectId The Google Cloud project ID.
 */
function build_service(string $projectId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);
    return $datastore;
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def create_client(project_id):
    return datastore.Client(project_id)
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/datastore"

datastore = Google::Cloud::Datastore.new
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
