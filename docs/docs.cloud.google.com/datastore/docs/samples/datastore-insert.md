Perform an insert.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Entities, Properties, and Keys](https://docs.cloud.google.com/datastore/docs/concepts/entities)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Entity task = new Entity()
    {
        Key = _keyFactory.CreateIncompleteKey()
    };
    task.Key = _db.Insert(task);

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Key taskKey = datastore.add(FullEntity.newBuilder(keyFactory.newKey()).build()).getKey();

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $task = $datastore->entity('Task', [
        'category' => 'Personal',
        'done' => false,
        'priority' => 4,
        'description' => 'Learn Cloud Datastore'
    ]);
    $datastore->insert($task);

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    datastore.transaction do |_tx|
      task = datastore.entity "Task" do |t|
        t["category"] = "Personal"
        t["done"] = false
        t["priority"] = 4
        t["description"] = "Learn Cloud Datastore"
      end
      datastore.save task
    end

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
