# Data model

Firestore is a NoSQL, document-oriented database. Unlike a SQL database, there are no tables or rows. Instead, you store data in *documents* , which are organized into *collections* .

Each *document* contains a set of key-value pairs. Firestore is optimized for storing large collections of small documents.

All documents must be stored in collections. Documents can contain *subcollections* and nested objects, both of which can include primitive fields like strings or complex objects like lists.

Collections and documents are created implicitly in Firestore. Simply assign data to a document within a collection. If either the collection or document does not exist, Firestore creates it.

## Documents

In Firestore, the unit of storage is the document. A document is a lightweight record that contains fields, which map to values. Each document is identified by a name.

A document representing a user `  alovelace  ` might look like this:

  - class alovelace
    
    `  first : "Ada"  `  
    `  last : "Lovelace"  `  
    `  born : 1815  `  

**Note:** Firestore supports a variety of data types for values: boolean, number, string, geo point, binary blob, and timestamp. You can also use arrays or nested objects, called maps, to structure data within a document.

Complex, nested objects in a document are called maps. For example, you could structure the user's name from the example above with a map, like this:

  - class alovelace
    
    `  name :  `  
    `  first : "Ada"  `  
    `  last : "Lovelace"  `  
    `  born : 1815  `  

You may notice that documents look a lot like JSON. In fact, they basically are. There are some differences (for example, documents support extra data types and are limited to the [document size limit](/firestore/quotas#collections_documents_and_fields) ), but in general, you can treat documents as lightweight JSON records.

## Collections

Documents live in collections, which are simply containers for documents. For example, you could have a `  users  ` collection to contain your various users, each represented by a document:

  - collections\_bookmark users
    
      - class alovelace
        
        `  first : "Ada"  `  
        `  last : "Lovelace"  `  
        `  born : 1815  `  
    
      - class aturing
        
        `  first : "Alan"  `  
        `  last : "Turing"  `  
        `  born : 1912  `  

Firestore is schemaless, so you have complete freedom over what fields you put in each document and what data types you store in those fields. Documents within the same collection can all contain different fields or store different types of data in those fields. However, it's a good idea to use the same fields and data types across multiple documents, so that you can query the documents more easily.

A collection contains documents and nothing else. It can't directly contain raw fields with values, and it can't contain other collections. (See [Hierarchical Data](#hierarchical-data) for an explanation of how to structure more complex data in Firestore.)

The names of documents within a collection are unique. You can provide your own keys, such as user IDs, or you can let Firestore create random IDs for you automatically.

You do not need to "create" or "delete" collections. After you create the first document in a collection, the collection exists. If you delete all of the documents in a collection, it no longer exists.

## References

Every document in Firestore is uniquely identified by its location within the database. The previous example showed a document `  alovelace  ` within the collection `  users  ` . To refer to this location in your code, you can create a *reference* to it.

### Web version 9

``` javascript
import { doc } from "firebase/firestore";

const alovelaceDocumentRef = doc(db, 'users', 'alovelace');doc_reference.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var alovelaceDocumentRef = db.collection('users').doc('alovelace');test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let alovelaceDocumentRef = db.collection("users").document("alovelace")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRDocumentReference *alovelaceDocumentRef =
    [[self.db collectionWithPath:@"users"] documentWithPath:@"alovelace"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val alovelaceDocumentRef = db.collection("users").document("alovelace")DocSnippets.kt
```

##### Java  
Android

``` java
DocumentReference alovelaceDocumentRef = db.collection("users").document("alovelace");DocSnippets.java
```

### Dart

``` dart
final alovelaceDocumentRef = db.collection("users").doc("alovelace");firestore.dart
```

##### Java

``` java
// Reference to a document with id "alovelace" in the collection "users"
DocumentReference document = db.collection("users").document("alovelace");References.java
```

##### Python

``` python
a_lovelace_ref = db.collection("users").document("alovelace")snippets.py
```

##### Python  
(Async)

``` python
a_lovelace_ref = db.collection("users").document("alovelace")snippets.py
```

##### C++

``` cpp
DocumentReference alovelace_document_reference =
    db->Collection("users").Document("alovelace");snippets.cpp
```

##### Node.js

``` javascript
const alovelaceDocumentRef = db.collection('users').doc('alovelace');index.js
```

##### Go

``` go
import (
 "cloud.google.com/go/firestore"
)

func createDocReference(client *firestore.Client) {

 alovelaceRef := client.Collection("users").Doc("alovelace")

 _ = alovelaceRef
}
retrieve_data_reference_document.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$document = $db->collection('samples/php/users')->document('alovelace');
```

##### Unity

``` text
DocumentReference documentRef = db.Collection("users").Document("alovelace");
```

##### C\#

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference documentRef = db.Collection("users").Document("alovelace");
```

##### Ruby

``` ruby
document_ref = firestore.col("users").doc("alovelace")data_model.rb
```

A reference is a lightweight object that just points to a location in your database. You can create a reference whether or not data exists there, and creating a reference does not perform any network operations.

You can also create references to *collections* :

### Web version 9

``` javascript
import { collection } from "firebase/firestore";

const usersCollectionRef = collection(db, 'users');collection_reference.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var usersCollectionRef = db.collection('users');test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let usersCollectionRef = db.collection("users")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *usersCollectionRef = [self.db collectionWithPath:@"users"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val usersCollectionRef = db.collection("users")DocSnippets.kt
```

##### Java  
Android

``` java
CollectionReference usersCollectionRef = db.collection("users");DocSnippets.java
```

### Dart

``` dart
final usersCollectionRef = db.collection("users");firestore.dart
```

##### Java

``` java
// Reference to the collection "users"
CollectionReference collection = db.collection("users");References.java
```

##### Python

``` python
users_ref = db.collection("users")snippets.py
```

##### Python  
(Async)

``` python
users_ref = db.collection("users")snippets.py
```

##### C++

``` cpp
CollectionReference users_collection_reference = db->Collection("users");snippets.cpp
```

##### Node.js

``` javascript
const usersCollectionRef = db.collection('users');index.js
```

##### Go

``` go
import (
 "cloud.google.com/go/firestore"
)

func createCollectionReference(client *firestore.Client) {
 usersRef := client.Collection("users")

 _ = usersRef
}
retrieve_data_reference_collection.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$collection = $db->collection('samples/php/users');
```

##### Unity

``` text
CollectionReference collectionRef = db.Collection("users");
```

##### C\#

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
CollectionReference collectionRef = db.Collection("users");
```

##### Ruby

``` ruby
collection_ref = firestore.col "users"data_model.rb
```

**Note:** *Collection references* and *document references* are two distinct types of references and let you perform different operations. For example, you could use a collection reference for querying the documents in the collection, and you could use a document reference to read or write an individual document.

For convenience, you can also create references by specifying the path to a document or collection as a string, with path components separated by a forward slash ( `  /  ` ). For example, to create a reference to the `  alovelace  ` document:

### Web version 9

``` javascript
import { doc } from "firebase/firestore"; 

const alovelaceDocumentRef = doc(db, 'users/alovelace');doc_reference_alternative.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var alovelaceDocumentRef = db.doc('users/alovelace');test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let aLovelaceDocumentReference = db.document("users/alovelace")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRDocumentReference *aLovelaceDocumentReference =
    [self.db documentWithPath:@"users/alovelace"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val alovelaceDocumentRef = db.document("users/alovelace")DocSnippets.kt
```

##### Java  
Android

``` java
DocumentReference alovelaceDocumentRef = db.document("users/alovelace");DocSnippets.java
```

### Dart

``` dart
final aLovelaceDocRef = db.doc("users/alovelace");firestore.dart
```

##### Java

``` java
// Reference to a document with id "alovelace" in the collection "users"
DocumentReference document = db.document("users/alovelace");References.java
```

##### Python

``` python
a_lovelace_ref = db.document("users/alovelace")snippets.py
```

##### Python  
(Async)

``` python
a_lovelace_ref = db.document("users/alovelace")snippets.py
```

##### C++

``` cpp
DocumentReference alovelace_document = db->Document("users/alovelace");snippets.cpp
```

##### Node.js

``` javascript
const alovelaceDocumentRef = db.doc('users/alovelace');index.js
```

##### Go

``` go
import (
 "cloud.google.com/go/firestore"
)

func createDocReferenceFromString(client *firestore.Client) {
 // Reference to a document with id "alovelace" in the collection "users"
 alovelaceRef := client.Doc("users/alovelace")

 _ = alovelaceRef
}
retrieve_data_reference_document_path.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$document = $db->document('users/alovelace');
```

##### Unity

``` text
DocumentReference documentRef = db.Document("users/alovelace");
```

##### C\#

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference documentRef = db.Document("users/alovelace");
```

##### Ruby

``` ruby
document_path_ref = firestore.doc "users/alovelace"data_model.rb
```

## Hierarchical Data

To understand how hierarchical data structures work in Firestore, consider an example chat app with messages and chat rooms.

You can create a collection called `  rooms  ` to store different chat rooms:

  - collections\_bookmark rooms
    
      - class roomA
        
        `  name : "my chat room"  `  
    
      - class roomB
        
        `  ...  `  

Now that you have chat rooms, decide how to store your messages. You might not want to store them in the chat room's document. Documents in Firestore should be lightweight, and a chat room could contain a large number of messages. However, you can create additional collections within your chat room's document, as subcollections.

### Subcollections

The best way to store messages in this scenario is by using subcollections. A subcollection is a collection associated with a specific document.

**Note:** You can query across subcollections with the same collection ID by using [Collection Group Queries](/firestore/native/docs/query-data/queries#collection-group-query) .

You can create a subcollection called `  messages  ` for every room document in your `  rooms  ` collection:

  - collections\_bookmark rooms
    
      - class roomA
        
        `  name : "my chat room"  `  
        
          - collections\_bookmark messages
            
              - class message1
                
                `  from : "alex"  `  
                `  msg : "Hello World!"  `  
            
              - class message2
                
                `  ...  `  
    
      - class roomB
        
        `  ...  `  

In this example, you would create a reference to a message in the subcollection with the following code:

### Web version 9

``` javascript
import { doc } from "firebase/firestore"; 

const messageRef = doc(db, "rooms", "roomA", "messages", "message1");subcollection_reference.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var messageRef = db.collection('rooms').doc('roomA')
                .collection('messages').doc('message1');test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let messageRef = db
  .collection("rooms").document("roomA")
  .collection("messages").document("message1")ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRDocumentReference *messageRef =
    [[[[self.db collectionWithPath:@"rooms"] documentWithPath:@"roomA"]
    collectionWithPath:@"messages"] documentWithPath:@"message1"];ViewController.m
```

##### Kotlin  
Android

``` kotlin
val messageRef = db
    .collection("rooms").document("roomA")
    .collection("messages").document("message1")DocSnippets.kt
```

##### Java  
Android

``` java
DocumentReference messageRef = db
        .collection("rooms").document("roomA")
        .collection("messages").document("message1");DocSnippets.java
```

### Dart

``` dart
final messageRef = db
    .collection("rooms")
    .doc("roomA")
    .collection("messages")
    .doc("message1");firestore.dart
```

##### Java

``` java
// Reference to a document in subcollection "messages"
DocumentReference document =
    db.collection("rooms").document("roomA").collection("messages").document("message1");References.java
```

##### Python

``` python
room_a_ref = db.collection("rooms").document("roomA")
message_ref = room_a_ref.collection("messages").document("message1")snippets.py
```

##### Python  
(Async)

``` python
room_a_ref = db.collection("rooms").document("roomA")
message_ref = room_a_ref.collection("messages").document("message1")snippets.py
```

##### C++

``` cpp
DocumentReference message_reference = db->Collection("rooms")
    .Document("roomA")
    .Collection("messages")
    .Document("message1");snippets.cpp
```

##### Node.js

``` javascript
const messageRef = db.collection('rooms').doc('roomA')
  .collection('messages').doc('message1');index.js
```

##### Go

``` go
import (
 "cloud.google.com/go/firestore"
)

func createSubcollectionReference(client *firestore.Client) {
 messageRef := client.Collection("rooms").Doc("roomA").
     Collection("messages").Doc("message1")

 _ = messageRef
}
retrieve_data_reference_subcollection.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$document = $db
    ->collection('rooms')
    ->document('roomA')
    ->collection('messages')
    ->document('message1');
```

##### Unity

``` text
DocumentReference documentRef = db
 .Collection("Rooms").Document("RoomA")
 .Collection("Messages").Document("Message1");
```

##### C\#

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
DocumentReference documentRef = db
    .Collection("Rooms").Document("RoomA")
    .Collection("Messages").Document("Message1");
```

##### Ruby

``` ruby
message_ref = firestore.col("rooms").doc("roomA").col("messages").doc("message1")data_model.rb
```

Notice the alternating pattern of collections and documents. Your collections and documents must always follow this pattern. You cannot reference a collection in a collection or a document in a document.

Subcollections allow you to structure data hierarchically, making data easier to access. To get all messages in `  roomA  ` , you can create a collection reference to the subcollection `  messages  ` and interact with it like you would any other collection reference.

Documents in subcollections can contain subcollections as well, allowing you to further nest data. You can nest data up to 100 levels deep.

**Warning:** Deleting a document does not delete its subcollections\!  
  
When you delete a document that has subcollections, those subcollections are not deleted. For example, there may be a document located at `  coll/doc/subcoll/subdoc  ` even though the document `  coll/doc  ` no longer exists. If you want to delete documents in subcollections when deleting a parent document, you must do so manually, as shown in [Delete Collections](/firestore/native/docs/manage-data/delete-data#collections) .
