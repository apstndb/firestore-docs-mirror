Creates and saves an Entity of the hypothetical type "Task"

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
///  Adds a task entity to the Datastore
/// </summary>
/// <param name="description">The task description.</param>
/// <returns>The key of the entity.</returns>
Key AddTask(string description)
{
    Entity task = new Entity()
    {
        Key = _keyFactory.CreateIncompleteKey(),
        ["description"] = new Value()
        {
            StringValue = description,
            ExcludeFromIndexes = true
        },
        ["created"] = DateTime.UtcNow,
        ["done"] = false
    };
    return _db.Insert(task);
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
/**
 * Adds a task entity to the Datastore.
 *
 * @param description The task description
 * @return The {@link Key} of the entity
 * @throws DatastoreException if the ID allocation or put fails
 */
Key addTask(String description) {
  Key key = datastore.allocateId(keyFactory.newKey());
  Entity task =
      Entity.newBuilder(key)
          .set(
              "description",
              StringValue.newBuilder(description).setExcludeFromIndexes(true).build())
          .set("created", Timestamp.now())
          .set("done", false)
          .build();
  datastore.put(task);
  return key;
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function addTask(description) {
  const taskKey = datastore.key('Task');
  const entity = {
    key: taskKey,
    data: [
      {
        name: 'created',
        value: new Date().toJSON(),
      },
      {
        name: 'description',
        value: description,
        excludeFromIndexes: true,
      },
      {
        name: 'done',
        value: false,
      },
    ],
  };

  try {
    await datastore.save(entity);
    console.log(`Task ${taskKey.id} created successfully.`);
  } catch (err) {
    console.error('ERROR:', err);
  }
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Create a new task with a given description.
 *
 * @param string $projectId The Google Cloud project ID.
 * @param string $description
 */
function add_task(string $projectId, string $description)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);

    $taskKey = $datastore->key('Task');
    $task = $datastore->entity(
        $taskKey,
        [
            'created' => new DateTime(),
            'description' => $description,
            'done' => false
        ],
        ['excludeFromIndexes' => ['description']]
    );
    $datastore->insert($task);
    printf('Created new task with ID %d.' . PHP_EOL, $task->key()->pathEnd()['id']);
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def add_task(client: datastore.Client, description: str):
    # Create an incomplete key for an entity of kind "Task". An incomplete
    # key is one where Datastore will automatically generate an Id
    key = client.key("Task")

    # Create an unsaved Entity object, and tell Datastore not to index the
    # `description` field
    task = datastore.Entity(key, exclude_from_indexes=("description",))

    # Apply new field values and save the Task entity to Datastore
    task.update(
        {
            "created": datetime.datetime.now(tz=datetime.timezone.utc),
            "description": description,
            "done": False,
        }
    )
    client.put(task)
    return task.key
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def add_task description
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  task = datastore.entity "Task" do |t|
    t["description"] = description
    t["created"]     = Time.now
    t["done"]        = false
    t.exclude_from_indexes! "description", true
  end

  datastore.save task

  puts task.key.id

  task.key.id
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
