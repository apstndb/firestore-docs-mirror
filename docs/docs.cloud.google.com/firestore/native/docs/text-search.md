# Use text search

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use text search features in Firestore to search for specific strings within documents.

## Edition requirements

Text search requires a Firestore Enterprise edition database.

## Before you begin

To perform a text search, you must first [create text indexes](https://docs.cloud.google.com/firestore/native/docs/enterprise-indexing#create-text-index) for the fields you need to search through.

## Run a text search

To perform a text search, use the `documentMatches` expression within the `query` parameter of the `search(...)` stage.

The operation searches only in the fields indexed with a text index. If multiple indexes are available, Firestore selects one index to use for the operation.

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles')
      }));test.firestore.js

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(query: DocumentMatches("waffles"))
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage.withQuery(documentMatches("waffles")))DocSnippets.kt

##### Java  
Android

    Pipeline pipeline = db.pipeline().collection("restaurants")
            .search(SearchStage.withQuery(documentMatches("waffles")));DocSnippets.java

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles')
      })
      .execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import DocumentMatches
    
    results = (
        client.pipeline()
        .collection("restaurants")
        .search(DocumentMatches("waffles"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot results1 =
        firestore.pipeline().collection("restaurants")
            .search(Search.withQuery(documentMatches("waffles")))
            .execute().get();PipelineSnippets.java

##### Go

    snapshot := client.Pipeline().
     Collection("restaurants").
     Search(firestore.WithSearchQuery(firestore.DocumentMatches("waffles"))).
     Execute(ctx)pipeline_snippets_search.go

### Search for an exact term

To search for an exact term, enclose the term in quotes ( `"` ):

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('"belgian waffles"')
      }));test.firestore.js

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(query: DocumentMatches("\"belgian waffles\""))
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage.withQuery(documentMatches("\"belgian waffles\"")))DocSnippets.kt

##### Java  
Android

    Pipeline pipeline = db.pipeline().collection("restaurants")
            .search(SearchStage.withQuery(documentMatches("\"belgian waffles\"")));DocSnippets.java

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('"belgian waffles"')
      })
      .execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import DocumentMatches
    
    results = (
        client.pipeline()
        .collection("restaurants")
        .search(DocumentMatches('"belgian waffles"'))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot results2 =
        firestore.pipeline().collection("restaurants")
            .search(Search.withQuery(documentMatches("\"belgian waffles\"")))
            .execute().get();PipelineSnippets.java

##### Go

    snapshot := client.Pipeline().
     Collection("restaurants").
     Search(firestore.WithSearchQuery(firestore.DocumentMatches("\"belgian waffles\""))).
     Execute(ctx)pipeline_snippets_search.go

### Search for a term combination

To search for combination for terms (logical `AND` ), separate the terms with spaces:

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles eggs')
      }));test.firestore.js

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(query: DocumentMatches("waffles eggs"))
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage.withQuery(documentMatches("waffles eggs")))DocSnippets.kt

##### Java  
Android

    Pipeline pipeline = db.pipeline().collection("restaurants")
            .search(SearchStage.withQuery(documentMatches("waffles eggs")));DocSnippets.java

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles eggs')
      })
      .execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import DocumentMatches
    
    results = (
        client.pipeline()
        .collection("restaurants")
        .search(DocumentMatches("waffles eggs"))
        .execute()
    )firestore_pipelines.py

##### Java

    firestore.collection("restaurants").add(new HashMap<String, Object>() {{
      put("name", "Morning Diner");
      put("description", "Start your day with waffles and eggs.");
    }});
    Pipeline.Snapshot results3 =
        firestore.pipeline().collection("restaurants")
            .search(Search.withQuery(documentMatches("waffles eggs")))
            .execute().get();PipelineSnippets.java

##### Go

    snapshot := client.Pipeline().
     Collection("restaurants").
     Search(firestore.WithSearchQuery(firestore.DocumentMatches("waffles eggs"))).
     Execute(ctx)pipeline_snippets_search.go

### Exclude a term

