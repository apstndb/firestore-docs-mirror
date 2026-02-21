Example datastore list tasks

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Returns a list of all task entities in ascending order of creation time.
/// </summary>
IEnumerable<Entity> ListTasks()
{
    Query query = new Query("Task")
    {
        Order = { { "created", PropertyOrder.Types.Direction.Descending } }
    };
    return _db.RunQuery(query).Entities;
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

// ListTasks returns all the tasks in ascending order of creation time.
func ListTasks(projectID string) ([]*Task, error) {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }

 var tasks []*Task
 // Create a query to fetch all Task entities, ordered by "created".
 query := datastore.NewQuery("Task").Order("created")
 keys, err := client.GetAll(ctx, query, &tasks)
 if err != nil {
     return nil, err
 }

 // Set the id field on each Task from the corresponding key.
 for i, key := range keys {
     tasks[i].id = key.ID
 }

 return tasks, nil
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
/**
 * Returns a list of all task entities in ascending order of creation time.
 *
 * @throws DatastoreException if the query fails
 */
Iterator<Entity> listTasks() {
  Query<Entity> query =
      Query.newEntityQueryBuilder().setKind("Task").setOrderBy(OrderBy.asc("created")).build();
  return datastore.run(query);
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function listTasks() {
  const query = datastore.createQuery('Task').order('created');

  const [tasks] = await datastore.runQuery(query);
  console.log('Tasks:');
  tasks.forEach(task => {
    const taskKey = task[datastore.KEY];
    console.log(taskKey.id, task);
  });
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Return an iterator for all the tasks in ascending order of creation time.
 *
 * @param string $projectId The Google Cloud project ID.
 */
function list_tasks(string $projectId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);

    $query = $datastore->query()
        ->kind('Task')
        ->order('created');
    $result = $datastore->runQuery($query);
    /* @var Entity $task */
    foreach ($result as $index => $task) {
        printf('ID: %s' . PHP_EOL, $task->key()->pathEnd()['id']);
        printf('  Description: %s' . PHP_EOL, $task['description']);
        printf('  Status: %s' . PHP_EOL, $task['done'] ? 'done' : 'created');
        printf('  Created: %s' . PHP_EOL, $task['created']->format('Y-m-d H:i:s e'));
        print(PHP_EOL);
    }
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def list_tasks(client: datastore.Client):
    # Create a query against all of your objects of kind "Task"
    query = client.query(kind="Task")
    query.order = ["created"]

    return list(query.fetch())
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def list_tasks
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  query = datastore.query("Task").order("created")
  tasks = datastore.run query

  tasks.each do |t|
    puts t["description"]
    puts t["done"] ? "  Done" : "  Not Done"
    puts "  ID: #{t.key.id}"
  end
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
