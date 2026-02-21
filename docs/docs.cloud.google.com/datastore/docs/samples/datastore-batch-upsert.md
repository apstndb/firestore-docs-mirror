Perform a batch upsert.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Entities, Properties, and Keys](/datastore/docs/concepts/entities)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
var taskList = new[]
{
    new Entity()
    {
        Key = _keyFactory.CreateIncompleteKey(),
        ["category"] = "Personal",
        ["done"] = false,
        ["priority"] = 4,
        ["description"] = "Learn Cloud Datastore"
    },
    new Entity()
    {
        Key = _keyFactory.CreateIncompleteKey(),
        ["category"] = "Personal",
        ["done"] = "false",
        ["priority"] = 5,
        ["description"] = "Integrate Cloud Datastore"
    }
};
var keyList = _db.Upsert(taskList[0], taskList[1]);
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
tasks := []*Task{
 {
     Category:    "Personal",
     Done:        false,
     Priority:    4,
     Description: "Learn Cloud Datastore",
 },
 {
     Category:    "Personal",
     Done:        false,
     Priority:    5,
     Description: "Integrate Cloud Datastore",
 },
}
keys := []*datastore.Key{
 datastore.IncompleteKey("Task", nil),
 datastore.IncompleteKey("Task", nil),
}

keys, err := client.PutMulti(ctx, keys, tasks)
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
FullEntity<IncompleteKey> task1 =
    FullEntity.newBuilder(keyFactory.newKey())
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 4)
        .set("description", "Learn Cloud Datastore")
        .build();
FullEntity<IncompleteKey> task2 =
    Entity.newBuilder(keyFactory.newKey())
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 5)
        .set("description", "Integrate Cloud Datastore")
        .build();
List<Entity> tasks = datastore.add(task1, task2);
Key taskKey1 = tasks.get(0).getKey();
Key taskKey2 = tasks.get(1).getKey();
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey1 = this.datastore.key(['Task', 1]);
const taskKey2 = this.datastore.key(['Task', 2]);

const task1 = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};

const task2 = {
  category: 'Work',
  done: false,
  priority: 8,
  description: 'Integrate Cloud Datastore',
};

const entities = [
  {
    key: taskKey1,
    data: task1,
  },
  {
    key: taskKey2,
    data: task2,
  },
];

await datastore.upsert(entities);
// Tasks inserted successfully.
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$result = $datastore->upsertBatch($tasks);
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

task1 = datastore.Entity(client.key("Task", 1))

task1.update(
    {
        "category": "Personal",
        "done": False,
        "priority": 4,
        "description": "Learn Cloud Datastore",
    }
)

task2 = datastore.Entity(client.key("Task", 2))

task2.update(
    {
        "category": "Work",
        "done": False,
        "priority": 8,
        "description": "Integrate Cloud Datastore",
    }
)

client.put_multi([task1, task2])
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task_1 = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end

task_2 = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 5
  t["description"] = "Integrate Cloud Datastore"
end

tasks = datastore.save task_1, task_2
task_key_1 = tasks[0].key
task_key_2 = tasks[1].key
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
