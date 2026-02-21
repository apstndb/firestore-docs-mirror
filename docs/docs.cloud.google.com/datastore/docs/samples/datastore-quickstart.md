Save an entity.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore mode client libraries](/datastore/docs/reference/libraries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Datastore.V1;

namespace GoogleCloudSamples
{
    public class QuickStart
    {
        public static void Main(string[] args)
        {
            // Your Google Cloud Platform project ID
            string projectId = "YOUR-PROJECT-ID";

            // Instantiates a client
            DatastoreDb db = DatastoreDb.Create(projectId);

            // The kind for the new entity
            string kind = "Task";
            // The name/ID for the new entity
            string name = "sampletask1";
            KeyFactory keyFactory = db.CreateKeyFactory(kind);
            // The Cloud Datastore key for the new entity
            Key key = keyFactory.CreateKey(name);

            var task = new Entity
            {
                Key = key,
                ["description"] = "Buy milk"
            };
            using (DatastoreTransaction transaction = db.BeginTransaction())
            {
                // Saves the task
                transaction.Upsert(task);
                transaction.Commit();

                Console.WriteLine($"Saved {task.Key.Path[0].Name}: {(string)task["description"]}");
            }
        }
    }
}
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// Sample datastore-quickstart fetches an entity from Google Cloud Datastore.
package main

import (
 "context"
 "fmt"
 "log"

 "cloud.google.com/go/datastore"
)

type Task struct {
 Description string
}

func main() {
 ctx := context.Background()

 // Set your Google Cloud Platform project ID.
 projectID := "YOUR_PROJECT_ID"

 // Creates a client.
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Failed to create client: %v", err)
 }
 defer client.Close()

 // Sets the kind for the new entity.
 kind := "Task"
 // Sets the name/ID for the new entity.
 name := "sampletask1"
 // Creates a Key instance.
 taskKey := datastore.NameKey(kind, name, nil)

 // Creates a Task instance.
 task := Task{
     Description: "Buy milk",
 }

 // Saves the new entity.
 if _, err := client.Put(ctx, taskKey, &task); err != nil {
     log.Fatalf("Failed to save task: %v", err)
 }

 fmt.Printf("Saved %v: %v\n", taskKey, task.Description)
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Imports the Google Cloud client library
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.Key;

public class QuickstartSample {
  public static void main(String... args) throws Exception {
    // Instantiates a client
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

    // The kind for the new entity
    String kind = "Task";
    // The name/ID for the new entity
    String name = "sampletask1";
    // The Cloud Datastore key for the new entity
    Key taskKey = datastore.newKeyFactory().setKind(kind).newKey(name);

    // Prepares the new entity
    Entity task = Entity.newBuilder(taskKey).set("description", "Buy milk").build();

    // Saves the entity
    datastore.put(task);

    System.out.printf("Saved %s: %s%n", task.getKey().getName(), task.getString("description"));

    // Retrieve entity
    Entity retrieved = datastore.get(taskKey);

    System.out.printf("Retrieved %s: %s%n", taskKey.getName(), retrieved.getString("description"));
  }
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Imports the Google Cloud client library
const {Datastore} = require('@google-cloud/datastore');

// Creates a client
const datastore = new Datastore();

async function quickstart() {
  // The kind for the new entity
  const kind = 'Task';

  // The name/ID for the new entity
  const name = 'sampletask1';

  // The Cloud Datastore key for the new entity
  const taskKey = datastore.key([kind, name]);

  // Prepares the new entity
  const task = {
    key: taskKey,
    data: {
      description: 'Buy milk',
    },
  };

  // Saves the entity
  await datastore.save(task);
  console.log(`Saved ${task.key.name}: ${task.data.description}`);
}
quickstart();
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
# Includes the autoloader for libraries installed with composer
require __DIR__ . '/vendor/autoload.php';

# Imports the Google Cloud client library
use Google\Cloud\Datastore\DatastoreClient;

# Your Google Cloud Platform project ID
$projectId = 'YOUR_PROJECT_ID';

# Instantiates a client
$datastore = new DatastoreClient([
    'projectId' => $projectId
]);

# The kind for the new entity
$kind = 'Task';

# The name/ID for the new entity
$name = 'sampletask1';

# The Cloud Datastore key for the new entity
$taskKey = $datastore->key($kind, $name);

# Prepares the new entity
$task = $datastore->entity($taskKey, ['description' => 'Buy milk']);

# Saves the entity
$datastore->upsert($task);

echo 'Saved ' . $task->key() . ': ' . $task['description'] . PHP_EOL;
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# Imports the Google Cloud client library
from google.cloud import datastore

# Instantiates a client
datastore_client = datastore.Client()

# The kind for the new entity
kind = "Task"
# The name/ID for the new entity
name = "sampletask1"
# The Cloud Datastore key for the new entity
task_key = datastore_client.key(kind, name)

# Prepares the new entity
task = datastore.Entity(key=task_key)
task["description"] = "Buy milk"

# Saves the entity
datastore_client.put(task)

print(f"Saved {task.key.name}: {task['description']}")
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
# Imports the Google Cloud client library
require "google/cloud/datastore"

# Instantiate a client
datastore = Google::Cloud::Datastore.new

# The kind for the new entity
kind = "Task"
# The name/ID for the new entity
# task_name = "sampleTask"
# The Cloud Datastore key for the new entity
task_key = datastore.key kind, task_name

# Prepares the new entity
task = datastore.entity task_key do |t|
  t["description"] = "Buy milk"
end

# Saves the entity
datastore.save task

puts "Saved #{task.key.name}: #{task['description']}"
task_key = datastore.find task_key
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
