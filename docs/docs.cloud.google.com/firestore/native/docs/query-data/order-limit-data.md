# Order and limit data

**Tip:** This page applies to the Core operations interface. To order and limit data in the Pipeline operations interface for Enterprise edition, see [Pipeline operation `  limit  ` stage](/firestore/native/docs/pipeline/stages/transformation/limit) .

Firestore provides powerful query functionality for specifying which documents you want to retrieve from a collection. These queries can also be used with either `  get()  ` or `  addSnapshotListener()  ` , as described in [Get Data](/firestore/native/docs/query-data/get-data) .

**Note:** While the code samples cover multiple languages, the text explaining the samples refers to the Web method names.

## Order and limit data

By default, a query retrieves all documents that satisfy the query in ascending order by document ID. You can specify the sort order for your data using `  orderBy()  ` , and you can limit the number of documents retrieved using `  limit()  ` . If you specify a `  limit()  ` , the value must be greater than or equal to zero.

**Note:** An `  orderBy()  ` clause also [filters for existence of the given field](#orderby_and_existence) . The result set will not include documents that do not contain the given field.

For example, you could query for the first 3 cities alphabetically with:

### Web version 9

``` javascript
import { query, orderBy, limit } from "firebase/firestore";  

const q = query(citiesRef, orderBy("name"), limit(3));order_and_limit.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.orderBy("name").limit(3);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef.order(by: "name").limit(to: 3)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[citiesRef queryOrderedByField:@"name"] queryLimitedTo:3];ViewController.m
```

##### Kotlin  
Android

``` text
citiesRef.orderBy("name").limit(3)DocSnippets.kt
```

##### Java  
Android

``` text
citiesRef.orderBy("name").limit(3);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
citiesRef.orderBy("name").limit(3);firestore.dart
```

##### Java

``` java
Query query = cities.orderBy("name").limit(3);
Query query = cities.orderBy("name").limitToLast(3);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
query = cities_ref.order_by("name").limit_to_last(2)
results = query.get()snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
query = cities_ref.order_by("name").limit_to_last(2)
results = await query.get()snippets.py
```

##### C++

``` cpp
cities_ref.OrderBy("name").Limit(3);snippets.cpp
```

##### Node.js

``` javascript
const firstThreeRes = await citiesRef.orderBy('name').limit(3).get();index.js
```

##### Go

``` go
query := cities.OrderBy("name", firestore.Asc).Limit(3)
query := cities.OrderBy("name", firestore.Asc).LimitToLast(3)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef->orderBy('name')->limit(3);
```

##### Unity

``` text
Query query = citiesRef.OrderBy("Name").Limit(3);
```

##### C\#

``` csharp
Query query = citiesRef.OrderBy("Name").Limit(3);Program.cs
```

##### Ruby

``` ruby
query = cities_ref.order("name").limit(3)order_limit_data.rb
```

You could also sort in descending order to get the *last* 3 cities:

### Web version 9

``` javascript
import { query, orderBy, limit } from "firebase/firestore";  

const q = query(citiesRef, orderBy("name", "desc"), limit(3));order_and_limit_desc.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.orderBy("name", "desc").limit(3);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef.order(by: "name", descending: true).limit(to: 3)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[citiesRef queryOrderedByField:@"name" descending:YES] queryLimitedTo:3];ViewController.m
```

##### Kotlin  
Android

``` text
citiesRef.orderBy("name", Query.Direction.DESCENDING).limit(3)DocSnippets.kt
```

##### Java  
Android

``` text
citiesRef.orderBy("name", Direction.DESCENDING).limit(3);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
citiesRef.orderBy("name", descending: true).limit(3);firestore.dart
```

##### Java

``` java
Query query = cities.orderBy("name", Direction.DESCENDING).limit(3);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
results = query.stream()snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
results = query.stream()snippets.py
```

##### C++

``` cpp
cities_ref.OrderBy("name", Query::Direction::kDescending).Limit(3);snippets.cpp
```

##### Node.js

``` javascript
const lastThreeRes = await citiesRef.orderBy('name', 'desc').limit(3).get();index.js
```

##### Go

``` go
query := cities.OrderBy("name", firestore.Desc).Limit(3)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef->orderBy('name', 'DESC')->limit(3);
```

##### Unity

``` text
Query query = citiesRef.OrderByDescending("Name").Limit(3);
```

##### C\#

``` csharp
Query query = citiesRef.OrderByDescending("Name").Limit(3);Program.cs
```

##### Ruby

``` ruby
query = cities_ref.order("name", "desc").limit(3)order_limit_data.rb
```

You can also order by multiple fields. For example, if you wanted to order by state, and within each state order by population in descending order:

### Web version 9

``` javascript
import { query, orderBy } from "firebase/firestore";  

const q = query(citiesRef, orderBy("state"), orderBy("population", "desc"));order_multiple.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.orderBy("state").orderBy("population", "desc");test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef
  .order(by: "state")
  .order(by: "population", descending: true)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[citiesRef queryOrderedByField:@"state"] queryOrderedByField:@"population" descending:YES];ViewController.m
```

##### Kotlin  
Android

``` text
citiesRef.orderBy("state").orderBy("population", Query.Direction.DESCENDING)DocSnippets.kt
```

##### Java  
Android

``` text
citiesRef.orderBy("state").orderBy("population", Direction.DESCENDING);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
citiesRef.orderBy("state").orderBy("population", descending: true);firestore.dart
```

##### Java

``` java
Query query = cities.orderBy("state").orderBy("population", Direction.DESCENDING);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
ordered_city_ref = cities_ref.order_by("state").order_by(
    "population", direction=firestore.Query.DESCENDING
)snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
cities_ref.order_by("state").order_by(
    "population", direction=firestore.Query.DESCENDING
)snippets.py
```

##### C++

``` cpp
cities_ref.OrderBy("state").OrderBy("name", Query::Direction::kDescending);snippets.cpp
```

##### Node.js

``` javascript
const byStateByPopRes = await citiesRef.orderBy('state').orderBy('population', 'desc').get();index.js
```

##### Go

``` go
query := client.Collection("cities").OrderBy("state", firestore.Asc).OrderBy("population", firestore.Desc)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef->orderBy('state')->orderBy('population', 'DESC');
```

##### Unity

``` text
Query query = citiesRef.OrderBy("State").OrderByDescending("Population");
```

##### C\#

``` csharp
Query query = citiesRef.OrderBy("State").OrderByDescending("Population");Program.cs
```

##### Ruby

``` ruby
query = cities_ref.order("state").order("population", "desc")order_limit_data.rb
```

You can combine `  where()  ` filters with `  orderBy()  ` and `  limit()  ` . In the following example, the queries define a population threshold, sort by population in ascending order, and return only the first few results that exceed the threshold:

### Web version 9

``` javascript
import { query, where, orderBy, limit } from "firebase/firestore";  

const q = query(citiesRef, where("population", ">", 100000), orderBy("population"), limit(2));filter_and_order.js
```

### Web version 8

[Learn more](//firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

``` javascript
citiesRef.where("population", ">", 100000).orderBy("population").limit(2);test.firestore.js
```

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

``` swift
citiesRef
  .whereField("population", isGreaterThan: 100000)
  .order(by: "population")
  .limit(to: 2)ViewController.swift
```

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

``` objective-c
[[[citiesRef queryWhereField:@"population" isGreaterThan:@100000]
    queryOrderedByField:@"population"]
    queryLimitedTo:2];ViewController.m
```

##### Kotlin  
Android

``` text
citiesRef.whereGreaterThan("population", 100000).orderBy("population").limit(2)DocSnippets.kt
```

##### Java  
Android

``` text
citiesRef.whereGreaterThan("population", 100000).orderBy("population").limit(2);DocSnippets.java
```

### Dart

``` dart
final citiesRef = db.collection("cities");
citiesRef
    .where("population", isGreaterThan: 100000)
    .orderBy("population")
    .limit(2);firestore.dart
```

##### Java

``` java
Query query = cities.whereGreaterThan("population", 2500000L).orderBy("population").limit(2);QueryDataSnippets.java
```

##### Python

``` python
cities_ref = db.collection("cities")
query = (
    cities_ref.where(filter=FieldFilter("population", ">", 2500000))
    .order_by("population")
    .limit(2)
)
results = query.stream()snippets.py
```

##### Python  
(Async)

``` python
cities_ref = db.collection("cities")
query = (
    cities_ref.where(filter=FieldFilter("population", ">", 2500000))
    .order_by("population")
    .limit(2)
)
results = query.stream()snippets.py
```

##### C++

``` cpp
cities_ref.WhereGreaterThan("population", FieldValue::Integer(100000))
    .OrderBy("population")
    .Limit(2);snippets.cpp
```

##### Node.js

``` javascript
const biggestRes = await citiesRef.where('population', '>', 2500000)
  .orderBy('population').limit(2).get();index.js
```

##### Go

``` go
query := cities.Where("population", ">", 2500000).OrderBy("population", firestore.Desc).Limit(2)query.go
```

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $citiesRef
    ->where('population', '>', 2500000)
    ->orderBy('population')
    ->limit(2);
```

##### Unity

``` text
Query query = citiesRef
    .WhereGreaterThan("Population", 2500000)
    .OrderBy("Population")
    .Limit(2);
```

##### C\#

``` csharp
Query query = citiesRef
    .WhereGreaterThan("Population", 2500000)
    .OrderBy("Population")
    .Limit(2);Program.cs
```

##### Ruby

``` ruby
query = cities_ref.where("population", ">", 2_500_000).order("population").limit(2)order_limit_data.rb
```

However, if you have a filter with a range comparison ( `  <  ` , `  <=  ` , `  >  ` , `  >=  ` ), your first ordering must be on the same field, see the list of `  orderBy()  ` limitations below.

## Limitations

Note the following restriction for `  orderBy()  ` clauses:

  - An `  orderBy()  ` clause also [filters for existence of the given fields](#orderby_and_existence) . The result set will not include documents that do not contain the given fields.

## `     orderBy    ` and existence

When you order a query by a given field, the query can return only the documents where the order-by field exists.

For example, the following query would not return any documents where the `  population  ` field is not set, even if they otherwise meet the query filters.

##### Java

``` text
db.collection("cities").whereEqualTo("country", “USA”).orderBy(“population”);
```

A related effect applies to inequalities. A query with an inequality filter on a field also implies ordering by that field. The following query does not return documents without a `  population  ` field even if `  country = USA  ` in that document . As a workaround, you can execute separate queries for each ordering or you can assign a value for all fields that you order by.

##### Java

``` text
db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000));
```

The query above includes an implied order-by on the inequality and is equivalent to the following:

##### Java

``` text
db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000)).orderBy(“population”);
```
