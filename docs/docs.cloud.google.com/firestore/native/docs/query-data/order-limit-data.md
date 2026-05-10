---
name: documents/docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data
uri: https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data
title: Order and limit data
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2026-05-09T06:58:59Z"
---

# Order and limit data

> **Tip:** This page applies to the Core operations interface. To order and limit data in the Pipeline operations interface for Enterprise edition, see [Pipeline operation `limit` stage](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/limit) .

Firestore provides powerful query functionality for specifying which documents you want to retrieve from a collection. These queries can also be used with either `get()` or `addSnapshotListener()` , as described in [Get Data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data) .

> **Note:** While the code samples cover multiple languages, the text explaining the samples refers to the Web method names.

## Order and limit data

By default, a query retrieves all documents that satisfy the query in ascending order by document ID. You can specify the sort order for your data using `orderBy()` , and you can limit the number of documents retrieved using `limit()` . If you specify a `limit()` , the value must be greater than or equal to zero.

> **Note:** An `orderBy()` clause also [filters for existence of the given field](https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data#orderby_and_existence) . The result set will not include documents that do not contain the given field.

For example, you could query for the first 3 cities alphabetically with:

### Web version 9

    import { query, orderBy, limit } from "firebase/firestore";  
    
    const q = query(citiesRef, orderBy("name"), limit(3));

### Web version 8

> [Learn more](https://firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

    citiesRef.orderBy("name").limit(3);

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

    citiesRef.order(by: "name").limit(to: 3)

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

    [[citiesRef queryOrderedByField:@"name"] queryLimitedTo:3];

##### Kotlin  
Android

    citiesRef.orderBy("name").limit(3)

##### Java  
Android

    citiesRef.orderBy("name").limit(3);

### Dart

    final citiesRef = db.collection("cities");
    citiesRef.orderBy("name").limit(3);

##### Java

    Query query = cities.orderBy("name").limit(3);
    Query query = cities.orderBy("name").limitToLast(3);

##### Python

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name").limit_to_last(2)
    results = query.get()

##### Python  
(Async)

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name").limit_to_last(2)
    results = await query.get()

##### C++

    cities_ref.OrderBy("name").Limit(3);

##### Node.js

    const firstThreeRes = await citiesRef.orderBy('name').limit(3).get();

##### Go

    query := cities.OrderBy("name", firestore.Asc).Limit(3)
    query := cities.OrderBy("name", firestore.Asc).LimitToLast(3)

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $citiesRef->orderBy('name')->limit(3);

##### Unity

    Query query = citiesRef.OrderBy("Name").Limit(3);

##### C\#

    Query query = citiesRef.OrderBy("Name").Limit(3);

##### Ruby

    query = cities_ref.order("name").limit(3)

You could also sort in descending order to get the *last* 3 cities:

### Web version 9

    import { query, orderBy, limit } from "firebase/firestore";  
    
    const q = query(citiesRef, orderBy("name", "desc"), limit(3));

### Web version 8

> [Learn more](https://firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

    citiesRef.orderBy("name", "desc").limit(3);

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

    citiesRef.order(by: "name", descending: true).limit(to: 3)

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

    [[citiesRef queryOrderedByField:@"name" descending:YES] queryLimitedTo:3];

##### Kotlin  
Android

    citiesRef.orderBy("name", Query.Direction.DESCENDING).limit(3)

##### Java  
Android

    citiesRef.orderBy("name", Direction.DESCENDING).limit(3);

### Dart

    final citiesRef = db.collection("cities");
    citiesRef.orderBy("name", descending: true).limit(3);

##### Java

    Query query = cities.orderBy("name", Direction.DESCENDING).limit(3);

##### Python

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
    results = query.stream()

##### Python  
(Async)

    cities_ref = db.collection("cities")
    query = cities_ref.order_by("name", direction=firestore.Query.DESCENDING).limit(3)
    results = query.stream()

##### C++

    cities_ref.OrderBy("name", Query::Direction::kDescending).Limit(3);

##### Node.js

    const lastThreeRes = await citiesRef.orderBy('name', 'desc').limit(3).get();

##### Go

    query := cities.OrderBy("name", firestore.Desc).Limit(3)

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $citiesRef->orderBy('name', 'DESC')->limit(3);

##### Unity

    Query query = citiesRef.OrderByDescending("Name").Limit(3);

##### C\#

    Query query = citiesRef.OrderByDescending("Name").Limit(3);

##### Ruby

    query = cities_ref.order("name", "desc").limit(3)

You can also order by multiple fields. For example, if you wanted to order by state, and within each state order by population in descending order:

### Web version 9

    import { query, orderBy } from "firebase/firestore";  
    
    const q = query(citiesRef, orderBy("state"), orderBy("population", "desc"));

### Web version 8

> [Learn more](https://firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

    citiesRef.orderBy("state").orderBy("population", "desc");

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

    citiesRef
      .order(by: "state")
      .order(by: "population", descending: true)

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

    [[citiesRef queryOrderedByField:@"state"] queryOrderedByField:@"population" descending:YES];

##### Kotlin  
Android

    citiesRef.orderBy("state").orderBy("population", Query.Direction.DESCENDING)

##### Java  
Android

    citiesRef.orderBy("state").orderBy("population", Direction.DESCENDING);

### Dart

    final citiesRef = db.collection("cities");
    citiesRef.orderBy("state").orderBy("population", descending: true);

##### Java

    Query query = cities.orderBy("state").orderBy("population", Direction.DESCENDING);

##### Python

    cities_ref = db.collection("cities")
    ordered_city_ref = cities_ref.order_by("state").order_by(
        "population", direction=firestore.Query.DESCENDING
    )

##### Python  
(Async)

    cities_ref = db.collection("cities")
    cities_ref.order_by("state").order_by(
        "population", direction=firestore.Query.DESCENDING
    )

##### C++

    cities_ref.OrderBy("state").OrderBy("name", Query::Direction::kDescending);

##### Node.js

    const byStateByPopRes = await citiesRef.orderBy('state').orderBy('population', 'desc').get();

##### Go

    query := client.Collection("cities").OrderBy("state", firestore.Asc).OrderBy("population", firestore.Desc)

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $citiesRef->orderBy('state')->orderBy('population', 'DESC');

##### Unity

    Query query = citiesRef.OrderBy("State").OrderByDescending("Population");

##### C\#

    Query query = citiesRef.OrderBy("State").OrderByDescending("Population");

##### Ruby

    query = cities_ref.order("state").order("population", "desc")

You can combine `where()` filters with `orderBy()` and `limit()` . In the following example, the queries define a population threshold, sort by population in ascending order, and return only the first few results that exceed the threshold:

### Web version 9

    import { query, where, orderBy, limit } from "firebase/firestore";  
    
    const q = query(citiesRef, where("population", ">", 100000), orderBy("population"), limit(2));

### Web version 8

> [Learn more](https://firebase.google.com/docs/web/learn-more#modular-version) about the tree-shakeable modular Web API and its advantages over the namespaced API.

    citiesRef.where("population", ">", 100000).orderBy("population").limit(2);

##### Swift

**Note:** This product is not available on watchOS and App Clip targets.

    citiesRef
      .whereField("population", isGreaterThan: 100000)
      .order(by: "population")
      .limit(to: 2)

##### Objective-C

**Note:** This product is not available on watchOS and App Clip targets.

    [[[citiesRef queryWhereField:@"population" isGreaterThan:@100000]
        queryOrderedByField:@"population"]
        queryLimitedTo:2];

##### Kotlin  
Android

    citiesRef.whereGreaterThan("population", 100000).orderBy("population").limit(2)

##### Java  
Android

    citiesRef.whereGreaterThan("population", 100000).orderBy("population").limit(2);

### Dart

    final citiesRef = db.collection("cities");
    citiesRef
        .where("population", isGreaterThan: 100000)
        .orderBy("population")
        .limit(2);

##### Java

    Query query = cities.whereGreaterThan("population", 2500000L).orderBy("population").limit(2);

##### Python

    cities_ref = db.collection("cities")
    query = (
        cities_ref.where(filter=FieldFilter("population", ">", 2500000))
        .order_by("population")
        .limit(2)
    )
    results = query.stream()

##### Python  
(Async)

    cities_ref = db.collection("cities")
    query = (
        cities_ref.where(filter=FieldFilter("population", ">", 2500000))
        .order_by("population")
        .limit(2)
    )
    results = query.stream()

##### C++

    cities_ref.WhereGreaterThan("population", FieldValue::Integer(100000))
        .OrderBy("population")
        .Limit(2);

##### Node.js

    const biggestRes = await citiesRef.where('population', '>', 2500000)
      .orderBy('population').limit(2).get();

##### Go

    query := cities.Where("population", ">", 2500000).OrderBy("population", firestore.Desc).Limit(2)

##### PHP

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $citiesRef
        ->where('population', '>', 2500000)
        ->orderBy('population')
        ->limit(2);

##### Unity

    Query query = citiesRef
        .WhereGreaterThan("Population", 2500000)
        .OrderBy("Population")
        .Limit(2);

##### C\#

    Query query = citiesRef
        .WhereGreaterThan("Population", 2500000)
        .OrderBy("Population")
        .Limit(2);

##### Ruby

    query = cities_ref.where("population", ">", 2_500_000).order("population").limit(2)

However, if you have a filter with a range comparison ( `<` , `<=` , `>` , `>=` ), your first ordering must be on the same field, see the list of `orderBy()` limitations below.

## Limitations

Note the following restriction for `orderBy()` clauses:

  - An `orderBy()` clause also [filters for existence of the given fields](https://docs.cloud.google.com/firestore/native/docs/query-data/order-limit-data#orderby_and_existence) . The result set will not include documents that do not contain the given fields.

## `orderBy` and existence

When you order a query by a given field, the query can return only the documents where the order-by field exists.

For example, the following query would not return any documents where the `population` field is not set, even if they otherwise meet the query filters.

##### Java

    db.collection("cities").whereEqualTo("country", “USA”).orderBy(“population”);

A related effect applies to inequalities. A query with an inequality filter on a field also implies ordering by that field. The following query does not return documents without a `population` field even if `country = USA` in that document . As a workaround, you can execute separate queries for each ordering or you can assign a value for all fields that you order by.

##### Java

    db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000));

The query above includes an implied order-by on the inequality and is equivalent to the following:

##### Java

    db.collection(“cities”).where(or(“country”, USA”), greaterThan(“population”, 250000)).orderBy(“population”);
