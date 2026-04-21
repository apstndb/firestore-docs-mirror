# Use text queries

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use text search features in Firestore with MongoDB compatibility to search for specific strings within a collection.

## Before you begin

Before you start using text queries, do the following:

1.  Ensure that you have access to an existing MongoDB compatible operations database, or [Create a database and connect to it](https://firebase.google.com/docs/firestore/enterprise/create-and-query-database) .

2.  Ensure that you have a text index, or [Create a text index](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/indexing#create-text-index) .

### IAM permissions

To create an index in Firestore with MongoDB compatibility, make sure that you are assigned any of the following roles:

  - `roles/datastore.owner`
  - `roles/datastore.indexAdmin`
  - `roles/editor`
  - `roles/owner`

To grant a role, see [Grant a single role](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access#single-role) . For more information about Firestore roles and associated permissions, see [Predefined roles](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/security/iam#predefined_roles) .

If you have defined custom roles, assign all of the following permissions to create indexes:

  - `datastore.indexes.create`
  - `datastore.indexes.delete`
  - `datastore.indexes.get`
  - `datastore.indexes.list`
  - `datastore.indexes.update`

## Run a text query

Text queries use the `$text` operator inside a filter. Specify the queried string in the `$search` argument.

### Run a general text query

Run the following query to perform a general query:

``` 
  # Find query
  db.cities.find({ $text: { $search: "french bread" } })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "french bread" } } }
  ]);
```

If your index is partitioned, then you can filter based on the partition by including the partition in an "and" equality filter within your query. For example, if you had a `city` partition, you could filter a text query as follows:

    db.myCollection.find( { $and: [
      { $text: { $search: "french bread" } },
      { "city": "Paris" }
    ] } )

You can also filter an aggregation based on a partition. For example:

    db.myCollection.aggregate([
     { $match: { $text: { $search: "french bread" } } },
     { "city": "Paris" }
    ] );

The value of your partition must be a string. Your partition filter must be joined to your query by using an "and".

### Set the query language

You can set the query language using the `$language` argument. For example:

``` 
  db.cities.find({ $text: { $search: "french bread", $language: "en"} })
```

If you don't set the query language, then the query uses the language of the text index.

### Query an exact term

To query an exact term, configure the term as a sequence of words enclosed by double quotes. For example:

``` 
  # Find query
  db.cities.find({ $text: { $search: "\"best french bread\"" } })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "\"best french bread\"" } } },
  ]);
```

### Query a term combination

To make your query more precise, specify a chain of terms. For example, the following query returns documents that match the combination **best AND french AND ("bread" OR "is")** :

``` 
  # Find query
  db.cities.find({ $text: { $search: "\"best\" \"french\" bread is" } })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "\"best\" \"french\" bread is" } } },
  ]);
```

### Exclude a term

To exclude a term from a query, prefix the term with a hyphen (-):

``` 
  # Find query
  db.cities.find({ $text: { $search: "best bread -french"} })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "best bread -french" } } },
  ]);
```

## Calculate relevance score

Use the `{$meta: "textScore"}` expression to calculate the relevance score of the documents matched by the text query. To sort the results in descending score order, use `$meta` in a sort expression. Consider the following examples, where SCORE\_FIELD is the name of the field used to store the score value:

``` 
  # Find query
  db.cities
    .find({ $text: { $search: "best french bread" } })
    .sort({ SCORE_FIELD: { $meta: "textScore" } })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "best french bread" } } },
    { $sort: { "SCORE_FIELD": { $meta: "textScore"} } },
  ]);
```

You can also use text score in projection expressions. For example:

``` 
  # Find query
  db.cities
    .find({ $text: { $search: "best french bread" } })
    .project({ score: { $meta: "textScore" } })

  # Aggregation query
  db.cities.aggregate([
    { $match: { $text: { $search: "best french bread" } } },
    { $project: { "scoreField": { $meta: "textScore"} } },
  ]);
```

## Expand query

To enhance the relevance of query outcomes, the `$text` operator augments the search string according to the specified language to include matches for context-aware synonyms, stemmed forms, spelling-corrected terms, diacritic variations and more.

## Limitations

  - `$near` operators and `$text` operators can't be used in the same the query.
  - A single `$text` operator is permitted per `find` or `aggregation` query.
  - In aggregations, the `$match` stage with `$text` must be the first pipeline stage.
  - `$text` can only be nested inside `$and` and `$or` .
  - If `$text` is inside `$or` , the non-search disjuncts may use existing ordered indexes to optimize the query. If the other disjuncts are not indexed, then the query will rely on a collection scan.
  - `$text` cannot be used with query hints.
  - Queries with text search can't sort by `$natural` .
