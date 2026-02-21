List indexes within a Datastore project

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Datastore.Admin.V1;
using System;
using System.Collections.Generic;

public class ListIndexesSample
{
    public IEnumerable<Google.Cloud.Datastore.Admin.V1.Index> ListIndexes(string projectId = "your-project-id")
    {
        // Create client
        DatastoreAdminClient datastoreAdminClient = DatastoreAdminClient.Create();

        // Initialize request argument(s)
        ListIndexesRequest listIndexesRequest = new ListIndexesRequest
        {
            ProjectId = projectId
        };

        var response = datastoreAdminClient.ListIndexes(listIndexesRequest);

        foreach (var index in response)
        {
            Console.WriteLine($"Index Id: {index.IndexId}");
            Console.WriteLine($"Kind: {index.Kind}");

            Console.WriteLine("Properties:");
            foreach (var property in index.Properties)
            {
                Console.WriteLine($"Property: {property.Name}");
                Console.WriteLine($"Direction: {property.Direction}");
            }
        }

        return response;
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
 "google.golang.org/api/iterator"
)

// indexList lists the indexes.
func indexList(w io.Writer, projectID string) ([]*adminpb.Index, error) {
 // projectID := "my-project-id"
 ctx := context.Background()
 client, err := admin.NewDatastoreAdminClient(ctx)
 if err != nil {
     return nil, fmt.Errorf("admin.NewDatastoreAdminClient: %w", err)
 }
 defer client.Close()

 req := &adminpb.ListIndexesRequest{
     ProjectId: projectID,
 }
 it := client.ListIndexes(ctx, req)
 var indices []*adminpb.Index
 for {
     index, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return nil, fmt.Errorf("ListIndexes: %w", err)
     }
     indices = append(indices, index)
     fmt.Fprintf(w, "Got index: %v\n", index.IndexId)
 }

 fmt.Fprintf(w, "Got lists of indexes\n")
 return indices, nil
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const {Datastore} = require('@google-cloud/datastore');
const datastore = new Datastore();

async function listIndexes() {
  const [indexes] = await datastore.getIndexes();

  console.log(`${indexes.length} indexes returned.`);

  // Each returned Index object includes metadata about the index.
  const [firstIndex] = indexes;
  console.log('Properties:', firstIndex.metadata.properties);

  // You may also get Index references as a readable object stream.
  datastore
    .getIndexesStream()
    .on('data', index => {
      console.log('Properties:', index.metadata.properties);
    })
    .on('end', () => {
      // All matching Index objects have been returned.
    });
}

listIndexes();
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
def list_indexes(project_id):
    """Lists the indexes."""
    # project_id := "my-project-id"
    client = DatastoreAdminClient()

    indexes = []
    for index in client.list_indexes({"project_id": project_id}):
        indexes.append(index)
        print("Got index: %v\n", index.index_id)

    print("Got list of indexes\n")
    return indexes
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# project_id = "project-id"
indexes = client.list_indexes(project_id: project_id).map do |index|
  puts "Got index: #{index.index_id}"
  index
end

puts "Got list of indexes"
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
