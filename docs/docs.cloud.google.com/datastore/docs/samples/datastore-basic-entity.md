Create a basic entity.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Entities, Properties, and Keys](https://docs.cloud.google.com/datastore/docs/concepts/entities)
  - [Structuring Data for Strong Consistency](https://docs.cloud.google.com/datastore/docs/concepts/structuring_for_strong_consistency)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Entity task = new Entity()
    {
        Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
        ["category"] = "Personal",
        ["done"] = false,
        ["priority"] = 4,
        ["description"] = "Learn Cloud Datastore"
    };

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Key taskKey = datastore.newKeyFactory().setKind("Task").newKey("sampleTask");
    Entity task =
        Entity.newBuilder(taskKey)
            .set("category", "Personal")
            .set("done", false)
            .set("priority", 4)
            .set("description", "Learn Cloud Datastore")
            .build();

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const task = {
      category: 'Personal',
      done: false,
      priority: 4,
      description: 'Learn Cloud Datastore',
    };

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $task = $datastore->entity('Task', [
        'category' => 'Personal',
        'done' => false,
        'priority' => 4,
        'description' => 'Learn Cloud Datastore'
    ]);

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    task = datastore.entity "Task" do |t|
      t["category"] = "Personal"
      t["done"] = false
      t["priority"] = 4
      t["description"] = "Learn Cloud Datastore"
    end

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
