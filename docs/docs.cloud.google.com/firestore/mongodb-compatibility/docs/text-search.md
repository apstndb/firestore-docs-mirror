# Use text searches

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use text search features in Firestore with MongoDB compatibility to search for specific strings within a collection.

## Before you begin

Before you start using text searches, do the following:

1.  Ensure that you have access to an existing MongoDB compatible operations database, or [Create a database and connect to it](https://firebase.google.com/docs/firestore/enterprise/create-and-query-database) .

2.  Ensure that you have a text index, or [Create a text index](https://docs.cloud.google.com/firestore/mongodb-compatibility/docs/indexing#create-text-index) .

## Run a text search

Text searches use the `$text` operator inside a filter. Specify the queried string in the `$search` argument.

### Run a general text search

Run the following command to perform a general text search:

``` 
  # Find search
  db.cities.find({ $text: { $search: "french bread" } })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "french bread" } } }
  ]);
```

If your index is partitioned, then you can filter based on the partition by including the partition in an "and" equality filter within your search. For example, if you had a `city` partition, you could filter a text search as follows:

    db.myCollection.find( { $and: [
      { $text: { $search: "french bread" } },
      { "city": "Paris" }
    ] } )

You can also filter an aggregation based on a partition. For example:

    db.myCollection.aggregate([
     { $match: { $text: { $search: "french bread" } } },
     { "city": "Paris" }
    ] );

The value of your partition must be a string. Your partition filter must be joined to your text search by using an "and".

### Set the text search language

You can set the text search language using the `$language` argument. For example:

``` 
  db.cities.find({ $text: { $search: "french bread", $language: "en"} })
```

If you don't set a language, then the search uses the language of the text index.

### Search for an exact term

To search for an exact term, configure the term as a sequence of words enclosed by double quotes. For example:

``` 
  # Find search
  db.cities.find({ $text: { $search: "\"best french bread\"" } })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "\"best french bread\"" } } },
  ]);
```

### Search for a term combination

To make your text search more precise, specify a chain of terms. For example, the following search returns documents that match the combination **best AND french AND ("bread" OR "is")** :

``` 
  # Find search
  db.cities.find({ $text: { $search: "\"best\" \"french\" bread is" } })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "\"best\" \"french\" bread is" } } },
  ]);
```

### Exclude a term

To exclude a term from a text search, prefix the term with a hyphen (-):

``` 
  # Find search
  db.cities.find({ $text: { $search: "best bread -french"} })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "best bread -french" } } },
  ]);
```

## Calculate relevance score

Use the `{$meta: "textScore"}` expression to calculate the relevance score of the documents matched by the text search. To sort the results in descending score order, use `$meta` in a sort expression. Consider the following examples, where SCORE\_FIELD is the name of the field used to store the score value:

``` 
  # Find search
  db.cities
    .find({ $text: { $search: "best french bread" } })
    .sort({ SCORE_FIELD: { $meta: "textScore" } })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "best french bread" } } },
    { $sort: { "SCORE_FIELD": { $meta: "textScore"} } },
  ]);
```

You can also use text score in projection expressions. For example:

``` 
  # Find search
  db.cities
    .find({ $text: { $search: "best french bread" } })
    .project({ score: { $meta: "textScore" } })

  # Aggregation search
  db.cities.aggregate([
    { $match: { $text: { $search: "best french bread" } } },
    { $project: { "scoreField": { $meta: "textScore"} } },
  ]);
```

## Expand search

To enhance the relevance of text search outcomes, the `$text` operator augments the search string according to the specified language to include matches for context-aware synonyms, stemmed forms, spelling-corrected terms, diacritic variations and more.

## Limitations

  - `$near` operators and `$text` operators can't be used in the same the text search.
  - A single `$text` operator is permitted per `find` or `aggregation` search.
  - In aggregations, the `$match` stage with `$text` must be the first pipeline stage.
  - `$text` can only be nested inside `$and` and `$or` .
  - If `$text` is inside `$or` , the non-search disjuncts may use existing ordered indexes to optimize the search. If the other disjuncts are not indexed, then the search relies on a collection scan.
  - `$text` cannot be used with hints.
  - Queries with text search can't sort by `$natural` .
