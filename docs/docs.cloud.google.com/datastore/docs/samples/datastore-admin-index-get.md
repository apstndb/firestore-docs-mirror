Get admin index

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Datastore.Admin.V1;
using System;
using Index = Google.Cloud.Datastore.Admin.V1.Index;

public class GetIndexSample
{
    public Index GetIndex(
        string projectId = "your-project-id",
        string indexId = "your-index-id")
    {
        // Create client
        DatastoreAdminClient datastoreAdminClient = DatastoreAdminClient.Create();

        // Initialize request argument(s)
        GetIndexRequest getIndexRequest = new GetIndexRequest
        {
            ProjectId = projectId,
            IndexId = indexId
        };

        Index index = datastoreAdminClient.GetIndex(getIndexRequest);

        Console.WriteLine($"Index Id: {index.IndexId}");
        Console.WriteLine($"Kind: {index.Kind}");
        Console.WriteLine("Properties:");
        foreach (var property in index.Properties)
        {
            Console.WriteLine($"Property: {property.Name}");
            Console.WriteLine($"Direction: {property.Direction}");
        }
        return index;
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

// indexGet gets an index.
func indexGet(w io.Writer, projectID, indexID string) (*adminpb.Index, error) {
 // projectID := "my-project-id"
 // indexID := "my-index"
 ctx := context.Background()
 client, err := admin.NewDatastoreAdminClient(ctx)
 if err != nil {
     return nil, fmt.Errorf("admin.NewDatastoreAdminClient: %w", err)
 }
 defer client.Close()

 req := &adminpb.GetIndexRequest{
     ProjectId: projectID,
     IndexId:   indexID,
 }
 index, err := client.GetIndex(ctx, req)
 if err != nil {
     return nil, fmt.Errorf("client.GetIndex: %w", err)
 }

 fmt.Fprintf(w, "Got index: %v\n", index.IndexId)
 return index, nil
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const {Datastore} = require('@google-cloud/datastore');
const datastore = new Datastore();

async function getIndex() {
  /**
   * TODO(developer): Uncomment these variables before running the sample.
   */
  // const indexId = 'YOUR_INDEX_ID';

  // Create a reference to the index before performing operations on it.
  const index = datastore.index(indexId);

  // Get the index's metadata, including its state, properties, and more.
  const [metadata] = await index.getMetadata();
  console.log('Properties:', metadata.properties);
}

getIndex();
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
def get_index(project_id, index_id):
    """Gets an index."""
    # project_id := "my-project-id"
    # index_id := "my-index"
    client = DatastoreAdminClient()
    index = client.get_index({"project_id": project_id, "index_id": index_id})

    print("Got index: %v\n", index.index_id)
    return index
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# project_id = "project-id"
# index_id = "my-index"
index = client.get_index project_id: project_id, index_id: index_id
puts "Got index: #{index.index_id}"
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
