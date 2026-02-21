# Summarize data with aggregation queries

An aggregation query processes the data from multiple index entries to return a single summary value.

Firestore supports the following aggregation queries:

  - `  count()  `
  - `  sum()  `
  - `  average()  `

Firestore calculates the aggregation and transmits only the result back to your application. Compared to executing a full query and calculating the aggregation in your app, aggregation queries save on both billed document reads and bytes transferred.

Aggregation queries rely on the existing index configuration that your queries already use, and scale proportionally to the number of index entries scanned. Latency increases with the number of items in the aggregation.

**Note:** While the code samples cover multiple languages, the text explaining the samples refers to the Web method names.

## Use the `     count()    ` aggregation

The `  count()  ` aggregation query lets you determine the number of documents in a collection or query.

For more information about the example data, see [Getting data](../query-data/get-data) .

The following `  count()  ` aggregation returns the total number of cities in the `  cities  ` collection.

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` javascript
const coll = collection(db, "cities");
const snapshot = await getCountFromServer(coll);
console.log('count: ', snapshot.data().count);count_aggregate_collection.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities")
let countQuery = query.count
do {
  let snapshot = try await countQuery.getAggregation(source: .server)
  print(snapshot.count)
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRCollectionReference *query = [self.db collectionWithPath:@"cities"];
[query.count aggregationWithSource:FIRAggregateSourceServer
                        completion:^(FIRAggregateQuerySnapshot *snapshot,
                                     NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching count: %@", error);
    } else {
        NSLog(@"Cities count: %@", snapshot.count);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities");
AggregateQuery countQuery = query.count();
countQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Count fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Count: " + snapshot.getCount());
        } else {
            Log.d(TAG, "Count failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities")
val countQuery = query.count()
countQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Count fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Count: ${snapshot.count}")
    } else {
        Log.d(TAG, "Count failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
// Returns number of documents in users collection
db.collection("cities").count().get().then(
      (res) => print(res.count),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Go

``` go
package firestore

import (
 "context"
 "errors"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
 firestorepb "cloud.google.com/go/firestore/apiv1/firestorepb"
)

func createCountQuery(w io.Writer, projectID string) error {

 // Instantiate the client
 ctx := context.Background()
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return err
 }
 defer client.Close()

 collection := client.Collection("users")
 query := collection.Where("born", ">", 1850)

 // `alias` argument--"all"--provides a key for accessing the aggregate query
 // results. The alias value must be unique across all aggregation aliases in
 // an aggregation query and must conform to allowed Document field names.
 //
 // See https://cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1#document for details.
 aggregationQuery := query.NewAggregationQuery().WithCount("all")
 results, err := aggregationQuery.Get(ctx)
 if err != nil {
     return err
 }

 count, ok := results["all"]
 if !ok {
     return errors.New("firestore: couldn't get alias for COUNT from results")
 }

 countValue := count.(*firestorepb.Value)
 fmt.Fprintf(w, "Number of results from query: %d\n", countValue.GetIntegerValue())
 return nil
}
aggregate_query_count.go
```

##### Java

``` text
CollectionReference collection = db.collection("cities");
AggregateQuerySnapshot snapshot = collection.count().get().get();
System.out.println("Count: " + snapshot.getCount());
      
```

##### Node.js

``` text
const collectionRef = db.collection('cities');
const snapshot = await collectionRef.count().get();
console.log(snapshot.data().count);
      
```

##### Python

``` python
from google.cloud import firestore
from google.cloud.firestore_v1 import aggregation
from google.cloud.firestore_v1.base_query import FieldFilter


