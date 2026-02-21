# Get real-time updates

You can *listen* to a document with the `  onSnapshot()  ` method. An initial call using the callback you provide creates a document snapshot immediately with the current contents of the single document. Then, each time the contents change, another call updates the document snapshot.

**Note:**

  - [Pipeline operations](/firestore/native/docs/query-data/understanding-core-pipelines) don't support realtime listeners. To use realtime listeners with Enterprise edition databases, use core operations as described on this page.
  - Realtime listeners are not supported in the PHP client library.

### Web version 9

``` javascript
import { doc, onSnapshot } from "firebase/firestore";

const unsub = onSnapshot(doc(db, "cities", "SF"), (doc) => {
    console.log("Current data: ", doc.data());
});listen_document.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").doc("SF")
    .onSnapshot((doc) => {
        console.log("Current data: ", doc.data());
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities").document("SF")
  .addSnapshotListener { documentSnapshot, error in
    guard let document = documentSnapshot else {
      print("Error fetching document: \(error!)")
      return
    }
    guard let data = document.data() else {
      print("Document data was empty.")
      return
    }
    print("Current data: \(data)")
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"SF"]
    addSnapshotListener:^(FIRDocumentSnapshot *snapshot, NSError *error) {
      if (snapshot == nil) {
        NSLog(@"Error fetching document: %@", error);
        return;
      }
      NSLog(@"Current data: %@", snapshot.data);
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val docRef = db.collection("cities").document("SF")
docRef.addSnapshotListener { snapshot, e ->
    if (e != null) {
        Log.w(TAG, "Listen failed.", e)
        return@addSnapshotListener
    }

    if (snapshot != null && snapshot.exists()) {
        Log.d(TAG, "Current data: ${snapshot.data}")
    } else {
        Log.d(TAG, "Current data: null")
    }
}DocSnippets.kt
```

##### Java  
Android

``` java
final DocumentReference docRef = db.collection("cities").document("SF");
docRef.addSnapshotListener(new EventListener<DocumentSnapshot>() {
    @Override
    public void onEvent(@Nullable DocumentSnapshot snapshot,
                        @Nullable FirebaseFirestoreException e) {
        if (e != null) {
            Log.w(TAG, "Listen failed.", e);
            return;
        }

        if (snapshot != null && snapshot.exists()) {
            Log.d(TAG, "Current data: " + snapshot.getData());
        } else {
            Log.d(TAG, "Current data: null");
        }
    }
});DocSnippets.java
```

### Dart

``` dart
final docRef = db.collection("cities").doc("SF");
docRef.snapshots().listen(
      (event) => print("current data: ${event.data()}"),
      onError: (error) => print("Listen failed: $error"),
    );
firestore.dart
```

Often, you want your UI to react to changes in the contents of a Firestore document or collection. You can do so with a `  StreamBuilder  ` widget that consumes the Firestore snapshot stream:

``` dart
class UserInformation extends StatefulWidget {
  @override
  _UserInformationState createState() => _UserInformationState();
}

class _UserInformationState extends State<UserInformation> {
  final Stream<QuerySnapshot> _usersStream =
      FirebaseFirestore.instance.collection('users').snapshots();

  @override
  Widget build(BuildContext context) {
    return StreamBuilder<QuerySnapshot>(
      stream: _usersStream,
      builder: (BuildContext context, AsyncSnapshot<QuerySnapshot> snapshot) {
        if (snapshot.hasError) {
          return const Text('Something went wrong');
        }

        if (snapshot.connectionState == ConnectionState.waiting) {
          return const Text("Loading");
        }

        return ListView(
          children: snapshot.data!.docs
              .map((DocumentSnapshot document) {
                Map<String, dynamic> data =
                    document.data()! as Map<String, dynamic>;
                return ListTile(
                  title: Text(data['full_name']),
                  subtitle: Text(data['company']),
                );
              })
              .toList()
              .cast(),
        );
      },
    );
  }
}user_info_streambuilder.dart
```

##### Java

``` java
DocumentReference docRef = db.collection("cities").document("SF");
docRef.addSnapshotListener(
    new EventListener<DocumentSnapshot>() {
      @Override
      public void onEvent(@Nullable DocumentSnapshot snapshot, @Nullable FirestoreException e) {
        if (e != null) {
          System.err.println("Listen failed: " + e);
          return;
        }

        if (snapshot != null && snapshot.exists()) {
          System.out.println("Current data: " + snapshot.getData());
        } else {
          System.out.print("Current data: null");
        }
      }
    });ListenDataSnippets.java
```

##### Python

``` python
# Create an Event for notifying main thread.
callback_done = threading.Event()

# Create a callback on_snapshot function to capture changes
def on_snapshot(doc_snapshot, changes, read_time):
    for doc in doc_snapshot:
        print(f"Received document snapshot: {doc.id}")
    callback_done.set()

doc_ref = db.collection("cities").document("SF")

# Watch the document
doc_watch = doc_ref.on_snapshot(on_snapshot)snippets.py
```

##### C++

``` cpp
DocumentReference doc_ref = db->Collection("cities").Document("SF");
doc_ref.AddSnapshotListener(
    [](const DocumentSnapshot& snapshot, Error error, const std::string& errorMsg) {
      if (error == Error::kErrorOk) {
        if (snapshot.exists()) {
          std::cout << "Current data: " << snapshot << std::endl;
        } else {
          std::cout << "Current data: null" << std::endl;
        }
      } else {
        std::cout << "Listen failed: " << error << std::endl;
      }
    });snippets.cpp
```

##### Node.js

