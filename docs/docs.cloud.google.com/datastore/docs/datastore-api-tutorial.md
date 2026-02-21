This page provides a short exercise in building a command-line TaskList application with the Firestore in Datastore mode API. The TaskList application stores, lists, updates, and removes tasks.

## Prerequisites

1.  **Ability to write and run a command line application in the programming languages used in this topic**  
    In addition to a basic understanding of how to develop applications, you should be able to download and install additional libraries before attempting this tutorial.
2.  **A Google Cloud project with the Datastore mode API enabled**  
    Applications that use Datastore mode are associated with a [Google Cloud](https://console.cloud.google.com/) project with the Datastore mode API enabled. This project provides authentication credentials you use in your application to identify it to Google and authorize its use of the Datastore mode API.  
    Follow [these instructions](/apis/docs/getting-started) to create a project, enable the Datastore mode API for it, and set up your local development environment with authentication credentials using the `  gcloud auth login  ` command. Make a note of the project's ID, which you'll use later on.

## Installation and setup

Install client libraries and configure any additional settings for your development environment.

### C\#

1.  Ensure you have [Visual Studio](https://www.visualstudio.com/) (version 2013 or later) installed.

2.  Download the TaskList sample application from [the samples repository](https://github.com/GoogleCloudPlatform/dotnet-docs-samples/archive/master.zip) .

3.  Extract the files from the zip into a directory in your *Documents* folder.

4.  In Visual Studio, open the file `  dotnet-docs-samples-master\datastore\api\Datastore.sln  ` .

5.  In Visual Studio's **Solution Explorer** window, right-click the **TaskList** project and choose **Set as StartUp Project** .

6.  Right-click the **TaskList** project again and choose **Properties** .

7.  In the **Properties** window, click **Debug** and type the ID of your Google Cloud project into the **Command line arguments:** box.

8.  Click **File** and then click **Save** to save your changes.

9.  Run the application\! Press **F5** on your keyboard.

### Go

1.  Clone the TaskList sample application.
    
    ``` text
    go get github.com/GoogleCloudPlatform/golang-samples/datastore/tasks
    ```

2.  Change directories to where you cloned the sample:
    
    ``` text
    cd $GOPATH/src/github.com/GoogleCloudPlatform/golang-samples/datastore/tasks
    ```

3.  At a command prompt, run the following, where `  <project-id>  ` is the ID of your Google Cloud project.
    
    ``` text
    export DATASTORE_PROJECT_ID=<project-id>
    ```
    
    (Windows users: use `  set  ` instead of `  export  ` .)

4.  Run the application\!
    
    ``` text
    go run tasks.go
    ```

### Java

1.  Ensure you have [Maven](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) and [Java](http://java.com/en/download/faq/develop.xml) (version 8 or later) installed.

2.  Download the TaskList sample application from [the samples repository](https://github.com/googleapis/java-datastore/archive/main.zip) .

3.  At a command prompt, extract the download:
    
    ``` text
    unzip main.zip
    ```

4.  Change directories to the TaskList application:
    
    ``` text
    cd java-datastore-main/samples/snippets
    ```

5.  Run the following, where `  <project-id>  ` is the ID of your Google Cloud project.
    
    ``` text
    gcloud config set project <project-id>
    ```

6.  Compile and run the application\!
    
    ``` text
    mvn clean compile
    mvn exec:java -Dexec.mainClass="com.google.datastore.snippets.TaskList"
    ```

### Node.js

1.  [Prepare your environment for Node.js development](/nodejs/docs/setup) .

2.  Download the TaskList sample application from [the samples repository](https://github.com/googleapis/nodejs-datastore/archive/master.zip) .

3.  Extract the download:
    
    ``` text
    unzip master.zip
    ```

4.  Change directories to the TaskList application:
    
    ``` text
    cd nodejs-datastore-master/samples
    ```

5.  Install the dependencies and link the application:
    
    ``` text
    npm install
    ```

6.  At a command prompt, run the following, where `  <project-id>  ` is the ID of your Google Cloud project.
    
    ``` text
    export GCLOUD_PROJECT=<project-id>
    ```
    
    (Windows users: use `  set  ` instead of `  export  ` .)

7.  Run the application\!
    
    ``` text
    node tasks.js
    ```

### PHP

1.  Ensure you have [PHP](http://php.net/downloads.php) (version 5.6 or later) and [Composer](https://getcomposer.org/) installed.

2.  Download the TaskList sample application from [the samples repository](https://github.com/GoogleCloudPlatform/php-docs-samples/archive/master.zip) .

3.  Extract the download:
    
    ``` text
    unzip master.zip
    ```

4.  Change directories to the TaskList application:
    
    ``` text
    cd php-docs-samples-master/datastore/tutorial
    ```

5.  Install dependencies.
    
    ``` text
    composer install
    ```

6.  Run the application\!
    
    ``` text
    php src/list_tasks.php
    ```

### Python

1.  Ensure you have [Python](https://www.python.org/downloads/) (version 2.7.9 or later), [pip](https://pip.pypa.io/en/latest/installing/) , and [virtualenv](http://docs.python-guide.org/en/latest/dev/virtualenvs/) installed.

2.  Activate a `  virtualenv  ` session.
    
    ``` text
    virtualenv venv
    source venv/bin/activate
    ```

3.  Download the TaskList sample application from [the samples repository](https://github.com/GoogleCloudPlatform/python-docs-samples/archive/master.zip) .

4.  Extract the download:
    
    ``` text
    unzip master.zip
    ```

5.  Change directories to the TaskList application:
    
    ``` text
    cd python-docs-samples-master/datastore/cloud-client
    ```

6.  Install dependencies:
    
    ``` text
    pip install -r requirements.txt
    ```

7.  Run the application\! Use the ID of your Google Cloud project for `  <project-id>  ` .
    
    ``` text
    python tasks.py new project-id
    ```

### Ruby

1.  Ensure you have [Ruby](https://www.ruby-lang.org/) and [Bundler](http://bundler.io/) installed.

2.  Download the TaskList sample application from [the samples repository](https://github.com/googleapis/google-cloud-ruby/archive/master.zip) .

3.  Extract the download:
    
    ``` text
    unzip master.zip
    ```

4.  Change directories to the TaskList application:
    
    ``` text
    cd google-cloud-ruby-master/google-cloud-datastore/samples
    ```

5.  Install the dependencies:
    
    ``` text
    bundle install
    ```

6.  At a command prompt, run the following, where `  <project-id>  ` is the ID of your Google Cloud project.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=<project-id>
    ```
    
    (Windows users: use `  set  ` instead of `  export  ` .)

7.  Run the application\!
    
    ``` text
    bundle exec ruby tasks.rb
    ```

## Creating an Authorized Service Object

In order to make authenticated requests to Google Cloud APIs using the Google APIs Client libraries, you must:

  - Fetch the credential to use for requests.
  - Create a service object that uses that credential.

You can then make API calls by calling methods on the Datastore mode service object.

For this example, you'll fetch [Application Default Credentials](https://developers.google.com/identity/protocols/application-default-credentials) from the environment, and pass it as an argument to create the service object.

Here's the call to create the authorized Datastore mode service object:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
// Create an authorized Datastore service using Application Default Credentials.
_db = DatastoreDb.Create(projectId);
// Create a Key factory to construct keys associated with this project.
_keyFactory = _db.CreateKeyFactory("Task");
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/datastore"
)

func createClient(projectID string) (*datastore.Client, error) {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }
 // Note: call the following from main() to ensure the client
 // properly frees all resources.
 // defer client.Close()
 return client, nil
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
// Create an authorized Datastore service using Application Default Credentials.
private final Datastore datastore = DatastoreOptions.getDefaultInstance().getService();

// Create a Key factory to construct keys associated with this project.
private final KeyFactory keyFactory = datastore.newKeyFactory().setKind("Task");
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// By default, the client will authenticate using the service account file
// specified by the GOOGLE_APPLICATION_CREDENTIALS environment variable and use
// the project specified by the GCLOUD_PROJECT environment variable. See
// https://googlecloudplatform.github.io/google-cloud-node/#/docs/datastore/latest/guides/authentication
const {Datastore} = require('@google-cloud/datastore');

// Creates a client
const datastore = new Datastore();
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Create a Cloud Datastore client.
 *
 * @param string $projectId The Google Cloud project ID.
 */
function build_service(string $projectId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);
    return $datastore;
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def create_client(project_id):
    return datastore.Client(project_id)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/datastore"

datastore = Google::Cloud::Datastore.new
```

## Storing data

Objects in Datastore mode are known as *entities* , and each entity is of a particular *kind* . The TaskList application will store entities of kind `  Task  ` , with the following properties:

  - `  description  ` : a string specified by the user as the task description
  - `  created  ` : a date that shows when the task was initially created
  - `  done  ` : a boolean that indicates whether the task has been completed

When the user adds a new task, the TaskList application creates a `  Task  ` entity with values for the properties previously listed:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
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
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

For this application, we also provide a method to update the `  done  ` property, to indicate the task is complete:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def mark_done task_id
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  task = datastore.find "Task", task_id

  task["done"] = true

  datastore.save task
end
```

Here's the method to delete a `  Task  ` entity, using the `  Task  ` entity's key:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
/// <summary>
/// Deletes a task entity.
/// </summary>
/// <param name="id">The ID of the task entity as given by Key.</param>
void DeleteTask(long id)
{
    _db.Delete(_keyFactory.CreateKey(id));
}
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
import (
 "context"
 "log"

 "cloud.google.com/go/datastore"
)

// DeleteTask deletes the task with the given ID.
func DeleteTask(projectID string, taskID int64) error {
 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     log.Fatalf("Could not create datastore client: %v", err)
 }
 return client.Delete(ctx, datastore.IDKey("Task", taskID, nil))
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
/**
 * Deletes a task entity.
 *
 * @param id The ID of the task entity as given by {@link Key#id()}
 * @throws DatastoreException if the delete fails
 */
void deleteTask(long id) {
  datastore.delete(keyFactory.newKey(id));
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function deleteTask(taskId) {
  const taskKey = datastore.key(['Task', datastore.int(taskId)]);

  await datastore.delete(taskKey);
  console.log(`Task ${taskId} deleted successfully.`);
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
use Google\Cloud\Datastore\DatastoreClient;

/**
 * Delete a task with a given id.
 *
 * @param string $projectId The Google Cloud project ID.
 * @param string $taskId
 */
function delete_task(string $projectId, string $taskId)
{
    $datastore = new DatastoreClient(['projectId' => $projectId]);

    $taskKey = $datastore->key('Task', $taskId);
    $datastore->delete($taskKey);

    printf('Task %d deleted successfully.' . PHP_EOL, $taskId);
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def delete_task(client: datastore.Client, task_id: str | int):
    # Create a key for an entity of kind "Task", and with the supplied
    # `task_id` as its Id
    key = client.key("Task", task_id)
    # Use that key to delete its associated document, if it exists
    client.delete(key)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
def delete_task task_id
  require "google/cloud/datastore"

  datastore = Google::Cloud::Datastore.new

  task = datastore.find "Task", task_id

  datastore.delete task
end
```

## Running a query

In addition to retrieving entities from Datastore mode directly by their keys, an application can perform a *query* to retrieve them by the values of their properties. A typical query includes the following:

  - An entity kind to which the query applies
  - Zero or more filters, for example to select kinds whose properties match a value
  - Zero or more sort orders, to sequence the results

For this application, we'll query Datastore mode for `  Task  ` entities sorted by creation time:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

def list_tasks(client: datastore.Client):
    # Create a query against all of your objects of kind "Task"
    query = client.query(kind="Task")
    query.order = ["created"]

    return list(query.fetch())
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

**Note:** You can also query using the SQL-like [GQL](/datastore/docs/reference/gql_reference) .

## Next Steps

This tutorial covers only the most basic steps necessary to make calls to the Datastore mode API from a command-line application. Datastore mode supports fast and highly scalable ACID transactions, SQL-like queries, indexes and more.

  - For a deeper look into the Datastore mode capabilities, see [What is Firestore in Datastore mode?](/datastore/docs/concepts/overview) .
  - For information about using the Datastore mode emulator while you develop your application, see [Datastore mode Emulator](/datastore/docs/tools/datastore-emulator) .
