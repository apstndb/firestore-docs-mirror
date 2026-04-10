# Create a Firestore database by using a server client library

This quickstart shows you how to set up Firestore, add data, and read data by using the C\#, Go, Java, Node.js, PHP, Python, or Ruby server client library.

## Before you begin

**Firestore and App Engine:** You can't use both Firestore and Datastore in the same project, which might affect apps using App Engine. Try using Firestore with a different project if you need to use Datastore.

## Create a Firestore in Native Mode in Native mode database

If this is a new project, you need to create a Firestore database instance.

1.  [Go to the Firestore viewer](https://console.cloud.google.com/firestore/data) .

2.  From the ***Select a database service*** screen, choose *Firestore in Native mode* .

3.  Select a [location](https://docs.cloud.google.com/firestore/docs/locations#types) for your Firestore.
    
    If you aren't able to select a location, then your project's ["location for default Google Cloud resources"](https://docs.cloud.google.com/firestore/docs/locations#default-cloud-location) has already been set. Some of your project's resources (like the default Firestore instance) share a common location dependency, and their location can be set either during project creation or when setting up another service that shares this location dependency.

4.  Click **Create Database** .

When you create a Firestore project, it also enables the API in the [Cloud API Manager](https://console.cloud.google.com/projectselector/apis/api/firestore.googleapis.com/overview) .

## Set up authentication

To run the client library, you must first set up [authentication](https://docs.cloud.google.com/docs/authentication/production) by creating a service account and setting an environment variable.

## Add the server client library to your app

Add the required dependencies and client libraries to your app.

##### Java

Add the Firestore Java library to your app:

  - **Using Maven:**
    
        <dependencyManagement>
          <dependencies>
            <dependency>
              <groupId>com.google.cloud</groupId>
              <artifactId>libraries-bom</artifactId>
              <version>26.65.0</version>
              <type>pom</type>
              <scope>import</scope>
            </dependency>
          </dependencies>
        </dependencyManagement>
        
        <dependencies>
          <dependency>
            <groupId>com.google.cloud</groupId>
            <artifactId>google-cloud-firestore</artifactId>
          </dependency>pom.xml

  - If you are using Gradle or setting up without BOM, see the [Firestore Client for Java README.](https://github.com/googleapis/java-firestore/tree/main#quickstart)

<!-- end list -->

  - **Using an IDE:**
    
    If you're using VS Code, IntelliJ, or Eclipse, you can add client libraries to your project using these IDE plugins:
    
      - [Cloud Code for VS Code](https://docs.cloud.google.com/code/docs/vscode/client-libraries)
      - [Cloud Code for IntelliJ](https://docs.cloud.google.com/code/docs/intellij/client-libraries)
      - [Cloud Tools for Eclipse](https://docs.cloud.google.com/eclipse/docs/libraries)
    
    The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

##### Python

Add the Firestore Python library to your app:

**Note:** We recommend that you use a [virtual Python environment](https://virtualenv.pypa.io/en/stable/) to install the Firestore Python library:

    pip install virtualenv
    virtualenv env
    source env/bin/activate

    pip install --upgrade google-cloud-firestore

##### Node.js

Add the Firestore Node.js library to your app:

    npm install --save @google-cloud/firestore

##### Go

Install the Firestore Go library:

    go get cloud.google.com/go/firestore

Add the Firestore Go library to your app:

    import "cloud.google.com/go/firestore"

##### PHP

1.  Install and enable the [gRPC extension](https://docs.cloud.google.com/php/docs/reference/help/grpc) for PHP, which you will need to use the client library.

2.  Add the Firestore PHP library to your app:
    
        composer require google/cloud-firestore

##### C\#

1.  Add the Firestore C\# library to your app in your `  .csproj  ` file:
    
        <ItemGroup>
          <PackageReference Include="Google.Cloud.Firestore" Version="1.1.0-beta01" />
        </ItemGroup>

2.  Add the following to your `  Program.cs  ` file:
    
        using Google.Cloud.Firestore;

##### Ruby

1.  Add the Firestore Ruby library to your app in your `  Gemfile  ` :
    
        gem "google-cloud-firestore"

2.  Install dependencies from your `  Gemfile  ` using:
    
        bundle install

## Initialize Firestore in Native Mode

Initialize an instance of Firestore:

##### Java

    import com.google.cloud.firestore.Firestore;
    import com.google.cloud.firestore.FirestoreOptions;

    FirestoreOptions firestoreOptions =
        FirestoreOptions.getDefaultInstance().toBuilder()
            .setProjectId(projectId)
            .setCredentials(GoogleCredentials.getApplicationDefault())
            .build();
    Firestore db = firestoreOptions.getService();Quickstart.java

##### Python

    from google.cloud import firestore
    
    # The `project` parameter is optional and represents which project the client
    # will act on behalf of. If not supplied, the client falls back to the default
    # project inferred from the environment.
    db = firestore.Client(project="my-project-id")snippets.py

##### Python  
(Async)

    from google.cloud import firestore
    
    # The `project` parameter is optional and represents which project the client
    # will act on behalf of. If not supplied, the client falls back to the default
    # project inferred from the environment.
    db = firestore.AsyncClient(project="my-project-id")snippets.py

##### Node.js

    const Firestore = require('@google-cloud/firestore');
    
    const db = new Firestore({
      projectId: 'YOUR_PROJECT_ID',
      keyFilename: '/path/to/keyfile.json',
    });

##### Go

    import (
     "context"
     "flag"
     "fmt"
     "log"
    
     "google.golang.org/api/iterator"
    
     "cloud.google.com/go/firestore"
    )
    
    func createClient(ctx context.Context) *firestore.Client {
     // Sets your Google Cloud Platform project ID.
     projectID := "YOUR_PROJECT_ID"
    
     client, err := firestore.NewClient(ctx, projectID)
     if err != nil {
         log.Fatalf("Failed to create client: %v", err)
     }
     // Close client when done with
     // defer client.Close()
     return client
    }
    main.go

##### PHP

    use Google\Cloud\Firestore\FirestoreClient;
    
    /**
     * Initialize Cloud Firestore with default project ID.
     */
    function setup_client_create(string $projectId = null)
    {
        // Create the Cloud Firestore client
        if (empty($projectId)) {
            // The `projectId` parameter is optional and represents which project the
            // client will act on behalf of. If not supplied, the client falls back to
            // the default project inferred from the environment.
            $db = new FirestoreClient();
            printf('Created Cloud Firestore client with default project ID.' . PHP_EOL);
        } else {
            $db = new FirestoreClient([
                'projectId' => $projectId,
            ]);
            printf('Created Cloud Firestore client with project ID: %s' . PHP_EOL, $projectId);
        }
    }setup_client_create.php

##### C\#

    FirestoreDb db = FirestoreDb.Create(project);
    Console.WriteLine("Created Cloud Firestore client with project ID: {0}", project);Program.cs

##### Ruby

    require "google/cloud/firestore"
    
    # The `project_id` parameter is optional and represents which project the
    # client will act on behalf of. If not supplied, the client falls back to the
    # default project inferred from the environment.
    firestore = Google::Cloud::Firestore.new project_id: project_id
    
    puts "Created Cloud Firestore client with given project ID."quickstart.rb

## Add data

Firestore stores data in Documents, which are stored in Collections. Firestore creates collections and documents implicitly the first time you add data to the document. You do not need to explicitly create collections or documents.

Create a new collection and a document using the following example code.

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.collection("users").document("alovelace");
    // Add document data  with id "alovelace" using a hashmap
    Map<String, Object> data = new HashMap<>();
    data.put("first", "Ada");
    data.put("last", "Lovelace");
    data.put("born", 1815);
    //asynchronously write data
    ApiFuture<WriteResult> result = docRef.set(data);
    // ...
    // result.get() blocks on response
    System.out.println("Update time : " + result.get().getUpdateTime());

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = db.collection("users").document("alovelace")
    doc_ref.set({"first": "Ada", "last": "Lovelace", "born": 1815})

### Python  
(Async)

    doc_ref = db.collection("users").document("alovelace")
    await doc_ref.set({"first": "Ada", "last": "Lovelace", "born": 1815})

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const docRef = db.collection('users').doc('alovelace');
    
    await docRef.set({
      first: 'Ada',
      last: 'Lovelace',
      born: 1815
    });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    _, _, err := client.Collection("users").Add(ctx, map[string]interface{}{
     "first": "Ada",
     "last":  "Lovelace",
     "born":  1815,
    })
    if err != nil {
     log.Fatalf("Failed adding alovelace: %v", err)
    }

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $docRef = $db->collection('samples/php/users')->document('alovelace');
    $docRef->set([
        'first' => 'Ada',
        'last' => 'Lovelace',
        'born' => 1815
    ]);
    printf('Added data to the lovelace document in the users collection.' . PHP_EOL);

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.Collection("users").Document("alovelace");
    Dictionary<string, object> user = new Dictionary<string, object>
    {
        { "First", "Ada" },
        { "Last", "Lovelace" },
        { "Born", 1815 }
    };
    await docRef.SetAsync(user);

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = firestore.doc "#{collection_path}/alovelace"
    
    doc_ref.set(
      {
        first: "Ada",
        last:  "Lovelace",
        born:  1815
      }
    )
    
    puts "Added data to the alovelace document in the users collection."

Now add another document to the `  users  ` collection. Notice that this document includes a key-value pair (middle name) that does not appear in the first document. Documents in a collection can contain different sets of information.

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.collection("users").document("aturing");
    // Add document data with an additional field ("middle")
    Map<String, Object> data = new HashMap<>();
    data.put("first", "Alan");
    data.put("middle", "Mathison");
    data.put("last", "Turing");
    data.put("born", 1912);
    
    ApiFuture<WriteResult> result = docRef.set(data);
    System.out.println("Update time : " + result.get().getUpdateTime());

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = db.collection("users").document("aturing")
    doc_ref.set({"first": "Alan", "middle": "Mathison", "last": "Turing", "born": 1912})

### Python  
(Async)

    doc_ref = db.collection("users").document("aturing")
    await doc_ref.set(
        {"first": "Alan", "middle": "Mathison", "last": "Turing", "born": 1912}
    )

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const aTuringRef = db.collection('users').doc('aturing');
    
    await aTuringRef.set({
      'first': 'Alan',
      'middle': 'Mathison',
      'last': 'Turing',
      'born': 1912
    });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    _, _, err = client.Collection("users").Add(ctx, map[string]interface{}{
     "first":  "Alan",
     "middle": "Mathison",
     "last":   "Turing",
     "born":   1912,
    })
    if err != nil {
     log.Fatalf("Failed adding aturing: %v", err)
    }

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $docRef = $db->collection('samples/php/users')->document('aturing');
    $docRef->set([
        'first' => 'Alan',
        'middle' => 'Mathison',
        'last' => 'Turing',
        'born' => 1912
    ]);
    printf('Added data to the aturing document in the users collection.' . PHP_EOL);

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    DocumentReference docRef = db.Collection("users").Document("aturing");
    Dictionary<string, object> user = new Dictionary<string, object>
    {
        { "First", "Alan" },
        { "Middle", "Mathison" },
        { "Last", "Turing" },
        { "Born", 1912 }
    };
    await docRef.SetAsync(user);

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    doc_ref = firestore.doc "#{collection_path}/aturing"
    
    doc_ref.set(
      {
        first:  "Alan",
        middle: "Mathison",
        last:   "Turing",
        born:   1912
      }
    )
    
    puts "Added data to the aturing document in the users collection."

## Read data

To quickly verify that you've added data to Firestore, use the data viewer in the [Firebase console](https://console.firebase.google.com/project/_/firestore/data) .

You can also use the `  get  ` method to retrieve the entire collection.

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    // asynchronously retrieve all users
    ApiFuture<QuerySnapshot> query = db.collection("users").get();
    // ...
    // query.get() blocks on response
    QuerySnapshot querySnapshot = query.get();
    List<QueryDocumentSnapshot> documents = querySnapshot.getDocuments();
    for (QueryDocumentSnapshot document : documents) {
      System.out.println("User: " + document.getId());
      System.out.println("First: " + document.getString("first"));
      if (document.contains("middle")) {
        System.out.println("Middle: " + document.getString("middle"));
      }
      System.out.println("Last: " + document.getString("last"));
      System.out.println("Born: " + document.getLong("born"));
    }

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    users_ref = db.collection("users")
    docs = users_ref.stream()
    
    for doc in docs:
        print(f"{doc.id} => {doc.to_dict()}")

### Python  
(Async)

    users_ref = db.collection("users")
    docs = users_ref.stream()
    
    async for doc in docs:
        print(f"{doc.id} => {doc.to_dict()}")

### Node.js

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const snapshot = await db.collection('users').get();
    snapshot.forEach((doc) => {
      console.log(doc.id, '=>', doc.data());
    });

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    iter := client.Collection("users").Documents(ctx)
    for {
     doc, err := iter.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         log.Fatalf("Failed to iterate: %v", err)
     }
     fmt.Println(doc.Data())
    }

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $usersRef = $db->collection('samples/php/users');
    $snapshot = $usersRef->documents();
    foreach ($snapshot as $user) {
        printf('User: %s' . PHP_EOL, $user->id());
        printf('First: %s' . PHP_EOL, $user['first']);
        if (!empty($user['middle'])) {
            printf('Middle: %s' . PHP_EOL, $user['middle']);
        }
        printf('Last: %s' . PHP_EOL, $user['last']);
        printf('Born: %d' . PHP_EOL, $user['born']);
        printf(PHP_EOL);
    }
    printf('Retrieved and printed out all documents from the users collection.' . PHP_EOL);

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    CollectionReference usersRef = db.Collection("users");
    QuerySnapshot snapshot = await usersRef.GetSnapshotAsync();
    foreach (DocumentSnapshot document in snapshot.Documents)
    {
        Console.WriteLine("User: {0}", document.Id);
        Dictionary<string, object> documentDictionary = document.ToDictionary();
        Console.WriteLine("First: {0}", documentDictionary["First"]);
        if (documentDictionary.ContainsKey("Middle"))
        {
            Console.WriteLine("Middle: {0}", documentDictionary["Middle"]);
        }
        Console.WriteLine("Last: {0}", documentDictionary["Last"]);
        Console.WriteLine("Born: {0}", documentDictionary["Born"]);
        Console.WriteLine();
    }

### Ruby

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    users_ref = firestore.col collection_path
    users_ref.get do |user|
      puts "#{user.document_id} data: #{user.data}."
    end

## Next steps

Deepen your knowledge with the following topics:

  - **[Data model](https://docs.cloud.google.com/firestore/native/docs/data-model)** — Learn more about how data is structured in Firestore, including hierarchical data and subcollections.
  - **[Add data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)** — Learn more about creating and updating data in Firestore.
  - **[Get data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)** — Learn more about how to retrieve data.
  - **[Perform simple and compound queries](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)** — Learn how to run simple and compound queries.
  - **[Order and limit queries](https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data)** — Learn how to order and limit the data returned by your queries.