``` javascript
const doc = db.collection('cities').doc('SF');

const observer = doc.onSnapshot(docSnapshot => {
  console.log(`Received doc snapshot: ${docSnapshot}`);
  // ...
}, err => {
  console.log(`Encountered error: ${err}`);
});index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/firestore"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenDocument listens to a single document.
func listenDocument(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 // Сontext with timeout stops listening to changes.
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Doc("SF").Snapshots(ctx)
 for {
     snap, err := it.Next()
     // DeadlineExceeded will be returned when ctx is cancelled.
     if status.Code(err) == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if !snap.Exists() {
         fmt.Fprintf(w, "Document no longer exists\n")
         return nil
     }
     fmt.Fprintf(w, "Received document snapshot: %v\n", ssnap.Data))
 }
}
listen_document.go
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
DocumentReference docRef = db.Collection("cities").Document("SF");
docRef.Listen(snapshot => {
    Debug.Log("Callback received document snapshot.");
    Debug.Log(String.Format("Document data for {0} document:", snapshot.Id));
    Dictionary<string, object> city = snapshot.ToDictionary();
    foreach (KeyValuePair<string, object> pair in city) {
        Debug.Log(String.Format("{0}: {1}", pair.Key, pair.Value));
    }
});
```

##### C\#

``` csharp
DocumentReference docRef = db.Collection("cities").Document("SF");
FirestoreChangeListener listener = docRef.Listen(snapshot =>
{
    Console.WriteLine("Callback received document snapshot.");
    Console.WriteLine("Document exists? {0}", snapshot.Exists);
    if (snapshot.Exists)
    {
        Console.WriteLine("Document data for {0} document:", snapshot.Id);
        Dictionary<string, object> city = snapshot.ToDictionary();
        foreach (KeyValuePair<string, object> pair in city)
        {
            Console.WriteLine("{0}: {1}", pair.Key, pair.Value);
        }
    }
});Program.cs
```

##### Ruby

``` ruby
doc_ref = firestore.col(collection_path).doc document_path
snapshots = []

# Watch the document.
listener = doc_ref.listen do |snapshot|
  puts "Received document snapshot: #{snapshot.document_id}"
  snapshots << snapshot
endquery_watch.rb
```

### Events for local changes

Local writes in your app will invoke snapshot listeners immediately. This is because of an important feature called "latency compensation." When you perform a write, your listeners will be notified with the new data *before* the data is sent to the backend.

Retrieved documents have a `  metadata.hasPendingWrites  ` property that indicates whether the document has local changes that haven't been written to the backend yet. You can use this property to determine the source of events received by your snapshot listener:

### Web version 9

``` javascript
import { doc, onSnapshot } from "firebase/firestore";

const unsub = onSnapshot(doc(db, "cities", "SF"), (doc) => {
  const source = doc.metadata.hasPendingWrites ? "Local" : "Server";
  console.log(source, " data: ", doc.data());
});listen_document_local.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").doc("SF")
    .onSnapshot((doc) => {
        var source = doc.metadata.hasPendingWrites ? "Local" : "Server";
        console.log(source, " data: ", doc.data());
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities").document("SF")
  .addSnapshotListener { documentSnapshot, error in
    guard let document = documentSnapshot else {
      print("Error fetching document: \(error!)")
      return
    }
    let source = document.metadata.hasPendingWrites ? "Local" : "Server"
    print("\(source) data: \(document.data() ?? [:])")
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"SF"]
    addSnapshotListener:^(FIRDocumentSnapshot *snapshot, NSError *error) {
      if (snapshot == nil) {
        NSLog(@"Error fetching document: %@", error);
        return;
      }
      NSString *source = snapshot.metadata.hasPendingWrites ? @"Local" : @"Server";
      NSLog(@"%@ data: %@", source, snapshot.data);
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val docRef = db.collection("cities").document("SF")
docRef.addSnapshotListener { snapshot, e ->
    if (e != null) {
        Log.w(TAG, "Listen failed.", e)
        return@addSnapshotListener
    }

    val source = if (snapshot != null && snapshot.metadata.hasPendingWrites()) {
        "Local"
    } else {
        "Server"
    }

    if (snapshot != null && snapshot.exists()) {
        Log.d(TAG, "$source data: ${snapshot.data}")
    } else {
        Log.d(TAG, "$source data: null")
    }
}DocSnippets.kt
```

##### Java  
Android

``` java
final DocumentReference docRef = db.collection("cities").document("SF");
docRef.addSnapshotListener(new EventListener<DocumentSnapshot>() {
    @Override
    public void onEvent(@Nullable DocumentSnapshot snapshot,
                        @Nullable FirebaseFirestoreException e) {
        if (e != null) {
            Log.w(TAG, "Listen failed.", e);
            return;
        }

        String source = snapshot != null && snapshot.getMetadata().hasPendingWrites()
                ? "Local" : "Server";

        if (snapshot != null && snapshot.exists()) {
            Log.d(TAG, source + " data: " + snapshot.getData());
        } else {
            Log.d(TAG, source + " data: null");
        }
    }
});DocSnippets.java
```

### Dart

``` dart
final docRef = db.collection("cities").doc("SF");
docRef.snapshots().listen(
  (event) {
    final source = (event.metadata.hasPendingWrites) ? "Local" : "Server";
    print("$source data: ${event.data()}");
  },
  onError: (error) => print("Listen failed: $error"),
);
firestore.dart
```

##### Java

``` text
# Not yet supported in the Java client library
```

##### Python

``` text
// Not yet supported in Python client library
```

##### C++

``` cpp
DocumentReference doc_ref = db->Collection("cities").Document("SF");
doc_ref.AddSnapshotListener([](const DocumentSnapshot& snapshot,
                               Error error, const std::string& errorMsg) {
  if (error == Error::kErrorOk) {
    const char* source =
        snapshot.metadata().has_pending_writes() ? "Local" : "Server";
    if (snapshot.exists()) {
      std::cout << source << " data: " << snapshot.Get("name").string_value()
                << std::endl;
    } else {
      std::cout << source << " data: null" << std::endl;
    }
  } else {
    std::cout << "Listen failed: " << error << std::endl;
  }
});snippets.cpp
```