To exclude a term, prefix the term with a hyphen ( `-` ):

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('coffee -waffles')
      }));test.firestore.js

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(query: DocumentMatches("coffee -waffles"))
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage.withQuery(documentMatches("waffles eggs")))DocSnippets.kt

##### Java  
Android

    Pipeline pipeline = db.pipeline().collection("restaurants")
            .search(SearchStage.withQuery(documentMatches("coffee -waffles")));DocSnippets.java

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('-waffles')
      })
      .execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import DocumentMatches
    
    results = (
        client.pipeline()
        .collection("restaurants")
        .search(DocumentMatches("-waffles"))
        .execute()
    )firestore_pipelines.py

##### Java

    firestore.collection("restaurants").add(new HashMap<String, Object>() {{
      put("name", "City Coffee");
      put("description", "Premium coffee and pastries.");
    }});
    Pipeline.Snapshot results4 =
        firestore.pipeline().collection("restaurants")
            .search(Search.withQuery(documentMatches("-waffles")))
            .execute().get();PipelineSnippets.java

##### Go

    snapshot := client.Pipeline().
     Collection("restaurants").
     Search(firestore.WithSearchQuery(firestore.DocumentMatches("-waffles"))).
     Execute(ctx)pipeline_snippets_search.go

You can also exclude a phrase, for example, `pizza -"New York"` .

### Sort results

By default, Firestore **sorts results by document creation time** , newest to oldest. You can sort by search score instead, but this requires more computation to calculate and compare the exact score of each document:

To sort results by search score:

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles'),
        sort: score().descending()
      }));

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(
          query: DocumentMatches("waffles"),
          sort: [Score().descending()]
          )
      .execute()

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage
                  .withQuery(documentMatches("waffles"))
                  .withSort(score().descending())
                  )

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: documentMatches('waffles'),
        sort: score().descending()
      })
      .execute();

### Add fields to documents returned by the search stage

You can use `addFields` to add fields to the documents returned by the search stage. Expressions returning values computed by the search stage, like `score()` , can be used within `addFields` in the search stage to write those \`values to the output documents.

The following example adds the score field to the documents returned by the search stage:

### Web version 9

    const result = await execute(db.pipeline().collection('restaurants')
      .search({
        query: 'menu:waffles',
        addFields: [
            score().as('score'),
        ]
      }));test.firestore.js

##### iOS

    let snapshot = try await db.pipeline().collection("restaurants")
      .search(
        query: DocumentMatches("waffles"),
        addFields: [
          Score().as("score")
        ]
      )
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val pipeline = db.pipeline().collection("restaurants")
        .search(SearchStage.withQuery(documentMatches("waffles eggs")))DocSnippets.kt

##### Java  
Android

    Pipeline pipeline = db.pipeline().collection("restaurants")
            .search(
                    SearchStage.withQuery(documentMatches("menu:waffles"))
                            .withAddFields(score().alias("score")));DocSnippets.java

##### Node.js

    await db.pipeline().collection('restaurants')
      .search({
        query: field('menu').matches('waffles'),
        addFields: [
            score().as('score'),
        ]
      }).execute();test.firestore.js

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import DocumentMatches, Score
    from google.cloud.firestore_v1.pipeline_stages import SearchOptions
    
    results = (
        client.pipeline()
        .collection("restaurants")
        .search(
            SearchOptions(
                query=DocumentMatches("menu:waffles"),
                add_fields=[Score().as_("score")],
            )
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot results5 =
        firestore.pipeline().collection("restaurants")
            .search(Search.withQuery(field("menu").regexMatch("waffles"))
                .withAddFields(score().as("score")))
            .execute().get();PipelineSnippets.java

##### Go

    snapshot := client.Pipeline().
     Collection("restaurants").
     Search(
         firestore.WithSearchQuery(firestore.FieldOf("menu").RegexMatch("waffles")),
         firestore.WithSearchAddFields(firestore.Score().As("score")),
     ).
     Execute(ctx)pipeline_snippets_search.go
