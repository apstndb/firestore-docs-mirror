# Create a Firestore database by using a web or mobile client library

This quickstart shows you how to set up Firestore, add data, and read data by using the Android, Apple platforms, Web, Unity, or C++ client library.

**Note:** This quickstart uses the Firebase console instead of the Google Cloud console.

1.  If you haven't already, create a Firebase project: In the [Firebase console](//console.firebase.google.com) , click **Add project** , then follow the on-screen instructions to create a Firebase project or to add Firebase services to an existing Google Cloud project.

2.  Open your project in the Firebase console. In the left panel, expand **Build** and then select [**Firestore database**](https://console.firebase.google.com/project/_/firestore/) .

3.  Click **Create database** .

4.  Select a [location](/firestore/docs/locations#types) for your database.
    
    If you aren't able to select a location, then your project's ["location for default Google Cloud resources"](/firestore/docs/locations#default-cloud-location) has already been set. Some of your project's resources (like the default Firestore instance) share a common location dependency, and their location can be set either during project creation or when setting up another service that shares this location dependency.

5.  Select a starting mode for your Firestore Security Rules:
    
      - Test mode  
        Good for getting started with the mobile and web client libraries, but allows anyone to read and overwrite your data. After testing, **make sure to review the [Secure your data](#secure_your_data) section.**
        
        To get started with the web, Apple platforms, or Android SDK, select test mode.
    
      - Locked mode  
        Denies all reads and writes from mobile and web clients. Your authenticated application servers (C\#, Go, Java, Node.js, PHP, Python, or Ruby) can still access your database.
        
        To get started with the C\#, Go, Java, Node.js, PHP, Python, or Ruby server client library, select locked mode.
    
    Your initial set of Firestore Security Rules will apply to your default Firestore database. If you create multiple databases for your project, you can deploy Firestore Security Rules for each database.

6.  Click **Create** .

**Firestore and App Engine:** You can't use both Firestore and Datastore in the same App Engine app. If you need to use Datastore with App Engine, we recommend that you use Firestore with a different project.

When you enable Firestore, it also enables the API in the [Cloud API Manager](https://console.cloud.google.com/projectselector/apis/api/firestore.googleapis.com/overview) .

## Set up your development environment

Add the required dependencies and client libraries to your app.

### Web version 9

1.  Follow the instructions to [add Firebase to your Web app](//firebase.google.com/docs/web/setup) .

2.  Import both Firebase and Firestore:
    
    ``` text
    import { initializeApp } from "firebase/app";
    import { getFirestore } from "firebase/firestore";
    ```

Looking for a compact Firestore library, and only need simple REST/CRUD capabilities? Try the [Firestore Lite SDK](https://firebase.google.com/docs/firestore/solutions/firestore-lite) , available only via npm.

### Web version 8

1.  Follow the instructions to [add Firebase to your Web app](//firebase.google.com/docs/web/setup) .

2.  Add the Firebase and Firestore libraries to your app:
    
    ``` text
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-firestore.js"></script>
    ```
    
    The Firestore SDK is also available as an npm package.
    
    ``` text
    npm install firebase@8.10.1 --save
    ```
    
    You'll need to manually require both Firebase and Firestore.
    
    ``` text
    const firebase = require("firebase");
    // Required for side-effects
    require("firebase/firestore");
    ```

##### Apple platforms

Follow the instructions to [add Firebase to your Apple app](//firebase.google.com/docs/ios/setup) .

Use Swift Package Manager to install and manage Firebase dependencies.

Visit [our installation guide](https://firebase.google.com/docs/ios/installation-methods) to learn about the different ways you can add Firebase SDKs to your Apple project, including importing frameworks directly and using CocoaPods.

1.  In Xcode, with your app project open, navigate to **File \> Swift Packages \> Add Package Dependency** .
2.  When prompted, add the Firebase Apple platforms SDK repository:
3.  Choose the Firestore library.
4.  When finished, Xcode will automatically begin resolving and downloading your dependencies in the background.

##### Android

1.  Follow the instructions to [add Firebase to your Android app](//firebase.google.com/docs/android/setup) .

2.  Declare the dependency for the Firestore library for Android in your module (app-level) Gradle file (usually `  app/build.gradle.kts  ` or `  app/build.gradle  ` ):
    
    ``` text
    implementation("com.google.firebase:firebase-firestore:26.1.0")
    ```
    
    If your app uses multiple Firebase libraries, consider using the [Firebase Android BoM](//firebase.google.com/docs/android/learn-more#bom) , which ensures that your app's Firebase library versions are always compatible.
    
    **Looking for a Kotlin-specific library module?** Starting with the [October 2023 release](//firebase.google.com/support/release-notes/android#2023-10-10) , both Kotlin and Java developers can depend on the main library module (for details, see the [FAQ about this initiative](//firebase.google.com/docs/android/kotlin-migration) ).

### Dart

1.  If you haven't already, [configure and initialize Firebase](https://firebase.google.com/docs/flutter/setup) in your Flutter app.

2.  From the root of your Flutter project, run the following command to install the plugin:
    
    ``` text
    flutter pub add cloud_firestore
    ```

3.  Once complete, rebuild your Flutter application:
    
    ``` text
    flutter run
    ```

##### C++

Follow the instructions to [add Firebase to your C++ project](//firebase.google.com/docs/cpp/setup) .

**C++ interface for Android.**

  - **Gradle dependencies.** Add the following to your module (app-level) Gradle file (usually `  app/build.gradle  ` ):
    
    ``` text
            android.defaultConfig.externalNativeBuild.cmake {
              arguments "-DFIREBASE_CPP_SDK_DIR=$gradle.firebase_cpp_sdk_dir"
            }
    
            apply from: "$gradle.firebase_cpp_sdk_dir/Android/firebase_dependencies.gradle"
            firebaseCpp.dependencies {
              // earlier entries
              auth
              firestore
            }
            
    ```

  - **Binary dependencies.** Similarly, the recommended way to get the binary dependencies is to add the following to your `  CMakeLists.txt  ` file:
    
    ``` text
            add_subdirectory(${FIREBASE_CPP_SDK_DIR} bin/ EXCLUDE_FROM_ALL)
            set(firebase_libs firebase_auth firebase_firestore firebase_app)
            # Replace the target name below with the actual name of your target,
            # for example, "native-lib".
            target_link_libraries(${YOUR_TARGET_NAME_HERE} "${firebase_libs}")
            
    ```

To set up **desktop integration** , see [Add Firebase to your C++ project](//firebase.google.com/docs/cpp/setup#desktop-workflow) .

##### Unity

Follow the instructions to [add Firebase to your Unity project](//firebase.google.com/docs/unity/setup) .

Use the Unity interface to configure your project to minify Android builds.

You must minify the build to avoid the message `  Error while merging dex archives  ` .

  - The option can be found in **Player Settings \> Android \> Publishing Settings \> Minify** .
  - The options may differ in different versions of Unity so refer to the official [Unity documentation](https://docs.unity3d.com/Manual/class-PlayerSettingsAndroid.html#minify) and the [Firebase Unity Build Debug Guide](https://firebase.google.com/docs/unity/build-debug-guide#single_dex_issues_and_minification_mandatory_if_using_cloud_firestore) .
  - If, after enabling minification, the number of referenced methods still exceeds the limit, another option is to enable `  multidex  ` in:
      - `  mainTemplate.gradle  ` if **Custom Gradle Template** under **Player Settings** is enabled
      - or, the module-level `  build.gradle  ` file, if you use Android Studio to build the exported project.

## Initialize Firestore in Native Mode

Initialize an instance of Firestore:

### Web version 9

``` text
// Initialize Firestore through Firebase
import { initializeApp } from "firebase/app"
import { getFirestore } from "firebase/firestore"
const firebaseApp = initializeApp({
  apiKey: '### FIREBASE API KEY ###',
  authDomain: '### FIREBASE AUTH DOMAIN ###',
  projectId: '### CLOUD FIRESTORE PROJECT ID ###'
});

const db = getFirestore();
```

The values for \`initializeApp\` can be found in your web app's [\`firebaseConfig\`](https://support.google.com/firebase/answer/7015592) . To persist data when the device loses its connection, see the [Enable Offline Data](/firestore/native/docs/manage-data/enable-offline) documentation.

### Web version 8

``` text
// Initialize Firestore through Firebase
firebase.initializeApp({
  apiKey: '### FIREBASE API KEY ###',
  authDomain: '### FIREBASE AUTH DOMAIN ###',
  projectId: '### CLOUD FIRESTORE PROJECT ID ###'
});

var db = firebase.firestore();
```

The values for \`initializeApp\` can be found in your web app's [\`firebaseConfig\`](https://support.google.com/firebase/answer/7015592) . To persist data when the device loses its connection, see the [Enable Offline Data](/firestore/native/docs/manage-data/enable-offline) documentation.

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` text
import FirebaseCore
import FirebaseFirestore

FirebaseApp.configure()

let db = Firestore.firestore()AppDelegate.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` text
@import FirebaseCore;
@import FirebaseFirestore;

// Use Firebase library to configure APIs
[FIRApp configure];

FIRFirestore *defaultFirestore = [FIRFirestore firestore];AppDelegate.m
  
```

##### Kotlin  
Android

``` text
  // Access a Firestore instance from your Activity
  val db = Firebase.firestoreDocSnippets.kt
```

##### Java  
Android

``` text
// Access a Firestore instance from your Activity
  FirebaseFirestore db = FirebaseFirestore.getInstance();DocSnippets.java
```

### Dart

``` text
db = FirebaseFirestore.instance;
```

##### C++

``` objective-c++
// Make sure the call to `Create()` happens some time before you call Firestore::GetInstance().
App::Create();
Firestore* db = Firestore::GetInstance();AppDelegate.mm
```

##### Unity

``` text
using Firebase.Firestore;
using Firebase.Extensions;
```

``` text
FirebaseFirestore db = FirebaseFirestore.DefaultInstance;
```

## Add data

Firestore stores data in Documents, which are stored in Collections. Firestore creates collections and documents implicitly the first time you add data to the document. You do not need to explicitly create collections or documents.

Create a new collection and a document using the following example code.

### Web version 9

``` javascript
import { collection, addDoc } from "firebase/firestore"; 

try {
  const docRef = await addDoc(collection(db, "users"), {
    first: "Ada",
    last: "Lovelace",
    born: 1815
  });
  console.log("Document written with ID: ", docRef.id);
} catch (e) {
  console.error("Error adding document: ", e);
}add_ada_lovelace.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("users").add({
    first: "Ada",
    last: "Lovelace",
    born: 1815
})
.then((docRef) => {
    console.log("Document written with ID: ", docRef.id);
})
.catch((error) => {
    console.error("Error adding document: ", error);
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Add a new document with a generated ID
do {
  let ref = try await db.collection("users").addDocument(data: [
    "first": "Ada",
    "last": "Lovelace",
    "born": 1815
  ])
  print("Document added with ID: \(ref.documentID)")
} catch {
  print("Error adding document: \(error)")
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Add a new document with a generated ID
__block FIRDocumentReference *ref =
    [[self.db collectionWithPath:@"users"] addDocumentWithData:@{
      @"first": @"Ada",
      @"last": @"Lovelace",
      @"born": @1815
    } completion:^(NSError * _Nullable error) {
      if (error != nil) {
        NSLog(@"Error adding document: %@", error);
      } else {
        NSLog(@"Document added with ID: %@", ref.documentID);
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Create a new user with a first and last name
val user = hashMapOf(
    "first" to "Ada",
    "last" to "Lovelace",
    "born" to 1815,
)

// Add a new document with a generated ID
db.collection("users")
    .add(user)
    .addOnSuccessListener { documentReference ->
        Log.d(TAG, "DocumentSnapshot added with ID: ${documentReference.id}")
    }
    .addOnFailureListener { e ->
        Log.w(TAG, "Error adding document", e)
    }DocSnippets.kt
```

##### Java  
Android

``` java
// Create a new user with a first and last name
Map<String, Object> user = new HashMap<>();
user.put("first", "Ada");
user.put("last", "Lovelace");
user.put("born", 1815);

// Add a new document with a generated ID
db.collection("users")
        .add(user)
        .addOnSuccessListener(new OnSuccessListener<DocumentReference>() {
            @Override
            public void onSuccess(DocumentReference documentReference) {
                Log.d(TAG, "DocumentSnapshot added with ID: " + documentReference.getId());
            }
        })
        .addOnFailureListener(new OnFailureListener() {
            @Override
            public void onFailure(@NonNull Exception e) {
                Log.w(TAG, "Error adding document", e);
            }
        });DocSnippets.java
```

### Dart

``` dart
// Create a new user with a first and last name
final user = <String, dynamic>{
  "first": "Ada",
  "last": "Lovelace",
  "born": 1815
};

// Add a new document with a generated ID
db.collection("users").add(user).then((DocumentReference doc) =>
    print('DocumentSnapshot added with ID: ${doc.id}'));firestore.dart
```

##### C++

``` cpp
// Add a new document with a generated ID
Future<DocumentReference> user_ref =
    db->Collection("users").Add({{"first", FieldValue::String("Ada")},
                                 {"last", FieldValue::String("Lovelace")},
                                 {"born", FieldValue::Integer(1815)}});

user_ref.OnCompletion([](const Future<DocumentReference>& future) {
  if (future.error() == Error::kErrorOk) {
    std::cout << "DocumentSnapshot added with ID: " << future.result()->id()
              << std::endl;
  } else {
    std::cout << "Error adding document: " << future.error_message() << std::endl;
  }
});snippets.cpp
```

##### Unity

``` text
DocumentReference docRef = db.Collection("users").Document("alovelace");
Dictionary<string, object> user = new Dictionary<string, object>
{
 { "First", "Ada" },
 { "Last", "Lovelace" },
 { "Born", 1815 },
};
docRef.SetAsync(user).ContinueWithOnMainThread(task => {
 Debug.Log("Added data to the alovelace document in the users collection.");
});
```

Now add another document to the `  users  ` collection. Notice that this document includes a key-value pair (middle name) that does not appear in the first document. Documents in a collection can contain different sets of information.

### Web version 9

``` javascript
// Add a second document with a generated ID.
import { addDoc, collection } from "firebase/firestore"; 

try {
  const docRef = await addDoc(collection(db, "users"), {
    first: "Alan",
    middle: "Mathison",
    last: "Turing",
    born: 1912
  });

  console.log("Document written with ID: ", docRef.id);
} catch (e) {
  console.error("Error adding document: ", e);
}add_alan_turing.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
// Add a second document with a generated ID.
db.collection("users").add({
    first: "Alan",
    middle: "Mathison",
    last: "Turing",
    born: 1912
})
.then((docRef) => {
    console.log("Document written with ID: ", docRef.id);
})
.catch((error) => {
    console.error("Error adding document: ", error);
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Add a second document with a generated ID.
do {
  let ref = try await db.collection("users").addDocument(data: [
    "first": "Alan",
    "middle": "Mathison",
    "last": "Turing",
    "born": 1912
  ])
  print("Document added with ID: \(ref.documentID)")
} catch {
  print("Error adding document: \(error)")
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Add a second document with a generated ID.
__block FIRDocumentReference *ref =
    [[self.db collectionWithPath:@"users"] addDocumentWithData:@{
      @"first": @"Alan",
      @"middle": @"Mathison",
      @"last": @"Turing",
      @"born": @1912
    } completion:^(NSError * _Nullable error) {
      if (error != nil) {
        NSLog(@"Error adding document: %@", error);
      } else {
        NSLog(@"Document added with ID: %@", ref.documentID);
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Create a new user with a first, middle, and last name
val user = hashMapOf(
    "first" to "Alan",
    "middle" to "Mathison",
    "last" to "Turing",
    "born" to 1912,
)

// Add a new document with a generated ID
db.collection("users")
    .add(user)
    .addOnSuccessListener { documentReference ->
        Log.d(TAG, "DocumentSnapshot added with ID: ${documentReference.id}")
    }
    .addOnFailureListener { e ->
        Log.w(TAG, "Error adding document", e)
    }DocSnippets.kt
```

##### Java  
Android

``` java
// Create a new user with a first, middle, and last name
Map<String, Object> user = new HashMap<>();
user.put("first", "Alan");
user.put("middle", "Mathison");
user.put("last", "Turing");
user.put("born", 1912);

// Add a new document with a generated ID
db.collection("users")
        .add(user)
        .addOnSuccessListener(new OnSuccessListener<DocumentReference>() {
            @Override
            public void onSuccess(DocumentReference documentReference) {
                Log.d(TAG, "DocumentSnapshot added with ID: " + documentReference.getId());
            }
        })
        .addOnFailureListener(new OnFailureListener() {
            @Override
            public void onFailure(@NonNull Exception e) {
                Log.w(TAG, "Error adding document", e);
            }
        });DocSnippets.java
```

### Dart

``` dart
// Create a new user with a first and last name
final user = <String, dynamic>{
  "first": "Alan",
  "middle": "Mathison",
  "last": "Turing",
  "born": 1912
};

// Add a new document with a generated ID
db.collection("users").add(user).then((DocumentReference doc) =>
    print('DocumentSnapshot added with ID: ${doc.id}'));firestore.dart
```

##### C++

``` cpp
db->Collection("users")
    .Add({{"first", FieldValue::String("Alan")},
          {"middle", FieldValue::String("Mathison")},
          {"last", FieldValue::String("Turing")},
          {"born", FieldValue::Integer(1912)}})
    .OnCompletion([](const Future<DocumentReference>& future) {
      if (future.error() == Error::kErrorOk) {
        std::cout << "DocumentSnapshot added with ID: "
                  << future.result()->id() << std::endl;
      } else {
        std::cout << "Error adding document: " << future.error_message()
                  << std::endl;
      }
    });snippets.cpp
```

##### Unity

``` text
DocumentReference docRef = db.Collection("users").Document("aturing");
Dictionary<string, object> user = new Dictionary<string, object>
{
 { "First", "Alan" },
 { "Middle", "Mathison" },
 { "Last", "Turing" },
 { "Born", 1912 }
};
docRef.SetAsync(user).ContinueWithOnMainThread(task => {
 Debug.Log("Added data to the aturing document in the users collection.");
});
```

## Read data

Use the data viewer in the [Firebase console](https://console.firebase.google.com/project/_/firestore/data) to quickly verify that you've added data to Firestore.

You can also use the `  get  ` method to retrieve the entire collection.

### Web version 9

``` javascript
import { collection, getDocs } from "firebase/firestore"; 

const querySnapshot = await getDocs(collection(db, "users"));
querySnapshot.forEach((doc) => {
  console.log(`${doc.id} => ${doc.data()}`);
});get_all_users.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
db.collection("users").get().then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(`${doc.id} => ${doc.data()}`);
    });
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
do {
  let snapshot = try await db.collection("users").getDocuments()
  for document in snapshot.documents {
    print("\(document.documentID) => \(document.data())")
  }
} catch {
  print("Error getting documents: \(error)")
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[self.db collectionWithPath:@"users"]
    getDocumentsWithCompletion:^(FIRQuerySnapshot * _Nullable snapshot,
                                 NSError * _Nullable error) {
      if (error != nil) {
        NSLog(@"Error getting documents: %@", error);
      } else {
        for (FIRDocumentSnapshot *document in snapshot.documents) {
          NSLog(@"%@ => %@", document.documentID, document.data);
        }
      }
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
db.collection("users")
    .get()
    .addOnSuccessListener { result ->
        for (document in result) {
            Log.d(TAG, "${document.id} => ${document.data}")
        }
    }
    .addOnFailureListener { exception ->
        Log.w(TAG, "Error getting documents.", exception)
    }DocSnippets.kt
```

##### Java  
Android

``` java
db.collection("users")
        .get()
        .addOnCompleteListener(new OnCompleteListener<QuerySnapshot>() {
            @Override
            public void onComplete(@NonNull Task<QuerySnapshot> task) {
                if (task.isSuccessful()) {
                    for (QueryDocumentSnapshot document : task.getResult()) {
                        Log.d(TAG, document.getId() + " => " + document.getData());
                    }
                } else {
                    Log.w(TAG, "Error getting documents.", task.getException());
                }
            }
        });DocSnippets.java
```

### Dart

``` dart
await db.collection("users").get().then((event) {
  for (var doc in event.docs) {
    print("${doc.id} => ${doc.data()}");
  }
});firestore.dart
```

##### C++

``` cpp
Future<QuerySnapshot> users = db->Collection("users").Get();
users.OnCompletion([](const Future<QuerySnapshot>& future) {
  if (future.error() == Error::kErrorOk) {
    for (const DocumentSnapshot& document : future.result()->documents()) {
      std::cout << document << std::endl;
    }
  } else {
    std::cout << "Error getting documents: " << future.error_message()
              << std::endl;
  }
});snippets.cpp
```

##### Unity

``` text
CollectionReference usersRef = db.Collection("users");
usersRef.GetSnapshotAsync().ContinueWithOnMainThread(task =>
{
  QuerySnapshot snapshot = task.Result;
  foreach (DocumentSnapshot document in snapshot.Documents)
  {
    Debug.Log(String.Format("User: {0}", document.Id));
    Dictionary<string, object> documentDictionary = document.ToDictionary();
    Debug.Log(String.Format("First: {0}", documentDictionary["First"]));
    if (documentDictionary.ContainsKey("Middle"))
    {
      Debug.Log(String.Format("Middle: {0}", documentDictionary["Middle"]));
    }

    Debug.Log(String.Format("Last: {0}", documentDictionary["Last"]));
    Debug.Log(String.Format("Born: {0}", documentDictionary["Born"]));
  }

  Debug.Log("Read all data from the users collection.");
});
```

## Secure your data

Use [Firebase Authentication](//firebase.google.com/docs/auth/) and [Firestore Security Rules](/firestore/native/docs/security/get-started) to secure your data in Firestore in Native Mode.

Here are some basic rule sets you can use to get started. You can modify your security rules in the [**Rules tab**](https://console.firebase.google.com/project/_/firestore/rules) of the Firebase console.

### Auth required

``` text
// Allow read/write access on all documents to any user signed in to the application
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### Locked mode

``` text
// Deny read/write access to all users under any conditions
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

### Test mode

``` text
// Allow read/write access to all users under any conditions
// Warning: **NEVER** use this rule set in production; it allows
// anyone to overwrite your entire database.
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

Before you deploy your Web, Android, or iOS app to production, also take steps to ensure that only your app clients can access your Firestore in Native Mode data. See the [App Check](https://firebase.google.com/docs/app-check) documentation.

## Watch a video tutorial

For detailed guidance on getting started with the Firestore mobile and web client libraries, watch one of the following video tutorials:

##### Web

##### iOS

##### Android

You can find more videos in the Firebase [YouTube channel](https://www.youtube.com/firebase) .

## Next steps

Deepen your knowledge with the following topics:

  - **Codelabs** — Learn to use Firestore in Native Mode in a real app by following the codelab for [Android](https://codelabs.developers.google.com/codelabs/firestore-android) , [iOS](https://codelabs.developers.google.com/codelabs/firestore-ios) , or [Web](https://codelabs.developers.google.com/codelabs/firestore-web) .
  - **[Data model](/firestore/native/docs/data-model)** — Learn more about how data is structured in Firestore, including hierarchical data and subcollections.
  - **[Add data](/firestore/native/docs/manage-data/add-data)** — Learn more about creating and updating data in Firestore.
  - **[Get data](/firestore/native/docs/query-data/get-data)** — Learn more about how to retrieve data.
  - **[Perform simple and compound queries](/firestore/native/docs/query-data/queries)** — Learn how to run simple and compound queries.
  - **[Order and limit queries](/firestore/native/docs/query-data/order-limit-data)** — Learn how to order and limit the data returned by your queries.