##### Node.js

``` text
// Not yet supported in the Node.js client library
```

##### Go

``` text
// Not yet supported in the Go client library
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
DocumentReference docRef = db.Collection("cities").Document("SF");
docRef.Listen(
  snapshot =>
  {
      string source = (snapshot != null && snapshot.Metadata.HasPendingWrites) ? "Local" : "Server";
      string snapshotData = "null";
      if (snapshot != null && snapshot.Exists)
      {
          System.Text.StringBuilder builder = new System.Text.StringBuilder();
          IDictionary<string, object> dict = snapshot.ToDictionary();
          foreach (var KVPair in dict)
          {
              builder.Append($"{KVPair.Key}: {KVPair.Value}\n");
          }
          snapshotData = builder.ToString();
      }
      Debug.Log($"{source} data: ${snapshotData}");
  });
```

##### C\#

``` text
// Not yet supported in the C# client library
```

##### Ruby

``` text
// Not yet supported in the Ruby client library
```

### Events for metadata changes

When listening for changes to a document, collection, or query, you can pass options to control the granularity of events that your listener will receive.

By default, listeners are not notified of changes that only affect metadata. Consider what happens when your app writes a new document:

1.  A change event is immediately fired with the new data. The document has not yet been written to the backend so the "pending writes" flag is `  true  ` .
2.  The document is written to the backend.
3.  The backend notifies the client of the successful write. There is no change to the document data, but there is a metadata change because the "pending writes" flag is now `  false  ` .

If you want to receive snapshot events when the document or query metadata changes, pass a listen options object when attaching your listener.

