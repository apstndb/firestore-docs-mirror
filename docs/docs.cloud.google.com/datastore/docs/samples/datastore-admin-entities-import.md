Import admin entities to Datastore

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Datastore.Admin.V1;
using Google.LongRunning;
using Google.Protobuf.WellKnownTypes;
using System;
using System.Collections.Generic;

public class ImportEntitiesSample
{
    public bool ImportEntities(
        string projectId = "your-project-id",
        // For information on accepted input URL formats, see
        // https://cloud.google.com/datastore/docs/reference/admin/rpc/google.datastore.admin.v1#google.datastore.admin.v1.ImportEntitiesRequest
        string inputUrl = "[URL to file containing data]",
        string kind = "Task",
        string namespaceId = "default")
    {
        // Create client
        DatastoreAdminClient datastoreAdminClient = DatastoreAdminClient.Create();

        IDictionary<string, string> labels = new Dictionary<string, string> { { "cloud_datastore_samples", "true" }, };
        EntityFilter entityFilter = new EntityFilter()
        {
            Kinds = { kind },
            NamespaceIds = { namespaceId }
        };

        Operation<Empty, ImportEntitiesMetadata> response = datastoreAdminClient.ImportEntities(projectId, labels, inputUrl, entityFilter);

        // Poll until the returned long-running operation is complete
        Operation<Empty, ImportEntitiesMetadata> completedResponse = response.PollUntilCompleted();

        if (completedResponse.IsFaulted)
        {
            Console.WriteLine($"Error while Importing Entities: {completedResponse.Exception}");
            throw completedResponse.Exception;
        }

        Console.WriteLine($"Entities imported successfully.");

        return completedResponse.IsCompleted;
    }
}
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
 "cloud.google.com/go/datastore/admin/apiv1/adminpb"
)

// entitiesImport imports entities into Datastore.
func entitiesImport(w io.Writer, projectID, inputURL string) error {
 // projectID := "project-id"
 // inputURL := "gs://bucket-name/overall-export-metadata-file"
 ctx := context.Background()
 client, err := admin.NewDatastoreAdminClient(ctx)
 if err != nil {
     return fmt.Errorf("admin.NewDatastoreAdminClient: %w", err)
 }
 defer client.Close()

 req := &adminpb.ImportEntitiesRequest{
     ProjectId: projectID,
     InputUrl:  inputURL,
 }
 op, err := client.ImportEntities(ctx, req)
 if err != nil {
     return fmt.Errorf("ImportEntities: %w", err)
 }
 if err = op.Wait(ctx); err != nil {
     return fmt.Errorf("Wait: %w", err)
 }
 fmt.Fprintf(w, "Entities were imported\n")
 return nil
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const {Datastore} = require('@google-cloud/datastore');
const datastore = new Datastore();

async function importEntities() {
  /**
   * TODO(developer): Uncomment these variables before running the sample.
   */
  // const file = 'YOUR_FILE_NAME';

  const [importOperation] = await datastore.import({file});

  // Uncomment to await the results of the operation.
  // await importOperation.promise();

  // Or cancel the operation.
  await importOperation.cancel();

  // You may also choose to include only specific kinds and namespaces.
  const [specificImportOperation] = await datastore.import({
    file,
    kinds: ['Employee', 'Task'],
    namespaces: ['Company'],
  });

  // Uncomment to await the results of the operation.
  // await specificImportOperation.promise();

  // Or cancel the operation.
  await specificImportOperation.cancel();
}

importEntities();
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
def import_entities(project_id, input_url):
    """Imports entities into Datastore."""
    # project_id := "project-id"
    # input_url := "gs://bucket-name/overall-export-metadata-file"
    client = DatastoreAdminClient()

    op = client.import_entities({"project_id": project_id, "input_url": input_url})
    response = op.result(timeout=300)

    print("Entities were imported\n")
    return response
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# project_id = "project-id"
# input_url = "gs://bucket-name/overall-export-metadata-file"
op = client.import_entities project_id: project_id, input_url: input_url

op.wait_until_done!
raise op.error.message if op.error?

response = op.response
# Process the response.

metadata = op.metadata
# Process the metadata.

puts "Entities were imported"
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
