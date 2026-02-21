Data objects in Firestore in Datastore mode are known as *entities* . An entity has one or more named *properties* , each of which can have one or more values. Entities of the same kind don't need to have the same properties, and an entity's values for a given property don't all need to be of the same data type. (If necessary, an application can establish and enforce such restrictions in its own data model.)

Datastore mode supports a variety of [data types for property values](#properties_and_value_types) . These include, among others:

  - Integers
  - Floating-point numbers
  - Strings
  - Dates
  - Binary data

Each entity in a Datastore mode database has a *key* that uniquely identifies it. The key consists of the following components:

  - The *namespace* of the entity, which allows for [*multitenancy*](/datastore/docs/concepts/multitenancy)
  - The [*kind*](#kinds_and_identifiers) of the entity, which categorizes it for the purpose of queries
  - An [*identifier*](#kinds_and_identifiers) for the individual entity, which can be either
      - a *key name* string
      - an integer *numeric ID*
  - An optional [*ancestor path*](#ancestor_paths) locating the entity within the database hierarchy

An application can fetch an individual entity from the database using the entity's key, or it can retrieve one or more entities by issuing a [*query*](/datastore/docs/concepts/queries) based on the entities' keys or property values.

Firestore in Datastore mode itself does not enforce any restrictions on the structure of entities, such as whether a given property has a value of a particular type; this task is left to the application.

The snippets on this page build upon the example at [Getting started with Firestore in Datastore mode](/datastore/docs/datastore-api-tutorial) .

## Work with entities

Applications can use the Firestore in Datastore mode API to create, retrieve, update, and delete entities. If the application knows the complete key for an entity (or can derive it from its parent key, kind, and identifier), it can use the key to operate directly on the entity. An application can also obtain an entity's key as a result of a query; see the [Queries](/datastore/docs/concepts/queries) topic for more information.

**Note:** If you want to learn about creating, modifying, or deleting entities in the Google Cloud console, see the [Quickstart](/datastore/docs/store-query-data) .

### Create an entity

You create a new entity by initializing it and setting its properties:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["category"] = "Personal",
    ["done"] = false,
    ["priority"] = 4,
    ["description"] = "Learn Cloud Datastore"
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Category        string
 Done            bool
 Priority        float64
 Description     string `datastore:",noindex"`
 PercentComplete float64
 Created         time.Time
}
task := &Task{
 Category:        "Personal",
 Done:            false,
 Priority:        4,
 Description:     "Learn Cloud Datastore",
 PercentComplete: 10.0,
 Created:         time.Now(),
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey = datastore.newKeyFactory().setKind("Task").newKey("sampleTask");
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("done", false)
        .set("priority", 4)
        .set("description", "Learn Cloud Datastore")
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity('Task', [
    'category' => 'Personal',
    'done' => false,
    'priority' => 4,
    'description' => 'Learn Cloud Datastore'
]);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

task = datastore.Entity(client.key("Task"))
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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end
```

You can save the entity to the database by using `  upsert  ` (which will overwrite an entity if it already exists in Datastore mode) or `  insert  ` (which requires that the entity key not already exist).

Here's how you `  upsert  ` an entity:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
_db.Upsert(_sampleTask);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
key := datastore.IncompleteKey("Task", nil)
key, err := client.Put(ctx, key, task)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task = Entity.newBuilder(keyFactory.newKey("sampleTask")).build();
datastore.put(task);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
const task = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};

const entity = {
  key: taskKey,
  data: task,
};

await datastore.upsert(entity);
// Task inserted successfully.
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$key = $datastore->key('Task', 'sampleTask');
$task = $datastore->entity($key, [
    'category' => 'Personal',
    'done' => false,
    'priority' => 4,
    'description' => 'Learn Cloud Datastore'
]);
$datastore->upsert($task);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

complete_key = client.key("Task", "sampleTask")

task = datastore.Entity(key=complete_key)

task.update(
    {
        "category": "Personal",
        "done": False,
        "priority": 4,
        "description": "Learn Cloud Datastore",
    }
)

client.put(task)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task = datastore.entity "Task", task_name do |t|
  t["category"] = "Personal"
  t["done"] = false
  t["priority"] = 4
  t["description"] = "Learn Cloud Datastore"
end
datastore.save task
```

Here's how you `  insert  ` an entity:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _keyFactory.CreateIncompleteKey()
};
task.Key = _db.Insert(task);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
taskKey := datastore.NameKey("Task", "sampleTask", nil)
_, err := client.RunInTransaction(ctx, func(tx *datastore.Transaction) error {
 // We first check that there is no entity stored with the given key.
 var empty Task
 if err := tx.Get(taskKey, &empty); err != datastore.ErrNoSuchEntity {
     return err
 }
 // If there was no matching entity, store it now.
 _, err := tx.Put(taskKey, &task)
 return err
})
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey = datastore.add(FullEntity.newBuilder(keyFactory.newKey()).build()).getKey();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
const task = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};

const entity = {
  key: taskKey,
  data: task,
};

datastore.insert(entity).then(() => {
  // Task inserted successfully.
});
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity('Task', [
    'category' => 'Personal',
    'done' => false,
    'priority' => 4,
    'description' => 'Learn Cloud Datastore'
]);
$datastore->insert($task);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

with client.transaction():
    incomplete_key = client.key("Task")

    task = datastore.Entity(key=incomplete_key)

    task.update(
        {
            "category": "Personal",
            "done": False,
            "priority": 4,
            "description": "Learn Cloud Datastore",
        }
    )

    client.put(task)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
datastore.transaction do |_tx|
  task = datastore.entity "Task" do |t|
    t["category"] = "Personal"
    t["done"] = false
    t["priority"] = 4
    t["description"] = "Learn Cloud Datastore"
  end
  datastore.save task
end
```

### Retrieve an entity

To retrieve an entity from the database, use its key for a lookup:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = _db.Lookup(_sampleTask.Key);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
var task Task
taskKey := datastore.NameKey("Task", "sampleTask", nil)
err := client.Get(ctx, taskKey, &task)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task = datastore.get(taskKey);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
const [entity] = await datastore.get(taskKey);
// entity = {
//   category: 'Personal',
//   done: false,
//   priority: 4,
//   description: 'Learn Cloud Datastore',
//   [Symbol(KEY)]:
//    Key {
//      namespace: undefined,
//      id: '...',
//      kind: 'Task',
//      path: [Getter]
//    }
//   }
// };
console.log(entity);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->lookup($key);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task", "sampleTask")
task = client.get(key)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task_key = datastore.key "Task", task_name
task = datastore.find task_key
```

### Update an entity

To `  update  ` an existing entity, modify the properties of the entity previously retrieved and store it using the key:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
_sampleTask["priority"] = 5;
_db.Update(_sampleTask);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
taskKey := datastore.NameKey("Task", "sampleTask", nil)
tx, err := client.NewTransaction(ctx)
if err != nil {
 log.Fatalf("client.NewTransaction: %v", err)
}
var task Task
if err := tx.Get(taskKey, &task); err != nil {
 log.Fatalf("tx.Get: %v", err)
}
task.Priority = 5
if _, err := tx.Put(taskKey, &task); err != nil {
 log.Fatalf("tx.Put: %v", err)
}
if _, err := tx.Commit(); err != nil {
 log.Fatalf("tx.Commit: %v", err)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task;
Transaction txn = datastore.newTransaction();
try {
  task = Entity.newBuilder(txn.get(taskKey)).set("priority", 5).build();
  txn.put(task);
  txn.commit();
} finally {
  if (txn.isActive()) {
    txn.rollback();
  }
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
const task = {
  category: 'Personal',
  done: false,
  priority: 4,
  description: 'Learn Cloud Datastore',
};

const entity = {
  key: taskKey,
  data: task,
};

await datastore.update(entity);
// Task updated successfully.
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$transaction = $datastore->transaction();
$key = $datastore->key('Task', 'sampleTask');
$task = $transaction->lookup($key);
$task['priority'] = 5;
$transaction->update($task);
$transaction->commit();
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

with client.transaction():
    key = client.key("Task", "sampleTask")
    task = client.get(key)

    task["done"] = True

    client.put(task)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
datastore.transaction do |_tx|
  task = datastore.find "Task", task_name
  task["priority"] = 5
  datastore.save task
end
```

The provided data overwrites the existing entity. The entire object must be sent to the database. If the entity does not exist, the update will fail. If you want to update-or-create an entity, use `  upsert  ` as described previously. Using a [transaction](/datastore/docs/concepts/transactions#uses_for_transactions) lets you perform the `  get  ` and `  update  ` operations in a single atomic transaction.

**Note:** To delete a property, remove the property from the entity, then save the entity.

### Delete an entity

Given an entity's key, you can `  delete  ` the entity:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
_db.Delete(_sampleTask.Key);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
key := datastore.NameKey("Task", "sampletask", nil)
err := client.Delete(ctx, key)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
datastore.delete(taskKey);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
await datastore.delete(taskKey);
// Task deleted successfully.
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$datastore->delete($taskKey);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task", "sampleTask")
client.delete(key)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task_key = datastore.key "Task", task_name
datastore.delete task_key
```

### Batch operations

Firestore in Datastore mode supports batch versions of the operations which allow it to operate on multiple objects in a single Datastore mode call.

Such batch calls are faster than making separate calls for each individual entity because they incur the overhead for only one service call. If multiple entity groups are involved, the work for all the groups is performed in parallel on the server side.

For example, you can `  upsert  ` multiple entities:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$result = $datastore->upsertBatch($tasks);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

You can look up multiple entities:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
var keys = new Key[] { _keyFactory.CreateKey(1), _keyFactory.CreateKey(2) };
var tasks = _db.Lookup(keys[0], keys[1]);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
var taskKeys []*datastore.Key // Populated with incomplete keys.
tasks := make([]*Task, len(taskKeys))
err := client.GetMulti(ctx, taskKeys, &tasks)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Iterator<Entity> tasks = datastore.get(taskKey1, taskKey2);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey1 = this.datastore.key(['Task', 1]);
const taskKey2 = this.datastore.key(['Task', 2]);

const keys = [taskKey1, taskKey2];

const [tasks] = await datastore.get(keys);
// Tasks retrieved successfully.
console.log(tasks);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$result = $datastore->lookupBatch($keys);
if (isset($result['found'])) {
    // $result['found'] is an array of entities.
} else {
    // No entities found.
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

keys = [client.key("Task", 1), client.key("Task", 2)]
tasks = client.get_multi(keys)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name_1 = "sampleTask1"
# task_name_2 = "sampleTask2"
task_key_1 = datastore.key "Task", task_name_1
task_key_2 = datastore.key "Task", task_name_2
tasks = datastore.find_all task_key_1, task_key_2
```

You can delete multiple entities:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
var keys = new Key[] { _keyFactory.CreateKey(1), _keyFactory.CreateKey(2) };
_db.Delete(keys);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
err := client.DeleteMulti(ctx, taskKeys)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
datastore.delete(taskKey1, taskKey2);
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey1 = this.datastore.key(['Task', 1]);
const taskKey2 = this.datastore.key(['Task', 2]);

const keys = [taskKey1, taskKey2];

await datastore.delete(keys);
// Tasks deleted successfully.
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$result = $datastore->deleteBatch($keys);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

keys = [client.key("Task", 1), client.key("Task", 2)]
client.delete_multi(keys)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name_1 = "sampleTask1"
# task_name_2 = "sampleTask2"
task_key_1 = datastore.key "Task", task_name_1
task_key_2 = datastore.key "Task", task_name_2
datastore.delete task_key_1, task_key_2
```

Batch operations don't change your read, write, or delete costs, which are documented at [Pricing and Quota](/datastore/docs/pricing) . You will be charged for every key in a batched operation, whether or not each key exists.

The size of the entities involved in an operation does not affect the read, write, or delete costs. However, the size of entities does impact your [storage size costs](/datastore/docs/concepts/storage-size) .

**Note:** The multiple updates specified in a non-transactional `  commit()  ` are **not** performed transactionally. So if the `  commit  ` ends with an error, it is possible that some, none, or all of the requested operations have been performed. If you need transactional batch updates, use the [transactional API](/datastore/docs/concepts/transactions) .

### Increment and other property transforms

Use property transforms like `  increment  ` to make server-side updates to a property. A property transform avoids an additional client-side read operation to get the current value and avoids a client-side calculation to determine the new value.

Datastore mode supports the following property transforms:

  - `  increment  `
  - `  maximum  `
  - `  minimum  `
  - `  appendMissingElements  `
  - `  removeAllFromArray  `
  - `  setToServerValue(REQUEST_TIME)  `

**Note:** Each of these operation is billed for one read operation and one write operation.

The following example demonstrate a property transform. This operation increments properties by the specified values:

### REST

``` text
POST https://datastore.googleapis.com/v1/projects/{projectId}:commit
{
  "mode": "NON_TRANSACTIONAL",
  "mutations": [
    {
      "propertyMask": {},  // Empty write mask indicates only transforms can change the entity.
      "propertyTransforms": [
        {
          "property": "quantity",
          "increment": {
            "integerValue": 2
          }
        },
        {
          "property": "inStock",
          "maximum": {
            "integerValue": 100
          }
        },
      ]
      "upsert": {
        "key": {
          "path": [
            {
              "kind": "Items",
              "name": "entity_1"
            }
          ]
        }
      }
    }
  ]
}
```

The following example sets a property value to the time at which the server processed the request with millisecond precision.

### REST

``` text
POST https://datastore.googleapis.com/v1/projects/{projectId}:commit
{
  "mode": "NON_TRANSACTIONAL",
  "mutations": [
    {
      "propertyMask": {},  // // Empty write mask indicates only transforms can change the entity.
      "propertyTransforms": [
        {
          "property": "timeField",
          "setToServerValue": "REQUEST_TIME"
        },
      ]
      "upsert": {
        "key": {
          "path": [
            {
              "kind": "Kind_1",
              "name": "entity_1"
            }
          ]
        }
      }
    }
  ]
}
```

The following example appends array elements if they are missing.

### REST

``` text
POST https://datastore.googleapis.com/v1/projects/{projectId}:commit
{
  "mode": "NON_TRANSACTIONAL",
  "mutations": [
    {
      "propertyMask": {},  // Empty write mask indicates only transforms can change the entity.
      "propertyTransforms": [
        {
          "property": "arrayField",
          "appendMissingElements": {
            "values": [
              { "stringValue": "str" }, { "integerValue": 10 }
            ]
          }
        },
      ]
      "upsert": {
        "key": {
          "path": [
            {
              "kind": "Kind_1",
              "name": "entity_1"
            }
          ]
        }
      }
    }
  ]
}
```

#### Mixed types with `     maximum    ` and `     minimum    `

The `  maximum  ` and `  minimum  ` property transforms take either an integer or a double (floating-point number) value as input. The value in the target property can also be an integer or a double value.

If the property is not an integer or double, or if the property doesn't exist, the transformation sets the property to the given input value and type. If a `  maximum  ` operation is applied where the property and the input value are of mixed types (that is, one is an integer and one is a double) the property takes on the type of the larger operand. For `  minimum  ` , the property takes on the type of the smaller operand.

If the operands are equivalent (e.g. 3 and 3.0), the property does not change. 0, 0.0, and -0.0 are all zero. The `  maximum  ` or `  minimum  ` of a zero stored value and zero input value is always the stored value. The `  maximum  ` or `  minimum  ` of any numeric value and NaN is NaN.

#### Multiple mutations and `     PropertyMask    `

Property transforms are sequentially applied after any additional mutations in the request. A [`  PropertyMask  `](/datastore/docs/reference/data/rest/v1/PropertyMask) restricts `  insert  ` , `  update  ` , and `  upsert  ` mutations to the specified properties, but does not restrict property transforms.

For example, starting with the following entity:

### REST

``` text
entity: {
  "key" : {
    "path": [
      {
        "kind": "Kind_1",
        "name": "entity_1"
      }
    ]
  }
  "properties" : {
    "a": 1,
    "b": 2,
    "c": 3
  }
}
```

The following request updates both `  a  ` and `  b  ` and then applies a property transform to property `  b  ` :

``` text
POST https://datastore.googleapis.com/v1/projects/{projectId}:commit
{
  "mode": "NON_TRANSACTIONAL",
  "mutations": [
    {
      "propertyMask": {"a", "b"},  // update property a, b
      "update": {
        "key": {
          "path": [
            {
              "kind": "Kind_1",
              "name": "entity_1"
            }
          ]
        }
        "properties": {
          "a" : "new_value",
          "b" : -2
        }
      },
      "propertyTransforms": [
        {
          "property": "b",
          "increment": { 
            "integerValue": 2
          }
        }
      ]
    }
  ]
}
```

The result is the following:

### REST

``` text
entity: {
  "key" : {
    "path": [
      {
        "kind": "Kind_1",
        "name": "entity_1"
      }
    ]
  }
  "properties" : {
    "a": "new_value",
    "b": 0,
    "c": 3
  }
}
```

## Kinds and identifiers

Each entity is of a particular *kind* , which categorizes the entity for the purpose of queries. For example, a task list application might represent each task to complete with an entity of kind `  Task  ` .

All kind names that begin with two underscores ( `  __  ` ) are reserved and may not be used.

### Assign identifiers

In addition to a kind, each entity has an *identifier* , assigned when the entity is created. Because it is part of the entity's key, the identifier is associated permanently with the entity and cannot be changed. It can be assigned in either of two ways:

  - Your application can specify its own *key name* string for the entity.
    
    For information about the maximum size of the entity key string, see [Limits](/datastore/docs/concepts/limits) .

  - You can have Firestore in Datastore mode automatically assign the entity an integer *numeric ID* .

  - For best practices on assigning identifiers, see the [Keys section in the best practices](/datastore/docs/best-practices#keys) .

The following example creates a key with kind `  Task  ` that uses a key name, "sampleTask", as the identifier:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key key = _db.CreateKeyFactory("Task").CreateKey("sampleTask");
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
taskKey := datastore.NameKey("Task", "sampletask", nil)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey = datastore.newKeyFactory().setKind("Task").newKey("sampleTask");
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key(['Task', 'sampleTask']);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$taskKey = $datastore->key('Task', 'sampleTask');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task", "sampleTask")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task_key = datastore.key "Task", task_name
```

Datastore mode can also automatically assign IDs. Datastore mode generates a random sequence of unused IDs that are approximately uniformly distributed. Each ID can be up to 16 decimal digits long.

The following example creates a key with kind `  Task  ` , without using a key name. The full key (including the automatically assigned ID) of the entity will be returned when an entity with the incomplete key is saved to Datastore mode:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key incompleteKey = _db.CreateKeyFactory("Task").CreateIncompleteKey();
Key key = _db.AllocateId(incompleteKey);
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// A complete key is assigned to the entity when it is Put.
taskKey := datastore.IncompleteKey("Task", nil)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
KeyFactory keyFactory = datastore.newKeyFactory().setKind("Task");
Key taskKey = datastore.allocateId(keyFactory.newKey());
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key('Task');
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$taskKey = $datastore->key('Task');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task_key = datastore.key "Task"
```

If you want to display the entity IDs to the user, and/or depend upon their order, the best thing to do is use manual allocation.

#### Assign your own numeric ID

Instead of using key name strings or generating numeric IDs automatically, advanced applications may sometimes assign their own numeric IDs manually to the entities they create. Be aware, however, that there is nothing to prevent a Datastore mode database from assigning one of your manual numeric IDs to another entity. The only way to avoid such conflicts is to have your application obtain a block of IDs with the `  allocateIds()  ` method.

Datastore mode's automatic ID generator will keep track of IDs that have been allocated with these methods and will avoid reusing them for another entity, so you can safely use such IDs without conflict. You can't manually choose which values are returned by the `  allocateIds()  ` method. The values returned by `  allocateIds()  ` are assigned by Datastore mode.

**Important:** Don't use the value `  0  ` (zero) for the ID. If you do, you will get an automatically allocated ID.

## Ancestor paths

Entities in a Datastore mode database form a hierarchically structured space similar to the directory structure of a file system. When you create an entity, you can optionally designate another entity as its *parent* ; the new entity is a *child* of the parent entity (note that unlike in a file system, the parent entity need not actually exist). An entity without a parent is a *root entity* . The association between an entity and its parent is permanent, and cannot be changed once the entity is created. Datastore mode will never assign the same numeric ID to two entities with the same parent, or to two root entities (those without a parent).

An entity can have multiple levels of ancestors and descendants. An entity's parent, parent's parent, and so on recursively, are its *ancestors* ; its children, children's children, and so on, are its *descendants* . The sequence of entities beginning with a root entity and proceeding from parent to child, leading to a given entity, constitute that entity's *ancestor path* . The complete key identifying the entity consists of a sequence of kind-identifier pairs specifying its ancestor path and terminating with those of the entity itself:

``` text
[User:alice, TaskList:default, Task:sampleTask]
```

For a root entity, the ancestor path is empty and the key consists solely of the entity's own kind and identifier:

``` text
[User:alice]
```

### Levels of parents

Use levels of parents to organize your data. For example, if your application organizes `  Task  ` entities by `  TaskList  ` entities, use one level of parent:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key rootKey = _db.CreateKeyFactory("TaskList").CreateKey("default");
Key key = new KeyFactory(rootKey, "Task").CreateKey("sampleTask");
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
parentKey := datastore.NameKey("TaskList", "default", nil)
taskKey := datastore.NameKey("Task", "sampleTask", parentKey)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key taskKey =
    datastore
        .newKeyFactory()
        .addAncestors(PathElement.of("TaskList", "default"))
        .setKind("Task")
        .newKey("sampleTask");
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key([
  'TaskList',
  'default',
  'Task',
  'sampleTask',
]);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$taskKey = $datastore->key('TaskList', 'default')
    ->pathElement('Task', 'sampleTask');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("TaskList", "default", "Task", "sampleTask")
# Alternatively
parent_key = client.key("TaskList", "default")
key = client.key("Task", "sampleTask", parent=parent_key)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_list_name = "default"
# task_name = "sampleTask"
task_key = datastore.key [["TaskList", task_list_name], ["Task", task_name]]
```

If your application organizes `  Task  ` entities first by `  User  ` entities and then by `  TaskList  ` entities, use multiple levels of parents:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key rootKey = _db.CreateKeyFactory("User").CreateKey("Alice");
Key taskListKey = new KeyFactory(rootKey, "TaskList").CreateKey("default");
Key key = new KeyFactory(taskListKey, "Task").CreateKey("sampleTask");
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
userKey := datastore.NameKey("User", "alice", nil)
parentKey := datastore.NameKey("TaskList", "default", userKey)
taskKey := datastore.NameKey("Task", "sampleTask", parentKey)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
KeyFactory keyFactory =
    datastore
        .newKeyFactory()
        .addAncestors(PathElement.of("User", "Alice"), PathElement.of("TaskList", "default"))
        .setKind("Task");
Key taskKey = keyFactory.newKey("sampleTask");
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const taskKey = datastore.key([
  'User',
  'alice',
  'TaskList',
  'default',
  'Task',
  'sampleTask',
]);
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$taskKey = $datastore->key('User', 'alice')
    ->pathElement('TaskList', 'default')
    ->pathElement('Task', 'sampleTask');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("User", "alice", "TaskList", "default", "Task", "sampleTask")
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# user_name = "alice"
# task_list_name = "default"
# task_name = "sampleTask"
task_key = datastore.key([
                           ["User", user_name],
                           ["TaskList", task_list_name],
                           ["Task", task_name]
                         ])
```

As shown in the earlier example, when you create an entity with a parent, you specify the parent's complete ancestor path.

An application that maintains user profiles may require only one level of parent for the user profile data. For example, use a single level `  User  ` ancestor path for `  Profile  ` entities:

``` text
[User:alice, Profile:public]
```

An application that provides conference room scheduling may require multiple levels of parents, such as a multiple level `  Building/Floor  ` ancestor path for `  Room  ` entities:

``` text
[Building:C, Floor:1, Room:123]
```

## Entity groups

An *entity group* consists of a root entity and all of its descendants. Applications typically use entity groups to organize highly related data. For example, an application could use an entity group to store data about one product, or one user profile.

## Properties and value types

The data values associated with an entity consist of one or more *properties* . Each property has a name and one or more values.

A property can have values of more than one type, and two entities can have values of different types for the same property. A property can be indexed or unindexed (queries that order or filter on a property *p* will ignore entities where *p* is unindexed).

Some example properties:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["category"] = "Personal",
    ["created"] = new DateTime(1999, 01, 01, 0, 0, 0, DateTimeKind.Utc),
    ["done"] = false,
    ["priority"] = 4,
    ["percent_complete"] = 10.0,
    ["description"] = new Value()
    {
        StringValue = "Learn Cloud Datastore",
        ExcludeFromIndexes = true
    },
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Category        string
 Done            bool
 Priority        int
 Description     string `datastore:",noindex"`
 PercentComplete float64
 Created         time.Time
}
task := &Task{
 Category:        "Personal",
 Done:            false,
 Priority:        4,
 Description:     "Learn Cloud Datastore",
 PercentComplete: 10.0,
 Created:         time.Now(),
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("created", Timestamp.now())
        .set("done", false)
        .set("priority", 4)
        .set("percent_complete", 10.0)
        .set(
            "description",
            StringValue.newBuilder("Learn Cloud Datastore").setExcludeFromIndexes(true).build())
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = [
  {
    name: 'category',
    value: 'Personal',
  },
  {
    name: 'created',
    value: new Date(),
  },
  {
    name: 'done',
    value: false,
  },
  {
    name: 'priority',
    value: 4,
  },
  {
    name: 'percent_complete',
    value: 10.0,
  },
  {
    name: 'description',
    value: 'Learn Cloud Datastore',
    excludeFromIndexes: true,
  },
];
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity(
    $key,
    [
        'category' => 'Personal',
        'created' => new DateTime(),
        'done' => false,
        'priority' => 4,
        'percent_complete' => 10.0,
        'description' => 'Learn Cloud Datastore'
    ],
    ['excludeFromIndexes' => ['description']]
);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

import datetime

key = client.key("Task")
task = datastore.Entity(key, exclude_from_indexes=("description",))
task.update(
    {
        "category": "Personal",
        "description": "Learn Cloud Datastore",
        "created": datetime.datetime.now(tz=datetime.timezone.utc),
        "done": False,
        "priority": 4,
        "percent_complete": 10.5,
    }
)
client.put(task)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["created"] = Time.now
  t["done"] = false
  t["priority"] = 4
  t["percent_complete"] = 10.0
  t["description"] = "Learn Cloud Datastore"
  t.exclude_from_indexes! "description", true
end
```

### Array properties

A property with more than one value is called an *array property* . This example contains two array properties. The first is named `  tags  ` with values `  fun  ` and `  programming  ` . The second is named `  collaborators  ` with values `  alice  ` and `  bob  ` .

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["collaborators"] = new ArrayValue() { Values = { "alice", "bob" } },
    ["tags"] = new ArrayValue() { Values = { "fun", "programming" } }
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Tags          []string
 Collaborators []string
}
task := &Task{
 Tags:          []string{"fun", "programming"},
 Collaborators: []string{"alice", "bob"},
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task =
    Entity.newBuilder(taskKey)
        .set("tags", "fun", "programming")
        .set("collaborators", ListValue.of("alice", "bob"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = {
  tags: ['fun', 'programming'],
  collaborators: ['alice', 'bob'],
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity(
    $key,
    [
        'tags' => ['fun', 'programming'],
        'collaborators' => ['alice', 'bob']
    ]
);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

key = client.key("Task")
task = datastore.Entity(key)
task.update({"tags": ["fun", "programming"], "collaborators": ["alice", "bob"]})
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# task_name = "sampleTask"
task = datastore.entity "Task", task_name do |t|
  t["tags"] = ["fun", "programming"]
  t["collaborators"] = ["alice", "bob"]
end
```

Array properties can be useful, for example, when performing queries with equality filters: an entity satisfies the query if any of its values for a property matches the value specified in the filter. For more details on array properties, including issues you should be aware of, see the [Queries](/datastore/docs/concepts/queries) topic.

## Supported value types

Properties are stored as a `  string/value  ` map that contains the entity's property names and values. The following types are supported for values:

### Array

  - REST API
    
      - field name: `  arrayValue  `
      - type: an `  ArrayValue  ` object that contains an array of JSON Value objects
      - An array property can be assigned by using the `  arrayValue  ` field, which is of type [ArrayValue](/datastore/docs/reference/data/rest/Shared.Types/ArrayValue) , and setting its `  values  ` field to an array of values. For a property to be unindexed, set the `  excludeFromIndexes  ` field of the property's value object to `  true  ` .

  - RPC API
    
      - field name: `  array_value  `
      - type: an `  ArrayValue  ` message that contains one or more `  Value  ` messages
      - An array property can be assigned by using the `  array_value  ` field, which is of type [ArrayValue](/datastore/reference/rpc/google.datastore.v1#google.datastore.v1.ArrayValue) , and populating its `  values  ` field with multiple `  Value  ` objects. For a property to be unindexed, set the `  exclude_from_indexes  ` field of `  Value  ` to `  true  ` .

  - Sort order: None

  - Notes: Cannot contain another array value. The value instance must not set `  meaning  ` or `  exclude_from_indexes  ` .

### Boolean

  - REST API
      - field name: `  booleanValue  `
      - type: `  true  ` or `  false  `
  - RPC API
      - field name: `  boolean_value  `
      - type: `  bool  `
  - Sort order: `  false  ` \< `  true  `

### Blob

  - REST API
      - field name: `  blobValue  `
      - type: string. Must be base64-encoded.
  - RPC API
      - field name: `  blob_value  `
      - type: `  bytes  `
  - Sort order: Byte order
  - Notes: Up to 1,500 bytes if property is indexed, up to 1,048,487 bytes (1 MiB - 89 bytes) otherwise.

### Date and time

  - REST API
      - field name: `  timestampValue  `
      - type: string (RFC 3339 formatted, with milliseconds, for instance `  2013-05-14T00:01:00.234Z  ` )
  - RPC API
      - field name: `  timestamp_value  `
      - type: `  Timestamp  `
  - Sort order: Chronological
  - Notes:
      - When stored in Datastore mode, precise only to microseconds; any additional precision is rounded down.
      - When returned as part of a [projection query](/datastore/docs/concepts/queries#projection_queries) , Datastore mode converts timestamp values to microsecond integer values.

### Embedded entity

  - REST API
      - field name: `  entityValue  `
      - type: a JSON entity
  - RPC API
      - field name: `  entity_value  `
      - type: an `  Entity  ` message
  - Sort order: None
  - Notes: When indexed, you can query on subproperties. If you exclude this value from indexing, then all subproperties are also excluded from indexing.

### Floating-point number

  - REST API
      - field name: `  doubleValue  `
      - type: number
  - RPC API
      - field name: `  double_value  `
      - type: `  double  `
  - Sort order: Numeric
  - Notes: 64-bit double precision, IEEE 754

### Geographical point

  - REST API
      - field name: `  geoPointValue  `
      - type: a JSON latitude/longitude pair
  - RPC API
      - field name: `  geo_point_value  `
      - type: a `  LatLng  ` message
  - Sort order: By latitude, then longitude

### Integer

  - REST API
      - field name: `  integerValue  `
      - type: number or string. Use strings for integers that cannot be exactly represented as numbers.
  - RPC API
      - field name: `  integer_value  `
      - type: `  int64  `
  - Sort order: Numeric

### Key

  - REST API
      - field name: `  keyValue  `
      - type: a JSON Datastore mode key
  - RPC API
      - field name: `  key_value  `
      - type: a `  Key  ` message
  - Sort order: By path elements (kind, identifier, kind, identifier...)

### Null

  - REST API
      - field name: `  nullValue  `
      - type: null
  - RPC API
      - field name: `  null_value  `
      - type: `  NullValue  `
  - Sort order: None

### Text string

  - REST API
      - field name: `  stringValue  `
      - type: string
  - RPC API
      - field name: `  string_value  `
      - type: `  string  `
  - Sort order: UTF-8 encoded byte order
  - Notes: Up to 1,500 bytes if property is indexed, up to 1,048,487 bytes (1 MiB - 89 bytes) otherwise.

## Value type ordering

When a query involves a property with values of mixed types, a Datastore mode database uses a deterministic ordering based on the internal representations. The following list shows the order:

1.  Null values
2.  Fixed-point numbers
      - Integers
      - Dates and times
3.  Boolean values
4.  Byte strings
5.  Unicode strings
6.  Floating-point numbers
7.  NaN values
8.  Geographical points
9.  Datastore mode keys

**Note:** Integers and floating-point numbers are considered separate types in Datastore mode. If an entity uses a mix of integers and floats for the same property, all integers will be sorted before all floats, for example: `  7  ` \< `  3.2  ` .
