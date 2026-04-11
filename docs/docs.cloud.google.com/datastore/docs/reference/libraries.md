This page shows how to get started with the Cloud Client Libraries for the Datastore API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](https://docs.cloud.google.com/apis/docs/client-libraries-explained) .

<span id="installing_the_client_library"></span>

## Install the client library

### C\#

``` notranslate
Install-Package Google.Cloud.Datastore.V1
```

For more information, see [Setting Up a C\# Development Environment](https://docs.cloud.google.com/dotnet/docs/setup) .

### Go

``` notranslate
go get cloud.google.com/go/datastore
```

For more information, see [Setting Up a Go Development Environment](https://docs.cloud.google.com/go/docs/setup) .

### Java

If you are using [Maven](https://maven.apache.org/) , add the following to your `pom.xml` file. For more information about BOMs, see [The Google Cloud Platform Libraries BOM](https://cloud.google.com/java/docs/bom) .

    <dependencyManagement>
      <dependencies>
        <dependency>
          <groupId>com.google.cloud</groupId>
          <artifactId>libraries-bom</artifactId>
          <version>26.62.0</version>
          <type>pom</type>
          <scope>import</scope>
        </dependency>
      </dependencies>
    </dependencyManagement>
    
    <dependencies>
      <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>google-cloud-datastore</artifactId>
      </dependency>

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

    implementation platform('com.google.cloud:libraries-bom:26.74.0')
    
    implementation 'com.google.cloud:google-cloud-datastore'

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

    libraryDependencies += "com.google.cloud" % "google-cloud-datastore" % "2.34.0"

If you're using Visual Studio Code or IntelliJ, you can add client libraries to your project using the following IDE plugins:

  - [Cloud Code for VS Code](https://docs.cloud.google.com/code/docs/vscode/client-libraries)
  - [Cloud Code for IntelliJ](https://docs.cloud.google.com/code/docs/intellij/client-libraries)

The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

**Note:** Cloud Java client libraries do not currently support Android.

For more information, see [Setting Up a Java Development Environment](https://docs.cloud.google.com/java/docs/setup) .

### Node.js

``` notranslate
npm install @google-cloud/datastore
```

For more information, see [Setting Up a Node.js Development Environment](https://docs.cloud.google.com/nodejs/docs/setup) .

### PHP

``` notranslate
composer require google/cloud-datastore
```

For more information, see [Using PHP on Google Cloud](https://docs.cloud.google.com/php/docs) .

### Python

``` notranslate
pip install --upgrade google-cloud-datastore
```

For more information, see [Setting Up a Python Development Environment](https://docs.cloud.google.com/python/docs/setup) .

### Ruby

``` notranslate
gem install google-cloud-datastore
```

For more information, see [Setting Up a Ruby Development Environment](https://docs.cloud.google.com/ruby/docs/setup) .

<span id="setting_up_authentication"></span>

## Set up authentication

To authenticate calls to Google Cloud APIs, client libraries support [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) ; the libraries look for credentials in a set of defined locations and use those credentials to authenticate requests to the API. With ADC, you can make credentials available to your application in a variety of environments, such as local development or production, without needing to modify your application code.

For production environments, the way you set up ADC depends on the service and context. For more information, see [Set up Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc) .

For a local development environment, you can set up ADC with the credentials that are associated with your Google Account:

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the Google Cloud CLI by running the following command:
    
        gcloud init
    
    If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

2.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .
    
    A sign-in screen appears. After you sign in, your credentials are stored in the [local credential file used by ADC](https://docs.cloud.google.com/docs/authentication/application-default-credentials#personal) .

<span id="using_the_client_library"></span>

## Use the client library

The following example shows how to use the client library.

### C\#

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

### Go

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

### Java

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

### Node.js

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

### PHP

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

### Python

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

### Ruby

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

<span id="additional_resources"></span>

## Additional resources

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-datastore/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-datastore)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://cloud.google.com/nodejs/docs/reference/datastore/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/nodejs-datastore/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/nodejs-datastore)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](https://cloud.google.com/python/docs/reference/datastore/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/python-datastore/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/python-datastore)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`google-cloud-datastore` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-cloud-datastore%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)

### Dependency on App Engine application

See [App Engine Requirement](https://docs.cloud.google.com/firestore/docs/app-engine-requirement) .

### Google App Engine Standard Environment Client Libraries

Integrate Firestore in Datastore mode with your App Engine Standard Environment applications by using the App Engine client libraries.

| Language | Library                                                                                                                                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Go       | [Google App Engine SDK for Go](https://cloud.google.com/appengine/docs/go/datastore/)                                                                                                                                                                               |
| Java     | [Google App Engine SDK for Java](https://cloud.google.com/appengine/docs/java/datastore/)                                                                                                                                                                           |
| Python 3 | [Google Cloud Datastore client library](https://docs.cloud.google.com/datastore/docs/reference/libraries#installing_the_client_library) or the [Google Cloud NDB Client Library](https://cloud.google.com/appengine/docs/standard/python3/migrating-to-cloud-ndb) . |
| Python 2 | [Google Cloud NDB Client Library](https://cloud.google.com/appengine/docs/standard/python3/migrating-to-cloud-ndb)                                                                                                                                                  |

**Warning:** For App Engine applications that are written in Python 2, the Google Datastore DB Client Library and the App Engine NDB Library are no longer recommended; use the Google Cloud NDB Client Library instead. See [Migrating to Cloud NDB](https://docs.cloud.google.com/appengine/docs/standard/python3/migrating-to-cloud-ndb) .

<span id="third-party_client_libraries"></span>

## Third-party Datastore API client libraries

In addition to the Google-supported client libraries listed in the tables above, a set of third-party libraries are available.

| Language | Library                                                           |
| -------- | ----------------------------------------------------------------- |
| Java     | [Objectify](https://github.com/objectify/objectify)               |
| PHP      | [Datastore Library for PHP](https://github.com/tomwalder/php-gds) |