**Note:** You can pass listener options as shown in the following samples. You can also use the configuration interfaces for snapshot options [described below](#events-local-only) to explicitly configure events for metadata changes. For more information, see the reference documentation for [Kotlin + KTX Android]() , [Java Android]() , [Swift]() , [Objective-C]() , and [Web modular]() .

### Web version 9

``` javascript
import { doc, onSnapshot } from "firebase/firestore";

const unsub = onSnapshot(
  doc(db, "cities", "SF"), 
  { includeMetadataChanges: true }, 
  (doc) => {
    // ...
  });listen_with_metadata.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").doc("SF")
    .onSnapshot({
        // Listen for document metadata changes
        includeMetadataChanges: true
    }, (doc) => {
        // ...
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Listen to document metadata.
db.collection("cities").document("SF")
  .addSnapshotListener(includeMetadataChanges: true) { documentSnapshot, error in
    // ...
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Listen for metadata changes.
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"SF"]
    addSnapshotListenerWithIncludeMetadataChanges:YES
                                         listener:^(FIRDocumentSnapshot *snapshot, NSError *error) {
   // ...
}];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Listen for metadata changes to the document.
val docRef = db.collection("cities").document("SF")
docRef.addSnapshotListener(MetadataChanges.INCLUDE) { snapshot, e ->
    // ...
}DocSnippets.kt
```

##### Java  
Android

``` java
// Listen for metadata changes to the document.
DocumentReference docRef = db.collection("cities").document("SF");
docRef.addSnapshotListener(MetadataChanges.INCLUDE, new EventListener<DocumentSnapshot>() {
    @Override
    public void onEvent(@Nullable DocumentSnapshot snapshot,
                        @Nullable FirebaseFirestoreException e) {
        // ...
    }
});DocSnippets.java
```

### Dart

``` dart
final docRef = db.collection("cities").doc("SF");
docRef.snapshots(includeMetadataChanges: true).listen((event) {
  // ...
});firestore.dart
```

##### Java

``` text
// Not yet supported in the Java client library
```

##### Python

``` text
// Not yet supported in Python client library
```

##### C++

``` cpp
DocumentReference doc_ref = db->Collection("cities").Document("SF");
doc_ref.AddSnapshotListener(
    MetadataChanges::kInclude,
    [](const DocumentSnapshot& snapshot, Error error, const std::string& errorMsg) { /* ... */ });snippets.cpp
```

##### Node.js

``` text
// Not yet supported the Node.js client library
```

##### Go

``` text
// Not yet supported in the Go client library
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
DocumentReference docRef = db.Collection("cities").Document("SF");
docRef.Listen(MetadataChanges.Include, snapshot =>
{
    // ...
});
```

##### C\#

``` text
// Not yet supported in the C# client library
```

##### Ruby

``` text
// Not yet supported in the Ruby client library
```

**Note:** If you just want to know when your write has completed, you can listen to the completion callback rather than using `  hasPendingWrites  ` . In JavaScript, use the `  Promise  ` returned from your write operation by attaching a `  .then()  ` callback. In Swift, pass a completion callback to your write function.

### Configure listeners for local changes only

Firestore in Native Mode snapshot listeners take an initial snapshot from the local cache and concurrently fetch corresponding data from the server.

In some cases, you may not want follow-up fetches from the server. Client SDKs allow you to configure listeners to fire only with respect to data in the local cache. This helps you avoid unnecessary server calls and their costs, and leverage the client-side cache, which reflects local data and mutations.

Here, snapshot options are set in client code to allow listening for local changes only.

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from the namespaced API.

``` text
const unsubscribe = onSnapshot(
   doc(db, "cities", "SF"),
    { 
      includeMetadataChanges: true,
      source:'cache'
     },
    (documentSnapshot) => {//…}
  );
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from the namespaced API.

``` text
// Not yet supported in the Web namespaced API
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` text
// Set up listener options
let options = SnapshotListenOptions()
    .withSource(ListenSource.cache)
    .withIncludeMetadataChanges(true)
db.collection("cities").document("SF")
  .addSnapshotListener(options: options) { documentSnapshot, error in
    // ...
  }
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` text
// Set up listener options
FIRSnapshotListenOptions *options = [[FIRSnapshotListenOptions alloc] init];
FIRSnapshotListenOptions *optionsWithSourceAndMetadata = 
                    [[options optionsWithIncludeMetadataChanges:YES] 
                      optionsWithSource:FIRListenSourceCache];
[[[self.db collectionWithPath:@"cities"] documentWithPath:@"SF"]
  addSnapshotListenerWithOptions:optionsWithSourceAndMetadata
  listener: ^ (FIRDocumentSnapshot * snapshot, NSError * error) {
    //…
  }
];
```

##### Kotlin  
Android

``` text
// Set up listener options
val options = SnapshotListenOptions.Builder()
  .setMetadataChanges(MetadataChanges.INCLUDE)
  .setSource(ListenSource.CACHE)
  .build();
db.collection("cities").document("SF")
  .addSnapshotListener(options) { snapshot, error ->
    //…
  }
```

##### Java  
Android

``` text
// Set up listener options
SnapshotListenOptions options = new SnapshotListenOptions.Builder()
  .setMetadataChanges(MetadataChanges.INCLUDE)
  .setSource(ListenSource.CACHE)
  .build();
db.collection("cities").document("SF").addSnapshotListener(options, new EventListener<DocumentSnapshot>() {
    //…
  });
```

### Dart

``` text
// Not yet supported in this client library
```

##### Java

``` text
# Not yet supported in the Java client library
```

##### Python

``` text
// Not yet supported in Python client library
```

##### C++

``` text
// Not yet supported in the C++ client library
```

##### Node.js

``` text
// Not yet supported in the Node.js client library
```

##### Go

``` text
// Not yet supported in the Go client library
```

##### PHP

``` text
// Not yet supported in the PHP client library
```

##### Unity

``` text
// Not yet supported in the Unity client library
```

##### C\#

``` text
// Not yet supported in the C# client library
```

##### Ruby

``` text
// Not yet supported in the Ruby client library
```

## Listen to multiple documents in a collection

As with documents, you can use `  onSnapshot()  ` instead of `  get()  ` to listen to the results of a query. This creates a query snapshot. For example, to listen to the documents with state `  CA  ` :

### Web version 9

``` javascript
import { collection, query, where, onSnapshot } from "firebase/firestore";

const q = query(collection(db, "cities"), where("state", "==", "CA"));
const unsubscribe = onSnapshot(q, (querySnapshot) => {
  const cities = [];
  querySnapshot.forEach((doc) => {
      cities.push(doc.data().name);
  });
  console.log("Current cities in CA: ", cities.join(", "));
});listen_multiple.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").where("state", "==", "CA")
    .onSnapshot((querySnapshot) => {
        var cities = [];
        querySnapshot.forEach((doc) => {
            cities.push(doc.data().name);
        });
        console.log("Current cities in CA: ", cities.join(", "));
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities").whereField("state", isEqualTo: "CA")
  .addSnapshotListener { querySnapshot, error in
    guard let documents = querySnapshot?.documents else {
      print("Error fetching documents: \(error!)")
      return
    }
    let cities = documents.compactMap { $0["name"] }
    print("Current cities in CA: \(cities)")
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] queryWhereField:@"state" isEqualTo:@"CA"]
    addSnapshotListener:^(FIRQuerySnapshot *snapshot, NSError *error) {
      if (snapshot == nil) {
        NSLog(@"Error fetching documents: %@", error);
        return;
      }
      NSMutableArray *cities = [NSMutableArray array];
      for (FIRDocumentSnapshot *document in snapshot.documents) {
        [cities addObject:document.data[@"name"]];
      }
      NSLog(@"Current cities in CA: %@", cities);
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collection("cities")
    .whereEqualTo("state", "CA")
    .addSnapshotListener { value, e ->
        if (e != null) {
            Log.w(TAG, "Listen failed.", e)
            return@addSnapshotListener
        }

        val cities = ArrayList<String>()
        for (doc in value!!) {
            doc.getString("name")?.let {
                cities.add(it)
            }
        }
        Log.d(TAG, "Current cites in CA: $cities")
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collection("cities")
        .whereEqualTo("state", "CA")
        .addSnapshotListener(new EventListener<QuerySnapshot>() {
            @Override
            public void onEvent(@Nullable QuerySnapshot value,
                                @Nullable FirebaseFirestoreException e) {
                if (e != null) {
                    Log.w(TAG, "Listen failed.", e);
                    return;
                }

                List<String> cities = new ArrayList<>();
                for (QueryDocumentSnapshot doc : value) {
                    if (doc.get("name") != null) {
                        cities.add(doc.getString("name"));
                    }
                }
                Log.d(TAG, "Current cites in CA: " + cities);
            }
        });DocSnippets.java
```

### Dart

``` dart
db
    .collection("cities")
    .where("state", isEqualTo: "CA")
    .snapshots()
    .listen((event) {
  final cities = [];
  for (var doc in event.docs) {
    cities.add(doc.data()["name"]);
  }
  print("cities in CA: ${cities.join(", ")}");
});firestore.dart
```

##### Java

``` java
db.collection("cities")
    .whereEqualTo("state", "CA")
    .addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          @Override
          public void onEvent(
              @Nullable QuerySnapshot snapshots, @Nullable FirestoreException e) {
            if (e != null) {
              System.err.println("Listen failed:" + e);
              return;
            }

            List<String> cities = new ArrayList<>();
            for (DocumentSnapshot doc : snapshots) {
              if (doc.get("name") != null) {
                cities.add(doc.getString("name"));
              }
            }
            System.out.println("Current cites in CA: " + cities);
          }
        });ListenDataSnippets.java
```

##### Python

``` python
# Create an Event for notifying main thread.
callback_done = threading.Event()

# Create a callback on_snapshot function to capture changes
def on_snapshot(col_snapshot, changes, read_time):
    print("Callback received query snapshot.")
    print("Current cities in California:")
    for doc in col_snapshot:
        print(f"{doc.id}")
    callback_done.set()

col_query = db.collection("cities").where(filter=FieldFilter("state", "==", "CA"))

# Watch the collection query
query_watch = col_query.on_snapshot(on_snapshot)
snippets.py
```

##### C++

``` cpp
db->Collection("cities")
    .WhereEqualTo("state", FieldValue::String("CA"))
    .AddSnapshotListener([](const QuerySnapshot& snapshot, Error error, const std::string& errorMsg) {
      if (error == Error::kErrorOk) {
        std::vector<std::string> cities;
        std::cout << "Current cities in CA: " << error << std::endl;
        for (const DocumentSnapshot& doc : snapshot.documents()) {
          cities.push_back(doc.Get("name").string_value());
          std::cout << "" << cities.back() << std::endl;
        }
      } else {
        std::cout << "Listen failed: " << error << std::endl;
      }
    });snippets.cpp
```

##### Node.js

``` javascript
const query = db.collection('cities').where('state', '==', 'CA');

const observer = query.onSnapshot(querySnapshot => {
  console.log(`Received query snapshot of size ${querySnapshot.size}`);
  // ...
}, err => {
  console.log(`Encountered error: ${err}`);
});index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/firestore"
 "google.golang.org/api/iterator"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenMultiple listens to a query, returning the names of all cities
// for a state.
func listenMultiple(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Where("state", "==", "CA").Snapshots(ctx)
 for {
     snap, err := it.Next()
     // DeadlineExceeded will be returned when ctx is cancelled.
     if status.Code(err) == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if snap != nil {
         for {
             doc, err := snap.Documents.Next()
             if err == iterator.Done {
                 break
             }
             if err != nil {
                 return fmt.Errorf("Documents.Next: %w", err)
             }
             fmt.Fprintf(w, "Current cities in California: %v\n", doc.Ref.ID)
         }
     }
 }
}
listen_multiple.go
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
Query query = db.Collection("cities").WhereEqualTo("State", "CA");

ListenerRegistration listener = query.Listen(snapshot => {
  Debug.Log("Callback received query snapshot.");
  Debug.Log("Current cities in California:");
  foreach (DocumentSnapshot documentSnapshot in snapshot.Documents) {
    Debug.Log(documentSnapshot.Id);
  }
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = db.Collection("cities").WhereEqualTo("State", "CA");

FirestoreChangeListener listener = query.Listen(snapshot =>
{
    Console.WriteLine("Callback received query snapshot.");
    Console.WriteLine("Current cities in California:");
    foreach (DocumentSnapshot documentSnapshot in snapshot.Documents)
    {
        Console.WriteLine(documentSnapshot.Id);
    }
});Program.cs
```

##### Ruby

``` ruby
query = firestore.col(collection_path).where :state, :==, "CA"
docs = []

# Watch the collection query.
listener = query.listen do |snapshot|
  puts "Callback received query snapshot."
  puts "Current cities in California:"
  snapshot.docs.each do |doc|
    puts doc.document_id
    docs << doc
  end
endquery_watch.rb
```

The snapshot handler will receive a new query snapshot every time the query results change (that is, when a document is added, removed, or modified).

**Important:** As explained above under [Events for local changes](#events-local-changes) , you will receive events *immediately* for your local writes. Your listener can use the `  metadata.hasPendingWrites  ` field on each document to determine whether the document has local changes that have not yet been written to the backend.

## View changes between snapshots

It is often useful to see the actual changes to query results between query snapshots, instead of simply using the entire query snapshot. For example, you may want to maintain a cache as individual documents are added, removed, and modified.

### Web version 9

``` javascript
import { collection, query, where, onSnapshot } from "firebase/firestore";

const q = query(collection(db, "cities"), where("state", "==", "CA"));
const unsubscribe = onSnapshot(q, (snapshot) => {
  snapshot.docChanges().forEach((change) => {
    if (change.type === "added") {
        console.log("New city: ", change.doc.data());
    }
    if (change.type === "modified") {
        console.log("Modified city: ", change.doc.data());
    }
    if (change.type === "removed") {
        console.log("Removed city: ", change.doc.data());
    }
  });
});listen_diffs.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities").where("state", "==", "CA")
    .onSnapshot((snapshot) => {
        snapshot.docChanges().forEach((change) => {
            if (change.type === "added") {
                console.log("New city: ", change.doc.data());
            }
            if (change.type === "modified") {
                console.log("Modified city: ", change.doc.data());
            }
            if (change.type === "removed") {
                console.log("Removed city: ", change.doc.data());
            }
        });
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities").whereField("state", isEqualTo: "CA")
  .addSnapshotListener { querySnapshot, error in
    guard let snapshot = querySnapshot else {
      print("Error fetching snapshots: \(error!)")
      return
    }
    snapshot.documentChanges.forEach { diff in
      if (diff.type == .added) {
        print("New city: \(diff.document.data())")
      }
      if (diff.type == .modified) {
        print("Modified city: \(diff.document.data())")
      }
      if (diff.type == .removed) {
        print("Removed city: \(diff.document.data())")
      }
    }
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[self.db collectionWithPath:@"cities"] queryWhereField:@"state" isEqualTo:@"CA"]
    addSnapshotListener:^(FIRQuerySnapshot *snapshot, NSError *error) {
      if (snapshot == nil) {
        NSLog(@"Error fetching documents: %@", error);
        return;
      }
      for (FIRDocumentChange *diff in snapshot.documentChanges) {
        if (diff.type == FIRDocumentChangeTypeAdded) {
          NSLog(@"New city: %@", diff.document.data);
        }
        if (diff.type == FIRDocumentChangeTypeModified) {
          NSLog(@"Modified city: %@", diff.document.data);
        }
        if (diff.type == FIRDocumentChangeTypeRemoved) {
          NSLog(@"Removed city: %@", diff.document.data);
        }
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collection("cities")
    .whereEqualTo("state", "CA")
    .addSnapshotListener { snapshots, e ->
        if (e != null) {
            Log.w(TAG, "listen:error", e)
            return@addSnapshotListener
        }

        for (dc in snapshots!!.documentChanges) {
            when (dc.type) {
                DocumentChange.Type.ADDED -> Log.d(TAG, "New city: ${dc.document.data}")
                DocumentChange.Type.MODIFIED -> Log.d(TAG, "Modified city: ${dc.document.data}")
                DocumentChange.Type.REMOVED -> Log.d(TAG, "Removed city: ${dc.document.data}")
            }
        }
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collection("cities")
        .whereEqualTo("state", "CA")
        .addSnapshotListener(new EventListener<QuerySnapshot>() {
            @Override
            public void onEvent(@Nullable QuerySnapshot snapshots,
                                @Nullable FirebaseFirestoreException e) {
                if (e != null) {
                    Log.w(TAG, "listen:error", e);
                    return;
                }

                for (DocumentChange dc : snapshots.getDocumentChanges()) {
                    switch (dc.getType()) {
                        case ADDED:
                            Log.d(TAG, "New city: " + dc.getDocument().getData());
                            break;
                        case MODIFIED:
                            Log.d(TAG, "Modified city: " + dc.getDocument().getData());
                            break;
                        case REMOVED:
                            Log.d(TAG, "Removed city: " + dc.getDocument().getData());
                            break;
                    }
                }

            }
        });DocSnippets.java
```

### Dart

``` dart
db
    .collection("cities")
    .where("state", isEqualTo: "CA")
    .snapshots()
    .listen((event) {
  for (var change in event.docChanges) {
    switch (change.type) {
      case DocumentChangeType.added:
        print("New City: ${change.doc.data()}");
        break;
      case DocumentChangeType.modified:
        print("Modified City: ${change.doc.data()}");
        break;
      case DocumentChangeType.removed:
        print("Removed City: ${change.doc.data()}");
        break;
    }
  }
});firestore.dart
```

##### Java

``` java
db.collection("cities")
    .whereEqualTo("state", "CA")
    .addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          @Override
          public void onEvent(
              @Nullable QuerySnapshot snapshots, @Nullable FirestoreException e) {
            if (e != null) {
              System.err.println("Listen failed: " + e);
              return;
            }

            for (DocumentChange dc : snapshots.getDocumentChanges()) {
              switch (dc.getType()) {
                case ADDED:
                  System.out.println("New city: " + dc.getDocument().getData());
                  break;
                case MODIFIED:
                  System.out.println("Modified city: " + dc.getDocument().getData());
                  break;
                case REMOVED:
                  System.out.println("Removed city: " + dc.getDocument().getData());
                  break;
                default:
                  break;
              }
            }
          }
        });ListenDataSnippets.java
```

##### C++

``` cpp
db->Collection("cities")
    .WhereEqualTo("state", FieldValue::String("CA"))
    .AddSnapshotListener([](const QuerySnapshot& snapshot, Error error, const std::string& errorMsg) {
      if (error == Error::kErrorOk) {
        for (const DocumentChange& dc : snapshot.DocumentChanges()) {
          switch (dc.type()) {
            case DocumentChange::Type::kAdded:
              std::cout << "New city: "
                        << dc.document().Get("name").string_value() << std::endl;
              break;
            case DocumentChange::Type::kModified:
              std::cout << "Modified city: "
                        << dc.document().Get("name").string_value() << std::endl;
              break;
            case DocumentChange::Type::kRemoved:
              std::cout << "Removed city: "
                        << dc.document().Get("name").string_value() << std::endl;
              break;
          }
        }
      } else {
        std::cout << "Listen failed: " << error << std::endl;
      }
    });snippets.cpp
```

##### Python

``` python
# Create an Event for notifying main thread.
delete_done = threading.Event()

# Create a callback on_snapshot function to capture changes
def on_snapshot(col_snapshot, changes, read_time):
    print("Callback received query snapshot.")
    print("Current cities in California: ")
    for change in changes:
        if change.type.name == "ADDED":
            print(f"New city: {change.document.id}")
        elif change.type.name == "MODIFIED":
            print(f"Modified city: {change.document.id}")
        elif change.type.name == "REMOVED":
            print(f"Removed city: {change.document.id}")
            delete_done.set()

col_query = db.collection("cities").where(filter=FieldFilter("state", "==", "CA"))

# Watch the collection query
query_watch = col_query.on_snapshot(on_snapshot)
snippets.py
```

##### Node.js

``` javascript
const observer = db.collection('cities').where('state', '==', 'CA')
  .onSnapshot(querySnapshot => {
    querySnapshot.docChanges().forEach(change => {
      if (change.type === 'added') {
        console.log('New city: ', change.doc.data());
      }
      if (change.type === 'modified') {
        console.log('Modified city: ', change.doc.data());
      }
      if (change.type === 'removed') {
        console.log('Removed city: ', change.doc.data());
      }
    });
  });index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/firestore"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenChanges listens to a query, returning the list of document changes.
func listenChanges(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Where("state", "==", "CA").Snapshots(ctx)
 for {
     snap, err := it.Next()
     // DeadlineExceeded will be returned when ctx is cancelled.
     if status.Code(err) == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if snap != nil {
         for _, change := range snap.Changes {
             switch change.Kind {
             case firestore.DocumentAdded:
                 fmt.Fprintf(w, "New city: %v\n", change.Doc.Data())
             case firestore.DocumentModified:
                 fmt.Fprintf(w, "Modified city: %v\n", change.Doc.Data())
             case firestore.DocumentRemoved:
                 fmt.Fprintf(w, "Removed city: %v\n", change.Doc.Data())
             }
         }
     }
 }
}
listen_changes.go
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
Query query = db.Collection("cities").WhereEqualTo("State", "CA");

ListenerRegistration listener = query.Listen(snapshot =>
{
    foreach (DocumentChange change in snapshot.GetChanges())
    {
        if (change.ChangeType == DocumentChange.Type.Added)
        {
            Debug.Log(String.Format("New city: {0}", change.Document.Id));
        }
        else if (change.ChangeType == DocumentChange.Type.Modified)
        {
            Debug.Log(String.Format("Modified city: {0}", change.Document.Id));
        }
        else if (change.ChangeType == DocumentChange.Type.Removed)
        {
            Debug.Log(String.Format("Removed city: {0}", change.Document.Id));
        }
    }
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = db.Collection("cities").WhereEqualTo("State", "CA");

FirestoreChangeListener listener = query.Listen(snapshot =>
{
    foreach (DocumentChange change in snapshot.Changes)
    {
        if (change.ChangeType.ToString() == "Added")
        {
            Console.WriteLine("New city: {0}", change.Document.Id);
        }
        else if (change.ChangeType.ToString() == "Modified")
        {
            Console.WriteLine("Modified city: {0}", change.Document.Id);
        }
        else if (change.ChangeType.ToString() == "Removed")
        {
            Console.WriteLine("Removed city: {0}", change.Document.Id);
        }
    }
});Program.cs
```

##### Ruby

``` ruby
query = firestore.col(collection_path).where :state, :==, "CA"
added = []
modified = []
removed = []

# Watch the collection query.
listener = query.listen do |snapshot|
  puts "Callback received query snapshot."
  puts "Current cities in California:"
  snapshot.changes.each do |change|
    if change.added?
      puts "New city: #{change.doc.document_id}"
      added << snapshot
    elsif change.modified?
      puts "Modified city: #{change.doc.document_id}"
      modified << snapshot
    elsif change.removed?
      puts "Removed city: #{change.doc.document_id}"
      removed << snapshot
    end
  end
endquery_watch.rb
```

**Important:** The first query snapshot contains `  added  ` events for all existing documents that match the query. This is because you're getting a set of changes that bring your query snapshot current with the initial state of the query. This allows you, for instance, to directly populate your UI from the changes you receive in the first query snapshot, without needing to add special logic for handling the initial state.

The initial state can come from the server directly, or from a local cache. If there is state available in a local cache, the query snapshot will be initially populated with the cached data, then updated with the server's data when the client has caught up with the server's state.

## Detach a listener

When you are no longer interested in listening to your data, you must detach your listener so that your event callbacks stop getting called. This allows the client to stop using bandwidth to receive updates. For example:

### Web version 9

``` javascript
import { collection, onSnapshot } from "firebase/firestore";

const unsubscribe = onSnapshot(collection(db, "cities"), () => {
  // Respond to data
  // ...
});

// Later ...

// Stop listening to changes
unsubscribe();detach_listener.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var unsubscribe = db.collection("cities")
    .onSnapshot(() => {
      // Respond to data
      // ...
    });

// Later ...

// Stop listening to changes
unsubscribe();test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let listener = db.collection("cities").addSnapshotListener { querySnapshot, error in
  // ...
}

// ...

// Stop listening to changes
listener.remove()ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
id<FIRListenerRegistration> listener = [[self.db collectionWithPath:@"cities"]
    addSnapshotListener:^(FIRQuerySnapshot *snapshot, NSError *error) {
      // ...
}];

// ...

// Stop listening to changes
[listener remove];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities")
val registration = query.addSnapshotListener { snapshots, e ->
    // ...
}

// ...

// Stop listening to changes
registration.remove()DocSnippets.kt
```

##### Java  
Android

``` java
Query query = db.collection("cities");
ListenerRegistration registration = query.addSnapshotListener(
        new EventListener<QuerySnapshot>() {
            // ...
        });

// ...

// Stop listening to changes
registration.remove();DocSnippets.java
```

### Dart

``` dart
final collection = db.collection("cities");
final listener = collection.snapshots().listen((event) {
  // ...
});
listener.cancel();firestore.dart
```

##### Java

``` java
Query query = db.collection("cities");
ListenerRegistration registration =
    query.addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          // ...
        });

// ...

// Stop listening to changes
registration.remove();ListenDataSnippets.java
```

##### Python

``` python
# Terminate watch on a document
doc_watch.unsubscribe()snippets.py
```

##### C++

``` cpp
// Add a listener
Query query = db->Collection("cities");
ListenerRegistration registration = query.AddSnapshotListener(
    [](const QuerySnapshot& snapshot, Error error, const std::string& errorMsg) { /* ... */ });
// Stop listening to changes
registration.Remove();snippets.cpp
```

##### Node.js

``` javascript
const unsub = db.collection('cities').onSnapshot(() => {
});

// ...

// Stop listening for changes
unsub();index.js
```

##### Go

``` go
// Сontext with timeout stops listening to changes.
ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
defer cancel()listen_document.go
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
listener.Stop();
```

##### C\#

``` csharp
await listener.StopAsync();Program.cs
```

##### Ruby

``` ruby
listener.stopquery_watch.rb
```

## Handle listen errors

A listen may occasionally fail — for example, due to security permissions, or if you tried to listen on an invalid query. (Learn more about [valid and invalid queries](/firestore/native/docs/query-data/queries#compound_queries) .) To handle these failures, you can provide an error callback when you attach your snapshot listener. After an error, the listener will not receive any more events, and there is no need to detach your listener.

### Web version 9

``` javascript
import { collection, onSnapshot } from "firebase/firestore";

const unsubscribe = onSnapshot(
  collection(db, "cities"), 
  (snapshot) => {
    // ...
  },
  (error) => {
    // ...
  });handle_listen_errors.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("cities")
    .onSnapshot((snapshot) => {
        // ...
    }, (error) => {
        // ...
    });test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities")
  .addSnapshotListener { querySnapshot, error in
    if let error = error {
      print("Error retreiving collection: \(error)")
    }
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[self.db collectionWithPath:@"cities"]
    addSnapshotListener:^(FIRQuerySnapshot *snapshot, NSError *error) {
      if (error != nil) {
        NSLog(@"Error retreving collection: %@", error);
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collection("cities")
    .addSnapshotListener { snapshots, e ->
        if (e != null) {
            Log.w(TAG, "listen:error", e)
            return@addSnapshotListener
        }

        for (dc in snapshots!!.documentChanges) {
            if (dc.type == DocumentChange.Type.ADDED) {
                Log.d(TAG, "New city: ${dc.document.data}")
            }
        }
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collection("cities")
        .addSnapshotListener(new EventListener<QuerySnapshot>() {
            @Override
            public void onEvent(@Nullable QuerySnapshot snapshots,
                                @Nullable FirebaseFirestoreException e) {
                if (e != null) {
                    Log.w(TAG, "listen:error", e);
                    return;
                }

                for (DocumentChange dc : snapshots.getDocumentChanges()) {
                    if (dc.getType() == Type.ADDED) {
                        Log.d(TAG, "New city: " + dc.getDocument().getData());
                    }
                }

            }
        });DocSnippets.java
```

### Dart

``` dart
final docRef = db.collection("cities");
docRef.snapshots().listen(
      (event) => print("listener attached"),
      onError: (error) => print("Listen failed: $error"),
    );firestore.dart
```

##### Java

``` java
db.collection("cities")
    .addSnapshotListener(
        new EventListener<QuerySnapshot>() {
          @Override
          public void onEvent(
              @Nullable QuerySnapshot snapshots, @Nullable FirestoreException e) {
            if (e != null) {
              System.err.println("Listen failed: " + e);
              return;
            }

            for (DocumentChange dc : snapshots.getDocumentChanges()) {
              if (dc.getType() == Type.ADDED) {
                System.out.println("New city: " + dc.getDocument().getData());
              }
            }
          }
        });ListenDataSnippets.java
```

##### Python

``` text
// Snippet coming soon
```

##### C++

``` text
// Snippet coming soon.
```

##### Node.js

``` javascript
db.collection('cities')
  .onSnapshot((snapshot) => {
    //...
  }, (error) => {
    //...
  });index.js
```

##### Go

``` go
import (
 "context"
 "fmt"
 "io"
 "time"

 "cloud.google.com/go/firestore"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
)

// listenErrors demonstrates how to handle listening errors.
func listenErrors(ctx context.Context, w io.Writer, projectID, collection string) error {
 // projectID := "project-id"
 ctx, cancel := context.WithTimeout(ctx, 30*time.Second)
 defer cancel()

 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("firestore.NewClient: %w", err)
 }
 defer client.Close()

 it := client.Collection(collection).Snapshots(ctx)
 for {
     snap, err := it.Next()
     // Canceled will be returned when ctx is cancelled and DeadlineExceeded will
     // be returned when ctx reaches its deadline.
     if e := status.Code(err); e == codes.Canceled || e == codes.DeadlineExceeded {
         return nil
     }
     if err != nil {
         return fmt.Errorf("Snapshots.Next: %w", err)
     }
     if snap != nil {
         for _, change := range snap.Changes {
             if change.Kind == firestore.DocumentAdded {
                 fmt.Fprintf(w, "New city: %v\n", change.Doc.Data())
             }
         }
     }
 }
}
listen_errors.go
```

##### PHP

``` text
// Not supported in the PHP client library
```

##### Unity

``` text
ListenerRegistration registration =
db.Collection("cities").Listen(
  querySnapshot =>
  {
      // ...
  });

registration.ListenerTask.ContinueWithOnMainThread(
    listenerTask =>
    {
        if (listenerTask.IsFaulted)
        {
            Debug.LogError($"Listen failed: {listenerTask.Exception}");
            // ...
            // Handle the listener error.
            // ...
        }
    });
```

##### C\#

``` text
// Snippet coming soon
```

##### Ruby

``` ruby
listener = firestore.col(collection_path).listen do |snapshot|
  snapshot.changes.each do |change|
    puts "New city: #{change.doc.document_id}" if change.added?
  end
end

# Register to be notified when unhandled errors occur.
listener.on_error do |error|
  puts "Listen failed: #{error.message}"
endquery_watch.rb
```

## Pricing

Pricing for realtime listener operations depends on the edition of the database. See the following:

  - [Standard edition pricing](https://cloud.google.com/firestore/pricing)
  - [Enterprise edition pricing](https://cloud.google.com/firestore/enterprise/pricing)

## What's next

  - [Combine listeners with simple and compound queries](/firestore/native/docs/query-data/queries) .
  - [Order and limit the documents retrieved](/firestore/native/docs/query-data/order-limit-data) .
  - [Understand billing for listeners](../pricing#operations) .