def create_count_query(project_id: str) -> None:
    """Builds an aggregate query that returns the number of results in the query.

    Arguments:
      project_id: your Google Cloud Project ID
    """
    client = firestore.Client(project=project_id)

    collection_ref = client.collection("users")
    query = collection_ref.where(filter=FieldFilter("born", ">", 1800))
    aggregate_query = aggregation.AggregationQuery(query)

    # `alias` to provides a key for accessing the aggregate query results
    aggregate_query.count(alias="all")

    results = aggregate_query.get()
    for result in results:
        print(f"Alias of results from query: {result[0].alias}")
        print(f"Number of results from query: {result[0].value}")

aggregate_query_count.py
```

The `  count()  ` aggregation takes into account any filters on the query and any `  limit  ` clauses.

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` javascript
const coll = collection(db, "cities");
const q = query(coll, where("state", "==", "CA"));
const snapshot = await getCountFromServer(q);
console.log('count: ', snapshot.data().count);count_aggregate_query.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities").whereField("state", isEqualTo: "CA")
let countQuery = query.count
do {
  let snapshot = try await countQuery.getAggregation(source: .server)
  print(snapshot.count)
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query =
    [[self.db collectionWithPath:@"cities"]
                 queryWhereField:@"state"
                       isEqualTo:@"CA"];
[query.count aggregationWithSource:FIRAggregateSourceServer
                        completion:^(FIRAggregateQuerySnapshot *snapshot,
                                      NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching count: %@", error);
    } else {
        NSLog(@"Cities count: %@", snapshot.count);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities").whereEqualTo("state", "CA");
AggregateQuery countQuery = query.count();
countQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Count fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Count: " + snapshot.getCount());
        } else {
            Log.d(TAG, "Count failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities").whereEqualTo("state", "CA")
val countQuery = query.count()
countQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Count fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Count: ${snapshot.count}")
    } else {
        Log.d(TAG, "Count failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
// This also works with collection queries.
db.collection("cities").where("capital", isEqualTo: 10).count().get().then(
      (res) => print(res.count),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Go

``` go
package firestore

import (
 "context"
 "errors"
 "fmt"
 "io"

 "cloud.google.com/go/firestore"
 firestorepb "cloud.google.com/go/firestore/apiv1/firestorepb"
)

func createCountQuery(w io.Writer, projectID string) error {

 // Instantiate the client
 ctx := context.Background()
 client, err := firestore.NewClient(ctx, projectID)
 if err != nil {
     return err
 }
 defer client.Close()

 collection := client.Collection("users")
 query := collection.Where("born", ">", 1850)

 // `alias` argument--"all"--provides a key for accessing the aggregate query
 // results. The alias value must be unique across all aggregation aliases in
 // an aggregation query and must conform to allowed Document field names.
 //
 // See https://cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1#document for details.
 aggregationQuery := query.NewAggregationQuery().WithCount("all")
 results, err := aggregationQuery.Get(ctx)
 if err != nil {
     return err
 }

 count, ok := results["all"]
 if !ok {
     return errors.New("firestore: couldn't get alias for COUNT from results")
 }

 countValue := count.(*firestorepb.Value)
 fmt.Fprintf(w, "Number of results from query: %d\n", countValue.GetIntegerValue())
 return nil
}
aggregate_query_count.go
```

##### Java

``` text
CollectionReference collection = db.collection("cities");
Query query = collection.whereEqualTo("state", "CA");
AggregateQuerySnapshot snapshot = query.count().get().get();
System.out.println("Count: " + snapshot.getCount());
      
```

##### Node.js

``` text
const collectionRef = db.collection('cities');
const query = collectionRef.where('state', '==', 'CA');
const snapshot = await query.count().get();
console.log(snapshot.data().count);
      
```

##### Python

``` python
from google.cloud import firestore
from google.cloud.firestore_v1 import aggregation
from google.cloud.firestore_v1.base_query import FieldFilter


def create_count_query(project_id: str) -> None:
    """Builds an aggregate query that returns the number of results in the query.

    Arguments:
      project_id: your Google Cloud Project ID
    """
    client = firestore.Client(project=project_id)

    collection_ref = client.collection("users")
    query = collection_ref.where(filter=FieldFilter("born", ">", 1800))
    aggregate_query = aggregation.AggregationQuery(query)

    # `alias` to provides a key for accessing the aggregate query results
    aggregate_query.count(alias="all")

    results = aggregate_query.get()
    for result in results:
        print(f"Alias of results from query: {result[0].alias}")
        print(f"Number of results from query: {result[0].value}")

aggregate_query_count.py
```

## Use the `     sum()    ` aggregation

Use the `  sum()  ` aggregation to return the total sum of numeric values that match a given query—for example:

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` text
const coll = collection(firestore, 'cities');
const snapshot = await getAggregateFromServer(coll, {
  totalPopulation: sum('population')
});

console.log('totalPopulation: ', snapshot.data().totalPopulation);
    
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities")
let aggregateQuery = query.aggregate([AggregateField.sum("population")])
do {
  let snapshot = try await aggregateQuery.getAggregation(source: .server)
  print(snapshot.get(AggregateField.sum("population")))
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [self.db collectionWithPath:@"cities"];
FIRAggregateQuery *aggregateQuery = [query aggregate:@[
    [FIRAggregateField aggregateFieldForSumOfField:@"population"]]];
[aggregateQuery aggregationWithSource:FIRAggregateSourceServer
                           completion:^(FIRAggregateQuerySnapshot *snapshot,
                                        NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching aggregate: %@", error);
    } else {
        NSLog(@"Sum: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForSumOfField:@"population"]]);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities");
AggregateQuery aggregateQuery = query.aggregate(AggregateField.sum("population"));
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Aggregate fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Sum: " + snapshot.get(AggregateField.sum("population")));
        } else {
            Log.d(TAG, "Aggregation failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities")
val aggregateQuery = query.aggregate(AggregateField.sum("population"))
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Aggregate fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Sum: ${snapshot.get(AggregateField.sum("population"))}")
    } else {
        Log.d(TAG, "Aggregate failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
db.collection("cities").aggregate(sum("population")).get().then(
      (res) => print(res.getAverage("population")),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Java

``` text
collection = db.collection("cities");
snapshot = collection.aggregate(sum("population")).get().get();
System.out.println("Sum: " + snapshot.get(sum("population")));
      
```

##### Node.js

``` text
const coll = firestore.collection('cities');
const sumAggregateQuery = coll.aggregate({
         totalPopulation: AggregateField.sum('population'),
       });

const snapshot = await sumAggregateQuery.get();
console.log('totalPopulation: ', snapshot.data().totalPopulation);
      
```

##### Python

``` text
collection_ref = client.collection("users")
aggregate_query = aggregation.AggregationQuery(collection_ref)

aggregate_query.sum("coins", alias="sum")

results = aggregate_query.get()
for result in results:
    print(f"Alias of results from query: {result[0].alias}")
    print(f"Sum of results from query: {result[0].value}")
      
```

##### Go

``` text
func createSumQuery(w io.Writer, projectID string) error {
  ctx := context.Background()
  client, err := firestore.NewClient(ctx, projectID)
  if err != nil {
    return err
  }
  defer client.Close()

  collection := client.Collection("users")
  query := collection.Where("born", ">", 1850)

  aggregationQuery := query.NewAggregationQuery().WithSum("coins", "sum_coins")
  results, err := aggregationQuery.Get(ctx)
  if err != nil {
    return err
  }

  sum, ok := results["sum_coins"]
  if !ok {
    return errors.New("firestore: couldn't get alias for SUM from results")
  }

  sumValue := sum.(*firestorepb.Value)
  fmt.Fprintf(w, "Sum of results from query: %d\n", sumValue.GetIntegerValue())
  return nil
}
      
```

The `  sum()  ` aggregation takes into account any filters on the query and any limit clauses—for example:

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` text
const coll = collection(firestore, 'cities');
const q = query(coll, where('capital', '==', true));
const snapshot = await getAggregateFromServer(q, {
  totalPopulation: sum('population')
});

console.log('totalPopulation: ', snapshot.data().totalPopulation);
      
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities").whereField("capital", isEqualTo: true)
let aggregateQuery = query.aggregate([AggregateField.sum("population")])
do {
  let snapshot = try await aggregateQuery.getAggregation(source: .server)
  print(snapshot.get(AggregateField.sum("population")))
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [[self.db collectionWithPath:@"cities"]
                   queryWhereFilter:[FIRFilter filterWhereField:@"capital" isEqualTo:@YES]];
FIRAggregateQuery *aggregateQuery = [query aggregate:@[
    [FIRAggregateField aggregateFieldForSumOfField:@"population"]]];
[aggregateQuery aggregationWithSource:FIRAggregateSourceServer
                           completion:^(FIRAggregateQuerySnapshot *snapshot,
                                        NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching aggregate: %@", error);
    } else {
        NSLog(@"Sum: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForSumOfField:@"population"]]);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities").whereEqualTo("capital", true);
AggregateQuery aggregateQuery = query.aggregate(AggregateField.sum("population"));
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Aggregate fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Sum: " + snapshot.get(AggregateField.sum("population")));
        } else {
            Log.d(TAG, "Aggregation failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities").whereEqualTo("capital", true)
val aggregateQuery = query.aggregate(AggregateField.sum("population"))
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Aggregate fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Sum: ${snapshot.get(AggregateField.sum("population"))}")
    } else {
        Log.d(TAG, "Aggregate failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
db
    .collection("cities")
    .where("capital", isEqualTo: true)
    .aggregate(sum("population"))
    .get()
    .then(
      (res) => print(res.getAverage("population")),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Java

``` text
collection = db.collection("cities");
query = collection.whereEqualTo("state", "CA");
snapshot = query.aggregate(sum("population")).get().get();
System.out.println("Sum: " + snapshot.get(sum("population")));
      
```

##### Node.js

``` text
const coll = firestore.collection('cities');
const q = coll.where("capital", "==", true);
const sumAggregateQuery = q.aggregate({
        totalPopulation: AggregateField.sum('population'),
      });

const snapshot = await sumAggregateQuery.get();
console.log('totalPopulation: ', snapshot.data().totalPopulation);
      
```

##### Python

``` text
collection_ref = client.collection("users")
query = collection_ref.where(filter=FieldFilter("people", "==", "Matthew"))
aggregate_query = aggregation.AggregationQuery(query)

aggregate_query.sum("coins", alias="sum")

results = aggregate_query.get()
for result in results:
    print(f"Alias of results from query: {result[0].alias}")
    print(f"Sum of results from query: {result[0].value}")
      
```

##### Go

``` text
func createSumQuery(w io.Writer, projectID string) error {
  ctx := context.Background()
  client, err := firestore.NewClient(ctx, projectID)
  if err != nil {
    return err
  }
  defer client.Close()

  collection := client.Collection("users")
  query := collection.Where("born", ">", 1850).Limit(5)

  aggregationQuery := query.NewAggregationQuery().WithSum("coins", "sum_coins")
  results, err := aggregationQuery.Get(ctx)
  if err != nil {
    return err
  }

  sum, ok := results["sum_coins"]
  if !ok {
    return errors.New("firestore: couldn't get alias for SUM from results")
  }

  sumValue := sum.(*firestorepb.Value)
  fmt.Fprintf(w, "Sum of results from query: %d\n", sumValue.GetIntegerValue())
  return nil
}
      
```

## Use the `     average()    ` aggregation

Use the `  average()  ` aggregation to return the average of numeric values that match a given query, for example:

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` text
const coll = collection(firestore, 'cities');
const snapshot = await getAggregateFromServer(coll, {
  averagePopulation: average('population')
});

console.log('averagePopulation: ', snapshot.data().averagePopulation);
    
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities")
let aggregateQuery = query.aggregate([AggregateField.average("population")])
do {
  let snapshot = try await aggregateQuery.getAggregation(source: .server)
  print(snapshot.get(AggregateField.average("population")))
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [self.db collectionWithPath:@"cities"];
FIRAggregateQuery *aggregateQuery = [query aggregate:@[
    [FIRAggregateField aggregateFieldForAverageOfField:@"population"]]];
[aggregateQuery aggregationWithSource:FIRAggregateSourceServer
                           completion:^(FIRAggregateQuerySnapshot *snapshot,
                                        NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching aggregate: %@", error);
    } else {
        NSLog(@"Avg: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForAverageOfField:@"population"]]);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities");
AggregateQuery aggregateQuery = query.aggregate(AggregateField.average("population"));
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Aggregate fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Average: " + snapshot.get(AggregateField.average("population")));
        } else {
            Log.d(TAG, "Aggregation failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities")
val aggregateQuery = query.aggregate(AggregateField.average("population"))
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Aggregate fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Average: ${snapshot.get(AggregateField.average("population"))}")
    } else {
        Log.d(TAG, "Aggregate failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
db.collection("cities").aggregate(average("population")).get().then(
      (res) => print(res.getAverage("population")),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Java

``` text
collection = db.collection("cities");
snapshot = collection.aggregate(average("population")).get().get();
System.out.println("Average: " + snapshot.get(average("population")));
      
```

##### Node.js

``` text
const coll = firestore.collection('cities');
const averageAggregateQuery = coll.aggregate({
        averagePopulation: AggregateField.average('population'),
      });

const snapshot = await averageAggregateQuery.get();
console.log('averagePopulation: ', snapshot.data().averagePopulation);
      
```

##### Python

``` text
collection_ref = client.collection("users")
aggregate_query = aggregation.AggregationQuery(collection_ref)

aggregate_query.avg("coins", alias="avg")

results = aggregate_query.get()
for result in results:
    print(f"Alias of results from query: {result[0].alias}")
    print(f"Average of results from query: {result[0].value}")
      
```

##### Go

``` text
func createAvgQuery(w io.Writer, projectID string) error {
  ctx := context.Background()
  client, err := firestore.NewClient(ctx, projectID)
  if err != nil {
          return err
  }
  defer client.Close()

  collection := client.Collection("users")
  query := collection.Where("born", ">", 1850)

  aggregationQuery := query.NewAggregationQuery().WithAvg("coins", "avg_coins")
  results, err := aggregationQuery.Get(ctx)
  if err != nil {
    return err
  }

  avg, ok := results["avg_coins"]
  if !ok {
    return errors.New("firestore: couldn't get alias for AVG from results")
  }

  avgValue := avg.(*firestorepb.Value)
  fmt.Fprintf(w, "Avg of results from query: %d\n", avgValue.GetDoubleValue())
  return nil
}
      
```

The `  average()  ` aggregation takes into account any filters on the query and any limit clauses, for example:

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` text
const coll = collection(firestore, 'cities');
const q = query(coll, where('capital', '==', true));
const snapshot = await getAggregateFromServer(q, {
  averagePopulation: average('population')
});

console.log('averagePopulation: ', snapshot.data().averagePopulation);
      
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities").whereField("capital", isEqualTo: true)
let aggregateQuery = query.aggregate([AggregateField.average("population")])
do {
  let snapshot = try await aggregateQuery.getAggregation(source: .server)
  print(snapshot.get(AggregateField.average("population")))
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [[self.db collectionWithPath:@"cities"]
                   queryWhereFilter:[FIRFilter filterWhereField:@"capital" isEqualTo:@YES]];
FIRAggregateQuery *aggregateQuery = [query aggregate:@[
    [FIRAggregateField aggregateFieldForAverageOfField:@"population"]]];
[aggregateQuery aggregationWithSource:FIRAggregateSourceServer
                           completion:^(FIRAggregateQuerySnapshot *snapshot,
                                        NSError *error) {
    if (error != nil) {
        NSLog(@"Error fetching aggregate: %@", error);
    } else {
        NSLog(@"Avg: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForAverageOfField:@"population"]]);
    }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities").whereEqualTo("capital", true);
AggregateQuery aggregateQuery = query.aggregate(AggregateField.average("population"));
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Aggregate fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Average: " + snapshot.get(AggregateField.average("population")));
        } else {
            Log.d(TAG, "Aggregation failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities").whereEqualTo("capital", true)
val aggregateQuery = query.aggregate(AggregateField.average("population"))
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Aggregate fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Average: ${snapshot.get(AggregateField.average("population"))}")
    } else {
        Log.d(TAG, "Aggregate failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
db
    .collection("cities")
    .where("capital", isEqualTo: true)
    .aggregate(average("population"))
    .get()
    .then(
      (res) => print(res.getAverage("population")),
      onError: (e) => print("Error completing: $e"),
    );firestore.dart
```

##### Java

``` text
collection = db.collection("cities");
query = collection.whereEqualTo("state", "CA");
snapshot = query.aggregate(average("population")).get().get();
System.out.println("Average: " + snapshot.get(average("population")));
  
```

##### Node.js

``` text
const coll = firestore.collection('cities');
const q = coll.where("capital", "==", true);
const averageAggregateQuery = q.aggregate({
        averagePopulation: AggregateField.average('population'),
      });

const snapshot = await averageAggregateQuery.get();
console.log('averagePopulation: ', snapshot.data().averagePopulation);
      
```

##### Python

``` text
collection_ref = client.collection("users")
query = collection_ref.where(filter=FieldFilter("people", "==", "Matthew"))
aggregate_query = aggregation.AggregationQuery(query)

aggregate_query.avg("coins", alias="avg")

results = aggregate_query.get()
for result in results:
    print(f"Alias of results from query: {result[0].alias}")
    print(f"Average of results from query: {result[0].value}")
      
```

##### Go

``` text
func createAvgQuery(w io.Writer, projectID string) error {
  ctx := context.Background()
  client, err := firestore.NewClient(ctx, projectID)
  if err != nil {
        return err
  }
  defer client.Close()

  collection := client.Collection("users")
  query := collection.Where("born", ">", 1850).Limit(5)

  aggregationQuery := query.NewAggregationQuery().WithAvg("coins", "avg_coins")
  results, err := aggregationQuery.Get(ctx)
  if err != nil {
    return err
  }

  avg, ok := results["avg_coins"]
  if !ok {
    return errors.New("firestore: couldn't get alias for AVG from results")
  }

  avgValue := avg.(*firestorepb.Value)
  fmt.Fprintf(w, "Avg of results from query: %d\n", avgValue.GetDoubleValue())
  return nil
}
      
```

## Calculate multiple aggregations in a query

You can combine multiple aggregations in a single aggregation pipeline. This can reduce the number of index reads required. If the query includes aggregations on multiple fields, the query might requires a composite index. In that case, Firestore suggests an index.

The following example performs multiple aggregations in a single aggregation query:

### Web version 9

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable Web v9 modular SDK and [upgrade](//firebase.google.com/docs/web/modular-upgrade) from version 8.

``` text
const coll = collection(firestore, 'cities');
const snapshot = await getAggregateFromServer(coll, {
  countOfDocs: count(),
  totalPopulation: sum('population'),
  averagePopulation: average('population')
});

console.log('countOfDocs: ', snapshot.data().countOfDocs);
console.log('totalPopulation: ', snapshot.data().totalPopulation);
console.log('averagePopulation: ', snapshot.data().averagePopulation);
      
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
let query = db.collection("cities")
let aggregateQuery = query.aggregate([
  AggregateField.count(),
  AggregateField.sum("population"),
  AggregateField.average("population")])
do {
  let snapshot = try await aggregateQuery.getAggregation(source: .server)
  print("Count: \(snapshot.get(AggregateField.count()))")
  print("Sum: \(snapshot.get(AggregateField.sum("population")))")
  print("Average: \(snapshot.get(AggregateField.average("population")))")
} catch {
  print(error)
}ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
FIRQuery *query = [self.db collectionWithPath:@"cities"];
FIRAggregateQuery *aggregateQuery = [query aggregate:@[
  [FIRAggregateField aggregateFieldForCount],
  [FIRAggregateField aggregateFieldForSumOfField:@"population"],
  [FIRAggregateField aggregateFieldForAverageOfField:@"population"]]];
[aggregateQuery aggregationWithSource:FIRAggregateSourceServer
                           completion:^(FIRAggregateQuerySnapshot *snapshot,
                                        NSError *error) {
  if (error != nil) {
    NSLog(@"Error fetching aggregate: %@", error);
  } else {
    NSLog(@"Count: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForCount]]);
    NSLog(@"Sum: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForSumOfField:@"population"]]);
    NSLog(@"Avg: %@", [snapshot valueForAggregateField:[FIRAggregateField aggregateFieldForAverageOfField:@"population"]]);
  }
}];ViewController.m
```

##### Java  
Android

``` java
Query query = db.collection("cities");
AggregateQuery aggregateQuery = query.aggregate(
        AggregateField.count(),
        AggregateField.sum("population"),
        AggregateField.average("population"));
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener(new OnCompleteListener<AggregateQuerySnapshot>() {
    @Override
    public void onComplete(@NonNull Task<AggregateQuerySnapshot> task) {
        if (task.isSuccessful()) {
            // Aggregate fetched successfully
            AggregateQuerySnapshot snapshot = task.getResult();
            Log.d(TAG, "Count: " + snapshot.get(AggregateField.count()));
            Log.d(TAG, "Sum: " + snapshot.get(AggregateField.sum("population")));
            Log.d(TAG, "Average: " + snapshot.get(AggregateField.average("population")));
        } else {
            Log.d(TAG, "Aggregation failed: ", task.getException());
        }
    }
});DocSnippets.java
```

##### Kotlin  
Android

``` kotlin
val query = db.collection("cities")
val aggregateQuery = query.aggregate(
    AggregateField.count(),
    AggregateField.sum("population"),
    AggregateField.average("population")
)
aggregateQuery.get(AggregateSource.SERVER).addOnCompleteListener { task ->
    if (task.isSuccessful) {
        // Aggregate fetched successfully
        val snapshot = task.result
        Log.d(TAG, "Count: ${snapshot.get(AggregateField.count())}")
        Log.d(TAG, "Sum: ${snapshot.get(AggregateField.sum("population"))}")
        Log.d(TAG, "Average: ${snapshot.get(AggregateField.average("population"))}")
    } else {
        Log.d(TAG, "Aggregate failed: ", task.getException())
    }
}DocSnippets.kt
```

### Dart

``` dart
db
    .collection("cities")
    .aggregate(
      count(),
      sum("population"),
      average("population"),
    )
    .get()
    .then(
  (res) {
    print(res.count);
    print(res.getSum("population"));
    print(res.getAverage("population"));
  },
  onError: (e) => print("Error completing: $e"),
);firestore.dart
```

##### Java

``` text
collection = db.collection("cities");
query = collection.whereEqualTo("state", "CA");
AggregateQuery aggregateQuery = query.aggregate(count(), sum("population"), average("population"));
snapshot = aggregateQuery.get().get();
System.out.println("Count: " + snapshot.getCount());
System.out.println("Sum: " + snapshot.get(sum("population")));
System.out.println("Average: " + snapshot.get(average("population")));
    
```

##### Node.js

``` text
const coll = firestore.collection('cities');
const aggregateQuery = coll.aggregate({
    countOfDocs: AggregateField.count(),
    totalPopulation: AggregateField.sum('population'),
    averagePopulation: AggregateField.average('population')
  });

const snapshot = await aggregateQuery.get();
console.log('countOfDocs: ', snapshot.data().countOfDocs);
console.log('totalPopulation: ', snapshot.data().totalPopulation);
console.log('averagePopulation: ', snapshot.data().averagePopulation);
      
```

##### Python

``` text
collection_ref = client.collection("users")
query = collection_ref.where(filter=FieldFilter("people", "==", "Matthew"))
aggregate_query = aggregation.AggregationQuery(query)

aggregate_query.sum("coins", alias="sum").avg("coins", alias="avg")

results = aggregate_query.get()
for result in results:
    print(f"Alias of results from query: {result[0].alias}")
    print(f"Aggregation of results from query: {result[0].value}")
      
```

##### Go

``` text
func createMultiAggregationQuery(w io.Writer, projectID string) error {
  ctx := context.Background()
  client, err := firestore.NewClient(ctx, projectID)
  if err != nil {
    return err
  }
  defer client.Close()

  collection := client.Collection("users")
  query := collection.Where("born", ">", 1850)

  aggregationQuery := query.NewAggregationQuery().WithCount("count").WithSum("coins", "sum_coins").WithAvg("coins", "avg_coins")
  results, err := aggregationQuery.Get(ctx)
  if err != nil {
    return err
  }
}
      
```

Queries with multiple aggregations include only the documents that contain all the fields in each aggregation. This might lead to different results from performing each aggregation separately.

## Security rules for aggregation queries

Firestore Security Rules work the same on aggregation queries as on queries that return documents. In other words, if and only if your rules allow clients to execute certain collection or collection group queries, clients can also perform the aggregation on those queries. Learn more about [how Firestore Security Rules interact with queries](../security/rules-query) .

## Behavior and limitations

As you work with aggregation queries, note the following behavior and limitations:

  - You can't use aggregation queries with real-time listeners and offline queries. Aggregation queries are only supported through a direct server response. Queries are served only by the Firestore backend, skipping the local cache and any buffered updates. This behavior is identical to operations that are performed inside [Firestore transactions](../manage-data/transactions) .

  - If an aggregation can't resolve within 60 seconds, it returns a `  DEADLINE_EXCEEDED  ` error. Performance depends on your index configuration and on the size of the dataset.
    
    **Note:** Most queries scale based on the on the size of the result set, not the dataset. However, aggregation queries scale based on the size of the dataset and the number of index entries scanned.
    
    If the operation can't be completed within the 60 second deadline, a possible workaround is to use [counters](../solutions/counters) for large datasets.

  - Aggregation queries read from index entries and include only indexed fields.

  - Adding an `  OrderBy  ` clause to an aggregation query limits the aggregation to the documents where the sorting field exists.

  - For `  sum()  ` and `  average()  ` aggregations, non-numeric values are ignored. `  sum()  ` and `  average()  ` aggregations take into account only integer values and floating-point number values.

  - When combining multiple aggregations in a single query, note that `  sum()  ` and `  average()  ` ignore non-numeric values while `  count()  ` includes non-numeric values.

  - If you combine aggregations that are on different fields, the calculation includes only the documents that contain all those fields.

### Pricing

Pricing for aggregation queries depends on the number of index entries that the query matches. You are charged a small number of reads for a large number of matched entries. You are charged one read operation for each batch of up to 1000 index entries read.

For more information about aggregation queries pricing, see [Aggregation queries](../../pricing#aggregation_queries) .

## What's next

  - Learn how to [query and filter data](/firestore/native/docs/query-data/queries) .
  - Save reads when you want to only [count results](./aggregation-queries)
