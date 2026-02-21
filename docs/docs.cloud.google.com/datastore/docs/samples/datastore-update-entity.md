Example datastore mark task done

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Marks a task entity as done.
/// </summary>
/// <param name="id">The ID of the task entity as given by Key.</param>
/// <returns>true if the task was found.</returns>
bool MarkDone(long id)
{
    using (var transaction = _db.BeginTransaction())
    {
        Entity task = transaction.Lookup(_keyFactory.CreateKey(id));
        if (task != null)
        {
            task["done"] = true;
            transaction.Update(task);
        }
        transaction.Commit();
        return task != null;
    }
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

// MarkDone marks the task done with the given ID.
func MarkDone(projectID string, taskID int64) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }
 defer client.Close()
 // Create a key using the given integer ID.
 key := datastore.IDKey("Task", taskID, nil)

 // In a transaction load each task, set done to true and store.
 _, err = client.RunInTransaction(ctx, func(tx *datastore.Transaction) error {
     var task Task
     if err := tx.Get(key, &task); err != nil {
         return err
     }
     task.Done = true
     _, err := tx.Put(key, &task)
     return err
 })
 return err
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
/**
 * Marks a task entity as done.
 *
 * @param id The ID of the task entity as given by {@link Key#id()}
 * @return true if the task was found, false if not
 * @throws DatastoreException if the transaction fails
 */
boolean markDone(long id) {
  Transaction transaction = datastore.newTransaction();
  try {
    Entity task = transaction.get(keyFactory.newKey(id));
    if (task != null) {
      transaction.put(Entity.newBuilder(task).set("done", true).build());
    }
    transaction.commit();
    return task != null;
  } finally {
    if (transaction.isActive()) {
      transaction.rollback();
    }
  }
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function markDone(taskId) {
  const transaction = datastore.transaction();
  const taskKey = datastore.key(['Task', datastore.int(taskId)]);

  try {
    await transaction.run();
    const [task] = await transaction.get(taskKey);
    task.done = true;
    transaction.save({
      key: taskKey,
      data: task,
    });
    await transaction.commit();
    console.log(`Task ${taskId} updated successfully.`);
  } catch (err) {
    await transaction.rollback();
  }
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Mark a task with a given id as done.
 *
 * @param string $projectId The Google Cloud project ID.
 * @param string $taskId
 */
function mark_done(string $projectId, string $taskId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);

    $taskKey = $datastore->key('Task', $taskId);
    $transaction = $datastore->transaction();
    $task = $transaction->lookup($taskKey);
    $task['done'] = true;
    $transaction->upsert($task);
    $transaction->commit();
    printf('Task %d updated successfully.' . PHP_EOL, $taskId);
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def mark_done(client: datastore.Client, task_id: str | int):
    with client.transaction():
        # Create a key for an entity of kind "Task", and with the supplied
        # `task_id` as its Id
        key = client.key("Task", task_id)
        # Use that key to load the entity
        task = client.get(key)

        if not task:
            raise ValueError(f"Task {task_id} does not exist.")

        # Update a field indicating that the associated
        # work has been completed
        task["done"] = True

        # Persist the change back to Datastore
        client.put(task)
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def mark_done task_id
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  task = datastore.find "Task", task_id

  task["done"] = true

  datastore.save task
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
