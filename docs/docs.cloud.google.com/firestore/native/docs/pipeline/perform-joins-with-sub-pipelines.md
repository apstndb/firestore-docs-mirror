# Perform joins with subqueries

## Background

Pipeline operations are a new query interface for Firestore. This interface provides advanced query functionality that includes complex expressions. Firestore Enterprise edition supports relational-style joins through **correlated subqueries** . Unlike many NoSQL databases that often require denormalizing data or performing multiple client-side requests, subqueries allow you to combine and aggregate data from related collections or subcollections directly on the server.

Subqueries are expressions that execute a nested pipeline for every document processed by the outer query. This enables complex data retrieval patterns, such as fetching a document alongside its related subcollection items or joining logically linked data across disparate root collections.

## Concepts

This section introduces the core concepts behind using subqueries for performing joins in Pipeline operations.

### Subqueries as expressions

A subquery is not a top-level stage; instead, it is an **expression** that can be used in any stage that accepts expressions, such as [`select(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/select) , [`add_fields(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/add_fields) , [`where(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/where) , or [`sort(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/sort) .

Firestore supports three types of subqueries:

  - **Array Subqueries:** Materialize the entire result set of the subquery as an array of documents.
  - **Scalar Subqueries:** Evaluate to a single value, such as a count, an average, or a specific field from a related document.
  - **`subcollection(...)` Subqueries:** simplified joins for a one-to-many parent-child relation.

### Scope and variables

When writing a join, the nested subquery often needs to reference fields from the "outer" document (the parent). To bridge these scopes, you use the [`let(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/let) stage (referred to as `define(...)` in some SDKs) to define variables in the parent scope that can then be referenced in the subquery using the `variable(...)` function.

## Syntax

The following sections give an overview of the syntax for performing joins.

### The `let(...)` stage

The [`let(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/let) stage (referred to as `define(...)` in some SDKs) is a non-filtering stage that explicitly brings data from the parent scope into a named variable for use in subsequent nested scopes.

### Web

``` 
    async function defineStageData() {
      await setDoc(doc(collection(db, "Authors"), "author_123"), {
        "id": "author_123",
        "name": "Jane Austen"
      });
    }
    
```

##### Swift

``` 
      func defineStageData() async throws {
      try await db.collection("authors").document("author_123").setData([
        "id": "author_123",
        "name": "Jane Austen"
      ])
    }
    
```

##### Kotlin  
Android

``` 
    fun defineStageData() {
        val author = hashMapOf(
            "id" to "author_123",
            "name" to "Jane Austen",
        )

        db.collection("Authors").document("author_123").set(author)
    }
  
```

##### Java  
Android

``` 
    public void defineStageData() {
        Map<String, Object> author = new HashMap<>();
        author.put("id", "author_123");
        author.put("name", "Jane Austen");

        db.collection("Authors").document("author_123").set(author);
    }
  
```

### Array Subqueries

An Array subquery is a special case of expression subquery that materializes the entire result set of the subquery into an array. If the subquery returns zero rows, it evaluates to an empty array. It never returns a `null` array. Such queries are useful when the full results are required in the final result, such as when materializing a nested or correlated collection.

Queries can filter, sort, & aggregate in the subquery to also reduce the amount of data that needs to be fetched and returned to help reduce the cost of the query. The order of the subquery is respected, meaning that a `sort(...)` stage in the subquery controls the order of results in the final array.

Use the `toArrayExpression()` SDK wrapper to convert a query into an array.

### Web

``` 
    async function toArrayExpressionStageData() {
      await setDoc(doc(collection(db, "Projects"), "project_1"), {
        "id": "project_1",
        "name": "Alpha Build"
      });
      await addDoc(collection(db, "Tasks"), {
        "project_id": "project_1",
        "title": "System Architecture"
      });
      await addDoc(collection(db, "Tasks"), {
        "project_id": "project_1",
        "title": "Database Schema Design"
      });
    }
  
```

**Response**

``` 
    {
        id: "project_1",
        name: "Alpha Build",
        taskTitles: [
          "System Architecture", "Database Schema Design"
      ]
    }
    
```

##### Swift

``` 
    async function toArrayExpressionStageData() {
      await setDoc(doc(collection(db, "Projects"), "project_1"), {
        "id": "project_1",
        "name": "Alpha Build"
      });
      await addDoc(collection(db, "Tasks"), {
        "project_id": "project_1",
        "title": "System Architecture"
      });
      await addDoc(collection(db, "Tasks"), {
        "project_id": "project_1",
        "title": "Database Schema Design"
      });
    }
    
```

**Response**

``` 
    {
      id: "project_1",
      name: "Alpha Build",
      taskTitles: [
        "System Architecture", "Database Schema Design"
      ]
    }
    
```

##### Kotlin  
Android

``` 
    fun toArrayExpressionData() {
        val project = hashMapOf(
            "id" to "project_1",
            "name" to "Alpha Build",
        )
        db.collection("Projects").document("project_1").set(project)

        val task1 = hashMapOf(
            "project_id" to "project_1",
            "title" to "System Architecture",
        )
        db.collection("Tasks").add(task1)

        val task2 = hashMapOf(
            "project_id" to "project_1",
            "title" to "Database Schema Design",
        )
        db.collection("Tasks").add(task2)
    }
  
```

**Response**

``` 
    {
      id: "project_1",
      name: "Alpha Build",
      taskTitles: [
        "System Architecture", "Database Schema Design"
      ]
    }
    
```

##### Java  
Android

``` 
      public void toArrayExpressionData() {
        Map<String, Object> project = new HashMap<>();
        project.put("id", "project_1");
        project.put("name", "Alpha Build");
        db.collection("Projects").document("project_1").set(project);

        Map<String, Object> task1 = new HashMap<>();
        task1.put("project_id", "project_1");
        task1.put("title", "System Architecture");
        db.collection("Tasks").add(task1);

        Map<String, Object> task2 = new HashMap<>();
        task2.put("project_id", "project_1");
        task2.put("title", "Database Schema Design");
        db.collection("Tasks").add(task2);
    }
  
```

**Response**

``` 
    {
        id: "project_1",
        name: "Alpha Build",
        taskTitles: [
          "System Architecture", "Database Schema Design"
      ]
    }
    
```

### Scalar Subqueries

Scalar subqueries are often used in a [`select(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/select) or [`where(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/where) stage as allow filtering or resulting the result of a subquery without materializing the full query directly.

A scalar subquery which produce zero results will evaluate to `null` itself, while a subquery which evaluates to multiple elements will result in a runtime error.

When a scalar subquery produces only a single field per-result, the field is *elevated* to be the top-level result for the subquery. This is most commonly seen when the subquery ends with a `select(field("user_name"))` or `aggregate(countAll().as("total"))` where the schema of the subquery is just a single field. Otherwise when a subquery can produce multiple fields they are wrapped in a map.

Use the `toScalarExpression()` SDK wrapper to convert a query into a scalar expression.

### Web

``` 
            async function toScalarExpressionStageData() {
              await setDoc(doc(collection(db, "Authors"), "author_202"), {
                "id": "author_202",
                "name": "Charles Dickens"
              });
              await addDoc(collection(db, "Books"), {
                "author_id": "author_202",
                "title": "Great Expectations",
                "rating": 4.8
              });
              await addDoc(collection(db, "Books"), {
                "author_id": "author_202",
                "title": "Oliver Twist",
                "rating": 4.5
              });
            }
        
```

**Response**

``` 
        {
            "id": "author_202",
            "name": "Charles Dickens",
            "averageBookRating": 4.65
        }
      
```

##### Swift

``` 
        try await db.collection("authors").document("author_202").setData([
          "id": "author_202",
          "name": "Charles Dickens"
        ])
        try await db.collection("books").document().setData([
          "author_id": "author_202",
          "title": "Great Expectations",
          "rating": 4.8
        ])
        try await db.collection("books").document().setData([
          "author_id": "author_202",
          "title": "Oliver Twist",
          "rating": 4.5
        ])
        
```

**Response**

``` 
        {
            "id": "author_202",
            "name": "Charles Dickens",
            "averageBookRating": 4.65
        }
      
```

##### Kotlin  
Android

``` 
        fun toScalarExpressionData() {
        val author = hashMapOf(
            "id" to "author_202",
            "name" to "Charles Dickens",
        )
        db.collection("Authors").document("author_202").set(author)

        val book1 = hashMapOf(
            "author_id" to "author_202",
            "title" to "Great Expectations",
            "rating" to 4.8,
        )
        db.collection("Books").add(book1)

        val book2 = hashMapOf(
            "author_id" to "author_202",
            "title" to "Oliver Twist",
            "rating" to 4.5,
        )
        db.collection("Books").add(book2)
    }
  
```

**Response**

``` 
        {
            "id": "author_202",
            "name": "Charles Dickens",
            "averageBookRating": 4.65
        }
      
```

##### Java  
Android

``` 
       public void toScalarExpressionData() {
        Map<String, Object> author = new HashMap<>();
        author.put("id", "author_202");
        author.put("name", "Charles Dickens");
        db.collection("Authors").document("author_202").set(author);

        Map<String, Object> book1 = new HashMap<>();
        book1.put("author_id", "author_202");
        book1.put("title", "Great Expectations");
        book1.put("rating", 4.8);
        db.collection("Books").add(book1);

        Map<String, Object> book2 = new HashMap<>();
        book2.put("author_id", "author_202");
        book2.put("title", "Oliver Twist");
        book2.put("rating", 4.5);
        db.collection("Books").add(book2);
    }
  
```

**Response**

``` 
        {
            "id": "author_202",
            "name": "Charles Dickens",
            "averageBookRating": 4.65
        }
      
```

### `subcollection(...)` Subqueries

While offered as a stage, the [`subcollection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/subcollection) input stage allows performing joins over Firestore's hierarchical data model. In a hierarchical model, queries often need to retrieve a document alongside data from its own subcollections. While you can achieve this using a [`collection_group(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/collection_group) input stage followed by a filter on the parent reference, `subcollection(...)` provides a much more concise syntax.

Other than the implicit join condition, this acts similarly to an array subquery, returning an empty result if no documents are matched, even if the nested collection does not exist.

It is fundamentally **syntactic sugar** : it automatically uses the `__name__` of the document in the outer scope as the join key to resolve the hierarchical relationship. This makes it the preferred way to perform lookups across collections linked in a parent-child relationship.

## Best practices

  - **Manage memory with `toArrayExpression()` :** Be cautious with `toArrayExpression()` subqueries, since materializing a large number of documents can exhaust the query memory limit (128 MiB). To mitigate this, use [`select(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/select) within the subquery to return only the necessary fields and apply [`where(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/where) filters to limit the number of documents returned. Consider using [`limit(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/limit) if appropriate to cap the number of documents returned by the subquery.
  - **Indexing:** Ensure that fields used in the [`where(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/transformation/where) clause of a subquery are indexed. Performant joins rely on the ability to perform index seeks rather than full table scans.

For more query best practices, refer to our [guide covering query optimization](https://docs.cloud.google.com/firestore/native/docs/enterprise-optimize-query-performance) .

## Limitations

  - **[`subcollection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/subcollection) scope:** The [`subcollection(...)`](https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/input/subcollection) input stage is only supported within subqueries, as it requires the context of a parent document to resolve the hierarchical relationship and perform the join.
  - **Nesting Depth:** Subqueries can be nested up to 20 layers deep.
  - **Memory Usage:** The 128 MiB limit on materialized data applies across the entire query, including all joined documents.
