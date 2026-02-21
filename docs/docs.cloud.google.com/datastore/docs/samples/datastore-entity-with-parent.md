Use entity with parent.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Structuring Data for Strong Consistency](/datastore/docs/concepts/structuring_for_strong_consistency)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key taskListKey = _db.CreateKeyFactory("TaskList").CreateKey(TestUtil.RandomName());
Key taskKey = new KeyFactory(taskListKey, "Task").CreateKey("sampleTask");
Entity task = new Entity()
{
    Key = taskKey,
    ["category"] = "Personal",
    ["done"] = false,
    ["priority"] = 4,
    ["description"] = "Learn Cloud Datastore"
};
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
parentKey := datastore.NameKey("TaskList", "default", nil)
key := datastore.IncompleteKey("Task", parentKey)

task := Task{
 Category:    "Personal",
 Done:        false,
 Priority:    4,
 Description: "Learn Cloud Datastore",
}

// A complete key is assigned to the entity when it is Put.
var err error
key, err = client.Put(ctx, key, &task)
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey =
    datastore
        .newKeyFactory()
        .addAncestors(PathElement.of("TaskList", "default"))
        .setKind("Task")
        .newKey("sampleTask");
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 4)
        .set("description", "Learn Cloud Datastore")
        .build();
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key([
  'TaskList',
  'default',
  'Task',
  'sampleTask',
]);

const task = {
  key: taskKey,
  data: {
    category: 'Personal',
    done: false,
    priority: 4,
    description: 'Learn Cloud Datastore',
  },
};
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$parentKey = $datastore->key('TaskList', 'default');
$key = $datastore->key('Task')->ancestorKey($parentKey);
$task = $datastore->entity(
    $key,
    [
        'Category' => 'Personal',
        'Done' => false,
        'Priority' => 4,
        'Description' => 'Learn Cloud Datastore'
    ]
);
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key_with_parent = client.key("TaskList", "default", "Task", "sampleTask")

task = datastore.Entity(key=key_with_parent)

task.update(
    {
        "category": "Personal",
        "done": False,
        "priority": 4,
        "description": "Learn Cloud Datastore",
    }
)
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
# task_name = "sampleTask"
task_key = datastore.key [["TaskList", task_list_name], ["Task", task_name]]

task = datastore.entity task_key do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
