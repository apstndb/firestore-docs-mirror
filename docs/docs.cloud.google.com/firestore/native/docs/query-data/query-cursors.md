# Paginate data with query cursors

**Tip:** This page applies to the Core operations interface. To paginate results with the Pipeline operations interface for Enterprise edition, see [paginate results with Pipeline operations](/firestore/native/docs/pipeline/overview#pagination) .

With query cursors in Firestore, you can split data returned by a query into batches according to the parameters you define in your query.

Query cursors define the start and end points for a query, allowing you to:

  - Return a subset of the data.
  - Paginate query results.

However, to define a specific range for a query, you should use the `  where()  ` method described in [Simple Queries](/firestore/native/docs/query-data/queries#simple_queries) .

## Add a simple cursor to a query

Use the `  startAt()  ` or `  startAfter()  ` methods to define the start point for a query. The `  startAt()  ` method includes the start point, while the `  startAfter()  ` method excludes it.

For example, if you use `  startAt(A)  ` in a query, it returns the entire alphabet. If you use `  startAfter(A)  ` instead, it returns `  B-Z  ` .

### Web version 9

``` javascript
import { query, orderBy, startAt } from "firebase/firestore";  

const q = query(citiesRef, orderBy("population"), startAt(1000000));order_and_start.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.orderBy("population").startAt(1000000);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Get all cities with population over one million, ordered by population.
db.collection("cities")
  .order(by: "population")
  .start(at: [1000000])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Get all cities with population over one million, ordered by population.
[[[db collectionWithPath:@"cities"]
    queryOrderedByField:@"population"]
    queryStartingAtValues:@[ @1000000 ]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Get all cities with a population >= 1,000,000, ordered by population,
db.collection("cities")
    .orderBy("population")
    .startAt(1000000)DocSnippets.kt
```

##### Java  
Android

``` java
// Get all cities with a population >= 1,000,000, ordered by population,
db.collection("cities")
        .orderBy("population")
        .startAt(1000000);DocSnippets.java
```

### Dart

``` dart
db.collection("cities").orderBy("population").startAt([1000000]);firestore.dart
```

##### Java

``` java
Query query = cities.orderBy("population").startAt(4921000L);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
query_start_at = cities_ref.order_by("population").start_at({"population": 1000000})snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
query_start_at = cities_ref.order_by("population").start_at({"population": 1000000})snippets.py
```

##### C++

``` cpp
// Get all cities with a population >= 1,000,000, ordered by population,
db->Collection("cities")
    .OrderBy("population")
    .StartAt({FieldValue::Integer(1000000)});snippets.cpp
```

##### Node.js

``` javascript
const startAtRes = await db.collection('cities')
  .orderBy('population')
  .startAt(1000000)
  .get();index.js
```

##### Go

``` go
query := client.Collection("cities").OrderBy("population", firestore.Asc).StartAt(1000000)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef
    ->orderBy('population')
    ->startAt([1000000]);
```

##### Unity

``` text
Query query = citiesRef.OrderBy("Population").StartAt(1000000);
```

##### C\#

``` csharp
Query query = citiesRef.OrderBy("Population").StartAt(1000000);Program.cs
```

##### Ruby

``` ruby
query = cities_ref.order("population").start_at(1_000_000)paginate_data.rb
```

Similarly, use the `  endAt()  ` or `  endBefore()  ` methods to define an end point for your query results.

### Web version 9

``` javascript
import { query, orderBy, endAt } from "firebase/firestore";  

const q = query(citiesRef, orderBy("population"), endAt(1000000));order_and_end.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.orderBy("population").endAt(1000000);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Get all cities with population less than one million, ordered by population.
db.collection("cities")
  .order(by: "population")
  .end(at: [1000000])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Get all cities with population less than one million, ordered by population.
[[[db collectionWithPath:@"cities"]
    queryOrderedByField:@"population"]
    queryEndingAtValues:@[ @1000000 ]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Get all cities with a population <= 1,000,000, ordered by population,
db.collection("cities")
    .orderBy("population")
    .endAt(1000000)DocSnippets.kt
```

##### Java  
Android

``` java
// Get all cities with a population <= 1,000,000, ordered by population,
db.collection("cities")
        .orderBy("population")
        .endAt(1000000);DocSnippets.java
```

### Dart

``` dart
db.collection("cities").orderBy("population").endAt([1000000]);firestore.dart
```

##### Java

``` java
Query query = cities.orderBy("population").endAt(4921000L);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
query_end_at = cities_ref.order_by("population").end_at({"population": 1000000})snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
query_end_at = cities_ref.order_by("population").end_at({"population": 1000000})snippets.py
```

##### C++

``` cpp
// Get all cities with a population <= 1,000,000, ordered by population,
db->Collection("cities")
    .OrderBy("population")
    .EndAt({FieldValue::Integer(1000000)});snippets.cpp
```

##### Node.js

``` javascript
const endAtRes = await db.collection('cities')
  .orderBy('population')
  .endAt(1000000)
  .get();index.js
```

##### Go

``` go
query := client.Collection("cities").OrderBy("population", firestore.Asc).EndAt(1000000)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef
    ->orderBy('population')
    ->endAt([1000000]);
```

##### Unity

``` text
Query query = citiesRef.OrderBy("Population").EndAt(1000000);
```

##### C\#

``` csharp
Query query = citiesRef.OrderBy("Population").EndAt(1000000);Program.cs
```

##### Ruby

``` ruby
query = cities_ref.order("population").end_at(1_000_000)paginate_data.rb
```

## Use a document snapshot to define the query cursor

You can also pass a document snapshot to the cursor clause as the start or end point of the query cursor. The values in the document snapshot serve as the values in the query cursor.

For example, take a snapshot of a "San Francisco" document in your data set of cities and populations. Then, use that document snapshot as the start point for your population query cursor. Your query will return all the cities with a population larger than or equal to San Francisco's, as defined in the document snapshot.

### Web version 9

``` javascript
import { collection, doc, getDoc, query, orderBy, startAt } from "firebase/firestore";  
const citiesRef = collection(db, "cities");

const docSnap = await getDoc(doc(citiesRef, "SF"));

// Get all cities with a population bigger than San Francisco
const biggerThanSf = query(citiesRef, orderBy("population"), startAt(docSnap));
// ...start_doc.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var citiesRef = db.collection("cities");

return citiesRef.doc("SF").get().then((doc) => {
    // Get all cities with a population bigger than San Francisco
    var biggerThanSf = citiesRef
        .orderBy("population")
        .startAt(doc);

    // ...
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
db.collection("cities")
  .document("SF")
  .addSnapshotListener { (document, error) in
    guard let document = document else {
      print("Error retreving cities: \(error.debugDescription)")
      return
    }

    // Get all cities with a population greater than or equal to San Francisco.
    let sfSizeOrBigger = db.collection("cities")
      .order(by: "population")
      .start(atDocument: document)
  }ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[db collectionWithPath:@"cities"] documentWithPath:@"SF"]
    addSnapshotListener:^(FIRDocumentSnapshot *snapshot, NSError *error) {
      if (snapshot == nil) {
        NSLog(@"Error retreiving cities: %@", error);
        return;
      }
      // Get all cities with a population greater than or equal to San Francisco.
      FIRQuery *sfSizeOrBigger = [[[db collectionWithPath:@"cities"]
          queryOrderedByField:@"population"]
          queryStartingAtDocument:snapshot];
    }];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Get the data for "San Francisco"
db.collection("cities").document("SF")
    .get()
    .addOnSuccessListener { documentSnapshot ->
        // Get all cities with a population bigger than San Francisco.
        val biggerThanSf = db.collection("cities")
            .orderBy("population")
            .startAt(documentSnapshot)

        // ...
    }DocSnippets.kt
```

##### Java  
Android

``` java
// Get the data for "San Francisco"
db.collection("cities").document("SF")
        .get()
        .addOnSuccessListener(new OnSuccessListener<DocumentSnapshot>() {
            @Override
            public void onSuccess(DocumentSnapshot documentSnapshot) {
                // Get all cities with a population bigger than San Francisco.
                Query biggerThanSf = db.collection("cities")
                        .orderBy("population")
                        .startAt(documentSnapshot);

                // ...
            }
        });DocSnippets.java
```

### Dart

``` dart
db.collection("cities").doc("SF").get().then(
  (documentSnapshot) {
    final biggerThanSf = db
        .collection("cities")
        .orderBy("population")
        .startAtDocument(documentSnapshot);
  },
  onError: (e) => print("Error: $e"),
);firestore.dart
```

##### Java

``` java
// Fetch the snapshot with an API call, waiting for a maximum of 30 seconds for a result.
ApiFuture<DocumentSnapshot> future = db.collection("cities").document("SF").get();
DocumentSnapshot snapshot = future.get(30, TimeUnit.SECONDS);

// Construct the query
Query query = db.collection("cities").orderBy("population").startAt(snapshot);QueryDataSnippets.java
```

##### Python

``` python
doc_ref = db.collection("cities").document("SF")

snapshot = doc_ref.get()
start_at_snapshot = (
    db.collection("cities").order_by("population").start_at(snapshot)
)snippets.py
```

##### Python  
(Async)

``` python
doc_ref = db.collection("cities").document("SF")

snapshot = await doc_ref.get()
start_at_snapshot = (
    db.collection("cities").order_by("population").start_at(snapshot)
)snippets.py
```

##### C++

``` cpp
db->Collection("cities").Document("SF").Get().OnCompletion(
    [db](const Future<DocumentSnapshot>& future) {
      if (future.error() == Error::kErrorOk) {
        const DocumentSnapshot& document_snapshot = *future.result();
        Query bigger_than_sf = db->Collection("cities")
                                   .OrderBy("population")
                                   .StartAt({document_snapshot});
        // ...
      }
    });snippets.cpp
```

##### Node.js

``` javascript
const docRef = db.collection('cities').doc('SF');
const snapshot = await docRef.get();
const startAtSnapshot = db.collection('cities')
  .orderBy('population')
  .startAt(snapshot);

await startAtSnapshot.limit(10).get();index.js
```

##### Go

``` go
cities := client.Collection("cities")
dsnap, err := cities.Doc("SF").Get(ctx)
if err != nil {
 fmt.Println(err)
}
query := cities.OrderBy("population", firestore.Asc).StartAt(dsnap.Data()["population"]).Documents(ctx)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$docRef = $citiesRef->document('SF');
$snapshot = $docRef->snapshot();

$query = $citiesRef
    ->orderBy('population')
    ->startAt($snapshot);
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
DocumentReference docRef = citiesRef.Document("SF");
docRef.GetSnapshotAsync().ContinueWith((snapshotTask) =>
{
    Query query = citiesRef.OrderBy("Population").StartAt(snapshotTask.Result);
});
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
DocumentReference docRef = citiesRef.Document("SF");
DocumentSnapshot snapshot = await docRef.GetSnapshotAsync();
Query query = citiesRef.OrderBy("Population").StartAt(snapshot);Program.cs
```

##### Ruby

``` ruby
doc_ref = firestore.doc "#{collection_path}/SF"
snapshot = doc_ref.get
query = cities_ref.order("population").start_at(snapshot)paginate_data.rb
```

## Paginate a query

Paginate queries by combining query cursors with the `  limit()  ` method. For example, use the last document in a batch as the start of a cursor for the next batch.

### Web version 9

``` javascript
import { collection, query, orderBy, startAfter, limit, getDocs } from "firebase/firestore";  

// Query the first page of docs
const first = query(collection(db, "cities"), orderBy("population"), limit(25));
const documentSnapshots = await getDocs(first);

// Get the last visible document
const lastVisible = documentSnapshots.docs[documentSnapshots.docs.length-1];
console.log("last", lastVisible);

// Construct a new query starting at this document,
// get the next 25 cities.
const next = query(collection(db, "cities"),
    orderBy("population"),
    startAfter(lastVisible),
    limit(25));paginate.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
var first = db.collection("cities")
        .orderBy("population")
        .limit(25);

return first.get().then((documentSnapshots) => {
  // Get the last visible document
  var lastVisible = documentSnapshots.docs[documentSnapshots.docs.length-1];
  console.log("last", lastVisible);

  // Construct a new query starting at this document,
  // get the next 25 cities.
  var next = db.collection("cities")
          .orderBy("population")
          .startAfter(lastVisible)
          .limit(25);
});test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Construct query for first 25 cities, ordered by population
let first = db.collection("cities")
  .order(by: "population")
  .limit(to: 25)

first.addSnapshotListener { (snapshot, error) in
  guard let snapshot = snapshot else {
    print("Error retreving cities: \(error.debugDescription)")
    return
  }

  guard let lastSnapshot = snapshot.documents.last else {
    // The collection is empty.
    return
  }

  // Construct a new query starting after this document,
  // retrieving the next 25 cities.
  let next = db.collection("cities")
    .order(by: "population")
    .start(afterDocument: lastSnapshot)

  // Use the query for pagination.
  // ...
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *first = [[[db collectionWithPath:@"cities"]
    queryOrderedByField:@"population"]
    queryLimitedTo:25];
[first addSnapshotListener:^(FIRQuerySnapshot *snapshot, NSError *error) {
  if (snapshot == nil) {
    NSLog(@"Error retreiving cities: %@", error);
    return;
  }
  if (snapshot.documents.count == 0) { return; }
  FIRDocumentSnapshot *lastSnapshot = snapshot.documents.lastObject;

  // Construct a new query starting after this document,
  // retreiving the next 25 cities.
  FIRQuery *next = [[[db collectionWithPath:@"cities"]
      queryOrderedByField:@"population"]
      queryStartingAfterDocument:lastSnapshot];
  // Use the query for pagination.
  // ...
}];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Construct query for first 25 cities, ordered by population
val first = db.collection("cities")
    .orderBy("population")
    .limit(25)

first.get()
    .addOnSuccessListener { documentSnapshots ->
        // ...

        // Get the last visible document
        val lastVisible = documentSnapshots.documents[documentSnapshots.size() - 1]

        // Construct a new query starting at this document,
        // get the next 25 cities.
        val next = db.collection("cities")
            .orderBy("population")
            .startAfter(lastVisible)
            .limit(25)

        // Use the query for pagination
        // ...
    }DocSnippets.kt
```

##### Java  
Android

``` java
// Construct query for first 25 cities, ordered by population
Query first = db.collection("cities")
        .orderBy("population")
        .limit(25);

first.get()
    .addOnSuccessListener(new OnSuccessListener<QuerySnapshot>() {
        @Override
        public void onSuccess(QuerySnapshot documentSnapshots) {
            // ...

            // Get the last visible document
            DocumentSnapshot lastVisible = documentSnapshots.getDocuments()
                    .get(documentSnapshots.size() -1);

            // Construct a new query starting at this document,
            // get the next 25 cities.
            Query next = db.collection("cities")
                    .orderBy("population")
                    .startAfter(lastVisible)
                    .limit(25);

            // Use the query for pagination
            // ...
        }
    });DocSnippets.java
```

### Dart

``` dart
// Construct query for first 25 cities, ordered by population
final first = db.collection("cities").orderBy("population").limit(25);

first.get().then(
  (documentSnapshots) {
    // Get the last visible document
    final lastVisible = documentSnapshots.docs[documentSnapshots.size - 1];

    // Construct a new query starting at this document,
    // get the next 25 cities.
    final next = db
        .collection("cities")
        .orderBy("population")
        .startAfterDocument(lastVisible)
        .limit(25);

    // Use the query for pagination
    // ...
  },
  onError: (e) => print("Error completing: $e"),
);firestore.dart
```

##### Java

``` java
// Construct query for first 25 cities, ordered by population.
CollectionReference cities = db.collection("cities");
Query firstPage = cities.orderBy("population").limit(25);

// Wait for the results of the API call, waiting for a maximum of 30 seconds for a result.
ApiFuture<QuerySnapshot> future = firstPage.get();
List<QueryDocumentSnapshot> docs = future.get(30, TimeUnit.SECONDS).getDocuments();

// Construct query for the next 25 cities.
QueryDocumentSnapshot lastDoc = docs.get(docs.size() - 1);
Query secondPage = cities.orderBy("population").startAfter(lastDoc).limit(25);

future = secondPage.get();
docs = future.get(30, TimeUnit.SECONDS).getDocuments();QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
first_query = cities_ref.order_by("population").limit(3)

# Get the last document from the results
docs = first_query.stream()
last_doc = list(docs)[-1]

# Construct a new query starting at this document
# Note: this will not have the desired effect if
# multiple cities have the exact same population value
last_pop = last_doc.to_dict()["population"]

next_query = (
    cities_ref.order_by("population").start_after({"population": last_pop}).limit(3)
)
# Use the query for pagination
# ...snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
first_query = cities_ref.order_by("population").limit(3)

# Get the last document from the results
docs = [d async for d in first_query.stream()]
last_doc = list(docs)[-1]

# Construct a new query starting at this document
# Note: this will not have the desired effect if
# multiple cities have the exact same population value
last_pop = last_doc.to_dict()["population"]

next_query = (
    cities_ref.order_by("population").start_after({"population": last_pop}).limit(3)
)
# Use the query for pagination
# ...snippets.py
```

##### C++

``` cpp
// Construct query for first 25 cities, ordered by population
Query first = db->Collection("cities").OrderBy("population").Limit(25);

first.Get().OnCompletion([db](const Future<QuerySnapshot>& future) {
  if (future.error() != Error::kErrorOk) {
    // Handle error...
    return;
  }

  // Get the last visible document
  const QuerySnapshot& document_snapshots = *future.result();
  std::vector<DocumentSnapshot> documents = document_snapshots.documents();
  const DocumentSnapshot& last_visible = documents.back();

  // Construct a new query starting at this document,
  // get the next 25 cities.
  Query next = db->Collection("cities")
                   .OrderBy("population")
                   .StartAfter(last_visible)
                   .Limit(25);

  // Use the query for pagination
  // ...
});snippets.cpp
```

##### Node.js

``` javascript
const first = db.collection('cities')
  .orderBy('population')
  .limit(3);

const snapshot = await first.get();

// Get the last document
const last = snapshot.docs[snapshot.docs.length - 1];

// Construct a new query starting at this document.
// Note: this will not have the desired effect if multiple
// cities have the exact same population value.
const next = db.collection('cities')
  .orderBy('population')
  .startAfter(last.data().population)
  .limit(3);

// Use the query for pagination
// ...index.js
```

##### Go

``` go
cities := client.Collection("cities")

// Get the first 25 cities, ordered by population.
firstPage := cities.OrderBy("population", firestore.Asc).Limit(25).Documents(ctx)
docs, err := firstPage.GetAll()
if err != nil {
 return err
}

// Get the last document.
lastDoc := docs[len(docs)-1]

// Construct a new query to get the next 25 cities.
secondPage := cities.OrderBy("population", firestore.Asc).
 StartAfter(lastDoc.Data()["population"]).
 Limit(25)

// ...query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$citiesRef = $db->collection('samples/php/cities');
$firstQuery = $citiesRef->orderBy('population')->limit(3);

# Get the last document from the results
$documents = $firstQuery->documents();
$lastPopulation = 0;
foreach ($documents as $document) {
    $lastPopulation = $document['population'];
}

# Construct a new query starting at this document
# Note: this will not have the desired effect if multiple cities have the exact same population value
$nextQuery = $citiesRef->orderBy('population')->startAfter([$lastPopulation]);
$snapshot = $nextQuery->documents();
```

##### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
Query firstQuery = citiesRef.OrderBy("Population").Limit(3);

// Get the last document from the results
firstQuery.GetSnapshotAsync().ContinueWith((querySnapshotTask) =>
{
    long lastPopulation = 0;
    foreach (DocumentSnapshot documentSnapshot in querySnapshotTask.Result.Documents)
    {
        lastPopulation = documentSnapshot.GetValue<long>("Population");
    }

    // Construct a new query starting at this document.
    // Note: this will not have the desired effect if multiple cities have the exact same population value
    Query secondQuery = citiesRef.OrderBy("Population").StartAfter(lastPopulation);
    Task<QuerySnapshot> secondQuerySnapshot = secondQuery.GetSnapshotAsync();
```

##### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query firstQuery = citiesRef.OrderBy("Population").Limit(3);

// Get the last document from the results
QuerySnapshot querySnapshot = await firstQuery.GetSnapshotAsync();
long lastPopulation = 0;
foreach (DocumentSnapshot documentSnapshot in querySnapshot.Documents)
{
    lastPopulation = documentSnapshot.GetValue<long>("Population");
}

// Construct a new query starting at this document.
// Note: this will not have the desired effect if multiple cities have the exact same population value
Query secondQuery = citiesRef.OrderBy("Population").StartAfter(lastPopulation);
QuerySnapshot secondQuerySnapshot = await secondQuery.GetSnapshotAsync();Program.cs
```

##### Ruby

``` ruby
cities_ref  = firestore.col collection_path
first_query = cities_ref.order("population").limit(3)

# Get the last document from the results.
last_population = 0
first_query.get do |city|
  last_population = city.data[:population]
end

# Construct a new query starting at this document.
# Note: this will not have the desired effect if multiple cities have the exact same population value.
second_query = cities_ref.order("population").start_after(last_population)
second_query.get do |city|
  puts "Document #{city.document_id} returned by paginated query cursor."
endpaginate_data.rb
```

## Set cursor based on multiple fields

When using a cursor based on a field value (not a DocumentSnapshot), you can make the cursor position more precise by adding additional fields. This is particularly useful if your data set includes multiple documents that all have the same value for your cursor field, making the cursor's position ambiguous. You can add additional field values to your cursor to further specify the start or end point and reduce ambiguity.

For example, in a data set containing all the cities named "Springfield" in the United States, there would be multiple start points for a query set to start at "Springfield":

Cities

Name

State

Springfield

Massachusetts

Springfield

Missouri

Springfield

Wisconsin

To start at a specific Springfield, you could add the state as a secondary condition in your cursor clause.

### Web version 9

``` javascript
// Will return all Springfields
import { collection, query, orderBy, startAt } from "firebase/firestore";  
const q1 = query(collection(db, "cities"),
   orderBy("name"),
   orderBy("state"),
   startAt("Springfield"));

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
const q2 = query(collection(db, "cities"),
   orderBy("name"),
   orderBy("state"),
   startAt("Springfield", "Missouri"));start_multiple_orderby.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
// Will return all Springfields
db.collection("cities")
   .orderBy("name")
   .orderBy("state")
   .startAt("Springfield");

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
db.collection("cities")
   .orderBy("name")
   .orderBy("state")
   .startAt("Springfield", "Missouri");test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
// Will return all Springfields
db.collection("cities")
  .order(by: "name")
  .order(by: "state")
  .start(at: ["Springfield"])

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
db.collection("cities")
  .order(by: "name")
  .order(by: "state")
  .start(at: ["Springfield", "Missouri"])ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
// Will return all Springfields
[[[[db collectionWithPath:@"cities"]
    queryOrderedByField:@"name"]
    queryOrderedByField:@"state"]
    queryStartingAtValues:@[ @"Springfield" ]];
// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
[[[[db collectionWithPath:@"cities"]
   queryOrderedByField:@"name"]
   queryOrderedByField:@"state"]
   queryStartingAtValues:@[ @"Springfield", @"Missouri" ]];ViewController.m
```

##### Kotlin  
Android

``` kotlin
// Will return all Springfields
db.collection("cities")
    .orderBy("name")
    .orderBy("state")
    .startAt("Springfield")

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
db.collection("cities")
    .orderBy("name")
    .orderBy("state")
    .startAt("Springfield", "Missouri")DocSnippets.kt
```

##### Java  
Android

``` java
// Will return all Springfields
db.collection("cities")
        .orderBy("name")
        .orderBy("state")
        .startAt("Springfield");

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
db.collection("cities")
        .orderBy("name")
        .orderBy("state")
        .startAt("Springfield", "Missouri");DocSnippets.java
```

### Dart

``` dart
// Will return all Springfields
db
    .collection("cities")
    .orderBy("name")
    .orderBy("state")
    .startAt(["Springfield"]);

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
db
    .collection("cities")
    .orderBy("name")
    .orderBy("state")
    .startAt(["Springfield", "Missouri"]);firestore.dart
```

##### Java

``` java
// Will return all Springfields
Query query1 = db.collection("cities").orderBy("name").orderBy("state").startAt("Springfield");

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
Query query2 =
    db.collection("cities").orderBy("name").orderBy("state").startAt("Springfield", "Missouri");QueryDataSnippets.java
```

##### Python

``` python
start_at_name = (
    db.collection("cities").order_by("name").start_at({"name": "Springfield"})
)

start_at_name_and_state = (
    db.collection("cities")
    .order_by("name")
    .order_by("state")
    .start_at({"name": "Springfield", "state": "Missouri"})
)snippets.py
```

##### Python  
(Async)

``` python
start_at_name = (
    db.collection("cities")
    .order_by("name")
    .order_by("state")
    .start_at({"name": "Springfield"})
)

start_at_name_and_state = (
    db.collection("cities")
    .order_by("name")
    .order_by("state")
    .start_at({"name": "Springfield", "state": "Missouri"})
)snippets.py
```

##### C++

``` text
// This is not yet supported.
```

##### Node.js

``` javascript
// Will return all Springfields
const startAtNameRes = await db.collection('cities')
  .orderBy('name')
  .orderBy('state')
  .startAt('Springfield')
  .get();

// Will return 'Springfield, Missouri' and 'Springfield, Wisconsin'
const startAtNameAndStateRes = await db.collection('cities')
  .orderBy('name')
  .orderBy('state')
  .startAt('Springfield', 'Missouri')
  .get();index.js
```

##### Go

``` go
// Will return all Springfields.
client.Collection("cities").
 OrderBy("name", firestore.Asc).
 OrderBy("state", firestore.Asc).
 StartAt("Springfield")

// Will return Springfields where state comes after Wisconsin.
client.Collection("cities").
 OrderBy("name", firestore.Asc).
 OrderBy("state", firestore.Asc).
 StartAt("Springfield", "Wisconsin")query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
// Will return all Springfields
$query1 = $db
    ->collection('samples/php/cities')
    ->orderBy('name')
    ->orderBy('state')
    ->startAt(['Springfield']);

// Will return "Springfield, Missouri" and "Springfield, Wisconsin"
$query2 = $db
    ->collection('samples/php/cities')
    ->orderBy('name')
    ->orderBy('state')
    ->startAt(['Springfield', 'Missouri']);
```

##### Unity

``` text
Query query1 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield");
Query query2 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield", "Missouri");
```

##### C\#

``` csharp
Query query1 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield");
Query query2 = db.Collection("cities").OrderBy("Name").OrderBy("State").StartAt("Springfield", "Missouri");Program.cs
```

##### Ruby

``` ruby
# Will return all Springfields
query1 = firestore.col(collection_path).order("name").order("state").start_at("Springfield")

# Will return "Springfield, Missouri" and "Springfield, Wisconsin"
query2 = firestore.col(collection_path).order("name").order("state").start_at(["Springfield", "Missouri"])paginate_data.rb
```
