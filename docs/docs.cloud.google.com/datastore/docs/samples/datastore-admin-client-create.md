Create a new Datastore admin client.

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
// Create client
DatastoreAdminClient datastoreAdminClient = DatastoreAdminClient.Create();
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "fmt"
 "io"

 admin "cloud.google.com/go/datastore/admin/apiv1"
)

// clientCreate creates a new Datastore admin client.
func clientCreate(w io.Writer) (*admin.DatastoreAdminClient, error) {
 ctx := context.Background()
 client, err := admin.NewDatastoreAdminClient(ctx)
 if err != nil {
     return nil, fmt.Errorf("admin.NewDatastoreAdminClient: %w", err)
 }
 // Close client when done using it.
 // defer client.Close()
 fmt.Fprintf(w, "Admin client created\n")
 return client, nil
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud.datastore_admin_v1 import DatastoreAdminClient


def client_create():
    """Creates a new Datastore admin client."""
    client = DatastoreAdminClient()

    print("Admin client created\n")
    return client
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# Import the client library
require "google/cloud/datastore/admin/v1"

# Instantiate a client
client = Google::Cloud::Datastore::Admin::V1::DatastoreAdmin::Client.new
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
