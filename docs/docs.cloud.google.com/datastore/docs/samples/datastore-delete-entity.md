Delete a task.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Deletes a task entity.
/// </summary>
/// <param name="id">The ID of the task entity as given by Key.</param>
void DeleteTask(long id)
{
    _db.Delete(_keyFactory.CreateKey(id));
}
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

// DeleteTask deletes the task with the given ID.
func DeleteTask(projectID string, taskID int64) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }
 return client.Delete(ctx, datastore.IDKey("Task", taskID, nil))
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
/**
 * Deletes a task entity.
 *
 * @param id The ID of the task entity as given by {@link Key#id()}
 * @throws DatastoreException if the delete fails
 */
void deleteTask(long id) {
  datastore.delete(keyFactory.newKey(id));
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function deleteTask(taskId) {
  const taskKey = datastore.key(['Task', datastore.int(taskId)]);

  await datastore.delete(taskKey);
  console.log(`Task ${taskId} deleted successfully.`);
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Delete a task with a given id.
 *
 * @param string $projectId The Google Cloud project ID.
 * @param string $taskId
 */
function delete_task(string $projectId, string $taskId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);

    $taskKey = $datastore->key('Task', $taskId);
    $datastore->delete($taskKey);

    printf('Task %d deleted successfully.' . PHP_EOL, $taskId);
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def delete_task(client: datastore.Client, task_id: str | int):
    # Create a key for an entity of kind "Task", and with the supplied
    # `task_id` as its Id
    key = client.key("Task", task_id)
    # Use that key to delete its associated document, if it exists
    client.delete(key)
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def delete_task task_id
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  task = datastore.find "Task", task_id

  datastore.delete task
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
