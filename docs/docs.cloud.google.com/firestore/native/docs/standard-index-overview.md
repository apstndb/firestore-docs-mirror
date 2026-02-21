# Standard edition index overview

Indexing behavior depends on the edition of the database. This page describes indexing for Firestore Standard edition. For Firestore Enterprise edition, see [Firestore Enterprise edition index overview](/firestore/docs/pipeline/concepts/enterprise-index-overview) .

Indexes are an important factor in the performance of a database. Much like the index of a book which maps topics in a book to page numbers, a database index maps the items in a database to their locations in the database. When you query a database, the database can use an index to quickly identify the locations of the items that you requested.

This page describes the two types of indexes that Firestore Standard edition uses, [single-field indexes](#single-field_indexes) and [composite indexes](#composite_indexes) .

#### Index definition and structure

An index is defined on a list of fields of a given document, with a corresponding [index mode](#index_modes) for each field.

An index contains an entry for every field named in the index definition. The index includes all documents that are the potential results for queries based on the index. A document is included in the index only if it has an indexed value set for every field used in the index. If the index definition refers to a field for which the document has no value set, that document won't appear in the index. In this case, the document will never be returned as a result for any query based on the index.

The composite index is sorted by field values, in the order specified in the index definition.

#### An index behind every query

If no index exists for a query, most databases crawl through their contents item by item, a slow process that slows down even more as the database grows. Firestore Standard edition guarantees high query performance by using indexes for *all* queries. As a result, query performance depends on the size of the result set and not on the number of items in the database.

#### Less index management, more app development

Firestore Standard edition includes features that reduce the amount of time that you need to spend on index management. The indexes required for the most basic queries are automatically created for you. As you use and test your app, Firestore Standard edition helps you identify and [create additional indexes](../query-data/indexing) that your app requires.

## Index types

Firestore Standard edition uses two types of indexes: *single-field* and *composite* . Besides the number of fields indexed, single-field and composite indexes differ in how you manage them.

### Single-field indexes

A single-field index stores a sorted mapping of all the documents in a collection that contain a specific field. Each entry in a single-field index records a document's value for a specific field and the location of the document in the database. Firestore Standard edition uses these indexes to perform many basic queries. You manage single-field indexes by configuring your database's automatic indexing settings and index exemptions.

#### Automatic indexing

By default, Firestore Standard edition automatically maintains single-field indexes for each field in a document and each subfield in a map. Firestore Standard edition uses the following default settings for single-field indexes:

  - For each non-array and non-map field, Firestore Standard edition defines two [collection-scope](#query_scopes) single-field indexes, one in ascending mode and one in descending mode.

  - For each map field, Firestore Standard edition creates the following:
    
      - One collection-scope ascending index for each non-array, non-map subfield.
      - One collection-scope descending index for each non-array, non-map subfield.
      - One collection-scope ascending index for the whole map value
      - One collection-scope descending index for the whole map value
      - One collection-scope array-contains index for each array subfield.
      - Firestore Standard edition recursively indexes each map subfield.

  - For each array field in a document, Firestore Standard edition creates the following:
    
      - One collection-scope ascending index for the whole array value
      - One collection-scope descending index for the whole array value
      - One collection-scope array-contains index.

  - Single-field indexes with collection group scope are not maintained by default.

#### Single-field index exemptions

You can exempt a field from your [automatic indexing](#automatic_indexing) settings by creating a single-field index exemption. An indexing exemption overrides the database-wide automatic index settings. An exemption can enable a single-field index that your automatic indexing settings would otherwise disable or disable a single-field index that automatic indexing would otherwise enable. For cases where exemptions can be useful, see the [indexing best practices](#indexing_best_practices) .

Use the `  *  ` field path value to add collection-level index exemptions on all fields in a collection group. For example, for collection group `  comments  ` , set the field path to `  *  ` to match all fields in the `  comments  ` collection group and disable indexing of all the fields under the collection group. You can then add exemptions to index only the fields required for your queries. Reducing the number of indexed fields reduces storage costs and can improve write performance.

If you create a single-field index exemption for a map field, the map's subfields inherit those settings. You can, however, define single-field index exemptions for specific subfields. If you delete an exemption for a subfield, the subfield will inherit its parent's exemption settings, if they exist, or the database-wide settings if no parent exemptions exist.

**Note:** An exemption only applies to automatic index settings. A field exempted from single-field indexing can still be indexed as part of a composite index.

To create and manage single-field index exemptions, see [Manage indexes](../query-data/indexing#exemptions) .

### Composite indexes

A composite index stores a sorted mapping of all the documents in a collection, based on an ordered list of fields to index.

**Note:** You can have at most one array field per composite index.

Firestore Standard edition uses composite indexes to support queries not already supported by single-field indexes.

Firestore Standard edition doesn't automatically create composite indexes like it does for single-field indexes because of the large number of possible field combinations. Instead, Firestore Standard edition helps you [identify and create required composite indexes](../query-data/indexing) as you build your app.

Any time you attempt a query that isn't supported by an index, Firestore Standard edition returns an error message with a link that you can follow to create the missing index.

You can also define and manage composite indexes manually by using the console or by using the [Firebase CLI](//firebase.google.com/docs/cli) . For more on creating and managing composite indexes, see [Manage indexes](../query-data/indexing) .

### Index modes and query scopes

You configure single-field and composite indexes differently, but both require that you configure index modes and query scopes for your indexes.

#### Index modes

When you define an index, you select an index mode for each indexed field. Each field's index mode supports specific query clauses on that field. You can select from the following index modes:

<table>
<thead>
<tr class="header">
<th>Index mode</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Ascending</strong> arrow_upward</td>
<td>Supports <code dir="ltr" translate="no">       &lt;      </code> , <code dir="ltr" translate="no">       &lt;=      </code> , <code dir="ltr" translate="no">       ==      </code> , <code dir="ltr" translate="no">       &gt;=      </code> , <code dir="ltr" translate="no">       &gt;      </code> , <code dir="ltr" translate="no">       !=      </code> , <code dir="ltr" translate="no">       in      </code> , and <code dir="ltr" translate="no">       not-in      </code> , query clauses on the field and supports sorting results in ascending order based on this field value.</td>
</tr>
<tr class="even">
<td><strong>Descending</strong> arrow_downward</td>
<td>Supports <code dir="ltr" translate="no">       &lt;      </code> , <code dir="ltr" translate="no">       &lt;=      </code> , <code dir="ltr" translate="no">       ==      </code> , <code dir="ltr" translate="no">       &gt;=      </code> , <code dir="ltr" translate="no">       &gt;      </code> , <code dir="ltr" translate="no">       !=      </code> , <code dir="ltr" translate="no">       in      </code> , and <code dir="ltr" translate="no">       not-in      </code> query clauses on the field and supports sorting results in descending order based on this field value.</td>
</tr>
<tr class="odd">
<td><strong>Array‑contains</strong></td>
<td>Supports <a href="../query-data/queries#array_contains"><code dir="ltr" translate="no">        array-contains       </code></a> and <a href="../query-data/queries#in_and_array-contains-any"><code dir="ltr" translate="no">        array-contains-any       </code></a> query clauses on the field.</td>
</tr>
<tr class="even">
<td><strong>Vector</strong></td>
<td>Supports <a href="/firestore/native/docs/vector-search"><code dir="ltr" translate="no">        FindNearest       </code></a> query clauses on the field.</td>
</tr>
</tbody>
</table>

#### Query scopes

Each index is scoped to either a collection or a collection group. This is known as the index's query scope:

  - Collection scope  
    Firestore Standard edition creates indexes with collection scope by default. These indexes support queries that return results from a single collection.

<!-- end list -->

  - Collection group scope  
    A collection group includes all collections with the same collection ID. To run a [collection group query](../query-data/queries#collection-group-query) that returns filtered or ordered results from a collection group, you must create a corresponding index with collection group scope.

### Default ordering and the `     __name__    ` field

In addition to sorting documents by the index modes specified for each field (ascending or descending) , indexes apply a final sorting by the `  __name__  ` field of each document. The value of the `  __name__  ` field is set to the full document path. This means that documents in the result set with the same field values are sorted by document path.

By default, the `  __name__  ` field is sorted in the same direction of the last sorted field in the index definition. For example:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>arrow_upward name, arrow_upward <code dir="ltr" translate="no">       __name__      </code></td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_downward state, arrow_downward <code dir="ltr" translate="no">       __name__      </code></td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_upward country, arrow_upward population, arrow_upward <code dir="ltr" translate="no">       __name__      </code></td>
<td>Collection</td>
</tr>
</tbody>
</table>

To sort results by the non-default `  __name__  ` direction, you need to create that index.

## Index properties

An index that allows the query to be executed most efficiently is defined by the following properties:

  - Fields used in equality filters
  - Fields used in sort orders
  - Fields used in range and inequality filters (that are not already included in sort orders)
  - Fields used in aggregations (that aren't already included in sort orders and range and inequality filters)

Firestore Standard edition computes the results for queries as follows:

1.  Identifies the index corresponding to the query's collection, filter properties, filter operators, and sort orders.
2.  Identifies the index position from which the scanning starts. The start position is prefixed with the query's equality filters and ends with the range and inequality filters on the first `  orderBy  ` field.
3.  Starts scanning the index, returning each document that satisfies all the filters, until the scanning process does one of the following:
      - Encounters a document that doesn't meet the filter conditions and confirms that any subsequent document will never fully meet the filter conditions.
      - Reaches the end of the index.
      - Collects the maximum number of results requested by the query.

## Indexing example

By automatically creating single-field indexes for you, Firestore Standard edition allows your application to quickly support the most basic database queries. Single-field indexes allow you to perform simple queries based on field values and the comparators `  <  ` , `  <=  ` , `  ==  ` , `  >=  ` , `  >  ` , and `  in  ` . For array fields, they allow you to perform `  array-contains  ` and `  array-contains-any  ` queries.

To illustrate, examine the following examples from the point of view of index creation. The following snippet creates a few `  city  ` documents in a `  cities  ` collection and sets `  name  ` , `  state  ` , `  country  ` , `  capital  ` , `  population  ` , and `  tags  ` fields for each document:

##### Web

``` javascript
var citiesRef = db.collection("cities");

citiesRef.doc("SF").set({
    name: "San Francisco", state: "CA", country: "USA",
    capital: false, population: 860000,
    regions: ["west_coast", "norcal"] });
citiesRef.doc("LA").set({
    name: "Los Angeles", state: "CA", country: "USA",
    capital: false, population: 3900000,
    regions: ["west_coast", "socal"] });
citiesRef.doc("DC").set({
    name: "Washington, D.C.", state: null, country: "USA",
    capital: true, population: 680000,
    regions: ["east_coast"] });
citiesRef.doc("TOK").set({
    name: "Tokyo", state: null, country: "Japan",
    capital: true, population: 9000000,
    regions: ["kanto", "honshu"] });
citiesRef.doc("BJ").set({
    name: "Beijing", state: null, country: "China",
    capital: true, population: 21500000,
    regions: ["jingjinji", "hebei"] });test.firestore.js
```

Assuming the default automatic indexing settings, Firestore Standard edition updates one ascending single-field index per field, one descending single- field index per field, and one array-contains single-field index for the array field. Each row in the following table represents an entry in a single-field index:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Field indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>arrow_upward name</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_upward state</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_upward country</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_upward capital</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_upward population</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_upward regions</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_downward name</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_downward state</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_downward country</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_downward capital</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td>arrow_downward population</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>cities</td>
<td>arrow_downward regions</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>cities</td>
<td><code dir="ltr" translate="no">       array-contains      </code> regions</td>
<td>Collection</td>
</tr>
</tbody>
</table>

### Queries supported by single-field indexes

Using these automatically created single-field indexes, you can run simple queries like the following:

##### Web

``` javascript
const stateQuery = citiesRef.where("state", "==", "CA");
const populationQuery = citiesRef.where("population", "<", 100000);
const nameQuery = citiesRef.where("name", ">=", "San Francisco");test.firestore.js
```

You can also create `  in  ` and compound equality ( `  ==  ` ) queries:

##### Web

``` text
citiesRef.where('country', 'in', ["USA", "Japan", "China"])

// Compound equality queries
citiesRef.where("state", "==", "CO").where("name", "==", "Denver")
citiesRef.where("country", "==", "USA")
         .where("capital", "==", false)
         .where("state", "==", "CA")
         .where("population", "==", 860000)
```

If you need to run a compound query that uses a range comparison ( `  <  ` , `  <=  ` , `  >  ` , or `  >=  ` ) or if you need to sort by a different field, you must create a [composite index](#composite_indexes) for that query.

The `  array-contains  ` index allows you to query the `  regions  ` array field:

##### Web

``` text
citiesRef.where("regions", "array-contains", "west_coast")
// array-contains-any and array-contains use the same indexes
citiesRef.where("regions", "array-contains-any", ["west_coast", "east_coast"])
```

### Queries supported by composite indexes

Firestore Standard edition uses composite indexes to support compound queries not already supported by single-field indexes. For example, you would need a composite index for the following queries:

##### Web

``` text
citiesRef.where("country", "==", "USA").orderBy("population", "asc")
citiesRef.where("country", "==", "USA").where("population", "<", 3800000)
citiesRef.where("country", "==", "USA").where("population", ">", 690000)
// in and == clauses use the same index
citiesRef.where("country", "in", ["USA", "Japan", "China"])
         .where("population", ">", 690000)
```

These queries require the composite index below. Since the query uses an equality ( `  ==  ` or `  in  ` ) for the `  country  ` field, you can use an ascending or descending index mode for this field. By default, inequality clauses apply an ascending sort order based on the field in the inequality clause.

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>arrow_upward (or arrow_downward ) country, arrow_upward population</td>
<td>Collection</td>
</tr>
</tbody>
</table>

To run the same queries but with a descending sort order, you need an additional composite index in the descending direction for `  population  ` :

##### Web

``` text
citiesRef.where("country", "==", "USA").orderBy("population", "desc")

citiesRef.where("country", "==", "USA")
         .where("population", "<", 3800000)
         .orderBy("population", "desc")

citiesRef.where("country", "==", "USA")
         .where("population", ">", 690000)
         .orderBy("population", "desc")

citiesRef.where("country", "in", ["USA", "Japan", "China"])
         .where("population", ">", 690000)
         .orderBy("population", "desc")
```

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td>arrow_upward country, arrow_upward population</td>
<td>Collection</td>
</tr>
<tr class="even">
<td><strong>cities</strong></td>
<td>arrow_upward <strong>country</strong> , arrow_downward <strong>population</strong></td>
<td>Collection</td>
</tr>
</tbody>
</table>

To avoid performance loss caused by [index merging](/datastore/docs/concepts/optimize-indexes#index_merging) , we recommend that you create a composite index to combine an `  array-contains  ` or `  array-contains-any  ` query with additional clauses:

##### Web

``` text
citiesRef.where("regions", "array-contains", "east_coast")
         .where("capital", "==", true)

// array-contains-any and array-contains use the same index
citiesRef.where("regions", "array-contains-any", ["west_coast", "east_coast"])
         .where("capital", "==", true)
```

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>cities</td>
<td><strong>array-contains</strong> tags, arrow_upward (or arrow_downward ) capital</td>
<td>Collection</td>
</tr>
</tbody>
</table>

### Queries supported by collection group indexes

To demonstrate an index with collection group scope, add a `  landmarks  ` sub-collection to some of the `  city  ` documents:

##### Web

``` text
var citiesRef = db.collection("cities");

citiesRef.doc("SF").collection("landmarks").doc().set({
    name: "Golden Gate Bridge",
    category : "bridge" });
citiesRef.doc("SF").collection("landmarks").doc().set({
    name: "Golden Gate Park",
    category : "park" });

citiesRef.doc("DC").collection("landmarks").doc().set({
    name: "National Gallery of Art",
    category : "museum" });
citiesRef.doc("DC").collection("landmarks").doc().set({
    name: "National Mall",
    category : "park" });
```

Using the following single-field index with collection scope, you can query a single city's `  landmarks  ` collection based on the `  category  ` field:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>landmarks</td>
<td>arrow_upward (or arrow_downward ) category</td>
<td>Collection</td>
</tr>
</tbody>
</table>

##### Web

``` text
citiesRef.doc("SF").collection("landmarks").where("category", "==", "park")
citiesRef.doc("SF").collection("landmarks").where("category", "in", ["park", "museum"])
```

If you're interested in querying the landmarks across all cities, for example, you run this query on the collection group that consists of all `  landmarks  ` collections. You must also enable a `  landmarks  ` single-field index with collection group scope:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>landmarks</td>
<td>arrow_upward (or arrow_downward ) category</td>
<td><strong>Collection group</strong></td>
</tr>
</tbody>
</table>

With this index enabled, you can query the `  landmarks  ` collection group:

##### Web

``` text
var landmarksGroupRef = db.collectionGroup("landmarks");

landmarksGroupRef.where("category", "==", "park")
landmarksGroupRef.where("category", "in", ["park", "museum"])
```

To run a collection group query that returns filtered or ordered results, you must enable a corresponding single-field or composite index with collection group scope. Collection group queries that don't filter or order results, however, do not require any additional index definitions.

For example, you can run the following collection group query without enabling an additional index:

##### Web

``` text
db.collectionGroup("landmarks").get()
```

## Index entries

Your project's configured indexes and the structure of a document determine the number of index entries for a document. Index entries count towards the [index entry count limit](#indexing_limits) .

The following example demonstrates the index entries of a document.

#### Document

`  /cities/SF  `

`  city_name : "San Francisco"  `  
`  temperatures : {summer: 67, winter: 55}  `  
`  neighborhoods : ["Mission", "Downtown", "Marina"]  `  

#### Single-Field indexes

  - city\_name ASC
  - city\_name DESC
  - neighborhoods ASC
  - neighborhoods DESC
  - temperatures ASC
  - temperatures DESC
  - temperatures.summer ASC
  - temperatures.summer DESC
  - temperatures.winter ASC
  - temperatures.winter DESC
  - neighborhoods Array Contains

#### Composite indexes

  - city\_name ASC, neighborhoods ARRAY
  - city\_name DESC, neighborhoods ARRAY

#### Index entries

This indexing configuration results in the following index entries for the document:

<table>
<thead>
<tr class="header">
<th>Index</th>
<th>Indexed data</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Single-field index entries</strong></td>
<td></td>
</tr>
<tr class="even">
<td>city_name ASC</td>
<td>city_name: "San Francisco"</td>
</tr>
<tr class="odd">
<td>city_name DESC</td>
<td>city_name: "San Francisco"</td>
</tr>
<tr class="even">
<td>neighborhoods ASC</td>
<td>neighborhoods: ["Mission", "Downtown", "Marina"]</td>
</tr>
<tr class="odd">
<td>neighborhoods DESC</td>
<td>neighborhoods: ["Mission", "Downtown", "Marina"]</td>
</tr>
<tr class="even">
<td>temperatures ASC</td>
<td>temperatures: {summer: 67, winter: 55}</td>
</tr>
<tr class="odd">
<td>temperatures DESC</td>
<td>temperatures: {summer: 67, winter: 55}</td>
</tr>
<tr class="even">
<td>temperatures.summer ASC</td>
<td>temperatures.summer: 67</td>
</tr>
<tr class="odd">
<td>temperatures.summer DESC</td>
<td>temperatures.summer: 67</td>
</tr>
<tr class="even">
<td>temperatures.winter ASC</td>
<td>temperatures.winter: 55</td>
</tr>
<tr class="odd">
<td>temperatures.winter DESC</td>
<td>temperatures.winter: 55</td>
</tr>
<tr class="even">
<td>neighborhoods Array Contains</td>
<td>neighborhoods: "Mission"</td>
</tr>
<tr class="odd">
<td>neighborhoods Array Contains</td>
<td>neighborhoods: "Downtown"</td>
</tr>
<tr class="even">
<td>neighborhoods Array Contains</td>
<td>neighborhoods: "Marina"</td>
</tr>
<tr class="odd">
<td><strong>Composite index entries</strong></td>
<td></td>
</tr>
<tr class="even">
<td>city_name ASC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Mission"</td>
</tr>
<tr class="odd">
<td>city_name ASC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Downtown"</td>
</tr>
<tr class="even">
<td>city_name ASC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Marina"</td>
</tr>
<tr class="odd">
<td>city_name DESC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Mission"</td>
</tr>
<tr class="even">
<td>city_name DESC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Downtown"</td>
</tr>
<tr class="odd">
<td>city_name DESC, neighborhoods ARRAY</td>
<td>city_name: "San Francisco", neighborhoods: "Marina"</td>
</tr>
</tbody>
</table>

## Indexes and pricing

Indexes contribute to the [storage costs](../pricing#storage-size) of your application. For more information about how to calculate storage size for indexes, see [Index entry size](../storage-size#index-entry-size) .

### Use index merging

Although Firestore Standard edition uses an index for every query, it doesn't necessarily require one index per query. For queries with multiple equality ( `  ==  ` ) clauses and, optionally, an `  orderBy  ` clause, Firestore Standard edition can re-use existing indexes. Firestore Standard edition can merge the indexes for simple equality filters to build the composite indexes needed for larger equality queries.

You can reduce indexing costs by identifying situations where you can use index merging. For example, in a `  restaurants  ` collection for a restaurant rating app:

  - collections\_bookmark restaurants
    
      - class burgerthyme
        
        `  name : "Burger Thyme"  `  
        `  category : "burgers"  `  
        `  city : "San Francisco"  `  
        `  editors_pick : true  `  
        `  star_rating : 4  `  

This app uses queries like the following. The app uses combinations of equality clauses for `  category  ` , `  city  ` , and `  editors_pick  ` while always sorting by ascending `  star_rating  ` :

##### Web

``` text
db.collection("restaurants").where("category", "==", "burgers")
                            .orderBy("star_rating")

db.collection("restaurants").where("city", "==", "San Francisco")
                            .orderBy("star_rating")

db.collection("restaurants").where("category", "==", "burgers")
                            .where("city", "==", "San Francisco")
                            .orderBy("star_rating")

db.collection("restaurants").where("category", "==", "burgers")
                            .where("city", "==" "San Francisco")
                            .where("editors_pick", "==", true )
                            .orderBy("star_rating")
```

You could create an index for each query:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>restaurants</td>
<td>arrow_upward category, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>restaurants</td>
<td>arrow_upward city, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>restaurants</td>
<td>arrow_upward category, arrow_upward city, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>restaurants</td>
<td>arrow_upward category, arrow_upward city, arrow_upward editors_pick, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
</tbody>
</table>

As a better solution, you can reduce the number of indexes by taking advantage of Firestore Standard edition's ability to merge indexes for equality clauses:

<table>
<thead>
<tr class="header">
<th>Collection</th>
<th>Fields indexed</th>
<th>Query scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>restaurants</td>
<td>arrow_upward category, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
<tr class="even">
<td>restaurants</td>
<td>arrow_upward city, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
<tr class="odd">
<td>restaurants</td>
<td>arrow_upward editors_pick, arrow_upward star_rating</td>
<td>Collection</td>
</tr>
</tbody>
</table>

Not only is this set of indexes smaller, it also supports an additional query:

##### Web

``` text
db.collection("restaurants").where("editors_pick", "==", true)
                            .orderBy("star_rating")
```

## Indexing limits

The following limits apply to indexes. For more information about quotas and limits, see [Quotas and Limits](../quotas) .

This page identifies the request quotas and limits for Firestore Standard edition.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Limit</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maximum number of composite indexes for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li><p>1000 when you enable billing for your Google Cloud project.</p>
<p>You can <a href="/support-hub">contact support</a> to request an increase to this limit.</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Maximum number of single-field configurations for a database</td>
<td><ul>
<li><p>200 when you have not enabled billing for your Google Cloud project.</p>
<p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
<li>1000 when you enable billing for your Google Cloud project.</li>
</ul>
<p>One field level configuration can contain multiple configurations for the same field. For example, a single-field indexing exemption and a TTL policy on the same field count as one field configuration towards the limit.</p></td>
</tr>
<tr class="odd">
<td><p>Maximum number of index entries for each document</p></td>
<td><p>40,000</p>
<p>The number of index entries is the sum of the following for a document:</p>
<ul>
<li>The number of single-field index entries</li>
<li>The number of composite index entries</li>
</ul>
<p>To see how Firestore Standard edition turns a document and a set of indexes into index entries, see <a href="/firestore/docs/concepts/index-overview#index_entries">this index entry count example</a> .</p></td>
</tr>
<tr class="even">
<td>Maximum number of fields in a composite index</td>
<td>100</td>
</tr>
<tr class="odd">
<td>Maximum size of an index entry</td>
<td><p>7.5 KiB</p>
<p>To see how Firestore Standard edition calculates index entry size, see <a href="/firestore/docs/storage-size#index-entry-size">index entry size</a> .</p></td>
</tr>
<tr class="even">
<td>Maximum sum of the sizes of a document's index entries</td>
<td><p>8 MiB</p>
<p>The total size is the sum of the following for a document:</p>
The sum of the size of a document's single-field index entries
The sum of the size of a document's composite index entries</td>
</tr>
<tr class="odd">
<td>Maximum size of an indexed field value</td>
<td><p>1500 bytes</p>
<p>Field values over 1500 bytes are truncated. Queries involving truncated field values may return inconsistent results.</p></td>
</tr>
</tbody>
</table>

## Indexing best practices

For most apps, you can rely on automatic indexing and the error message links to manage your indexes. However, you may want to add single-field exemptions in the following cases:

Case

Description

Large string fields

If you have a string field that often holds long string values that you don't use for querying, you can cut storage costs by exempting the field from indexing.

High write rates to a collection containing documents with sequential values

If you index a field that increases or decreases sequentially between documents in a collection, like a timestamp, then the maximum write rate to the collection is 500 writes per second. If you don't query based on the field with sequential values, you can exempt the field from indexing to bypass this limit.

In an IoT use case with a high write rate, for example, a collection containing documents with a timestamp field might approach the 500 writes per second limit.

TTL fields

If you use [TTL (time-to-live) policies](/firestore/native/docs/ttl) , note that the TTL field must be a timestamp. Indexing on TTL fields is enabled by default and can affect performance at higher traffic rates. As a best practice, add single-field exemptions for your TTL fields.

Large array or map fields

Large array or map fields can approach the limit of 40,000 index entries per document. If you are not querying based on a large array or map field, you should exempt it from indexing.

If you are using queries with range and inequality operators on multiple fields, see the [indexing considerations](../query-data/multiple-range-fields#best-practices) that you should consider to optimize the performance and cost of Firestore Standard edition queries

For more information about how to resolve indexing issues (index fanout, `  INVALID_ARGUMENT  ` errors) see the [troubleshooting page](https://cloud.google.com/firestore/docs/troubleshooting) .
