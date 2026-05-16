---
name: documents/docs.cloud.google.com/datastore/docs/samples/datastore-add-entity
uri: https://docs.cloud.google.com/datastore/docs/samples/datastore-add-entity
title: Add task
description: Creates and saves an Entity of the hypothetical type &#34;Task&#34;
data_source: docs.cloud.google.com
---

Creates and saves an Entity of the hypothetical type "Task"

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Getting started with the Firestore in Datastore mode API](https://docs.cloud.google.com/datastore/docs/datastore-api-tutorial)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import (
     "context"
     "log"
     "time"
    
     "cloud.google.com/go/datastore"
    )
    
    // Task is the model used to store tasks in the datastore.
    type Task struct {
     Desc    string    `datastore:"description"`
     Created time.Time `datastore:"created"`
     Done    bool      `datastore:"done"`
     id      int64     // The integer ID used in the datastore.
    }
    
    // AddTask adds a task with the given description to the datastore,
    // returning the key of the newly created entity.
    func AddTask(projectID string, desc string) (*datastore.Key, error) {
     ctx := context.Background()
     client, err := datastore.NewClient(ctx, projectID)
     if err != nil {
         log.Fatalf("Could not create datastore client: %v", err)
     }
     defer client.Close()
     task := &Task{
         Desc:    desc,
         Created: time.Now(),
     }
     key := datastore.IncompleteKey("Task", nil)
     return client.Put(ctx, key, task)
    
    }

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
