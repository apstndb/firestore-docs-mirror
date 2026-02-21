This page describes concepts to consider when selecting Firestore in Datastore mode indexes for your app.

Firestore in Datastore mode delivers high query performance by using indexes for all queries. Performance for most queries depends on the size of the result set and not on the total size of the database.

Firestore in Datastore mode defines built-in indexes for each property in an entity. These single property indexes support many simple queries. Firestore in Datastore mode supports an index merging feature that lets your database merge built-in indexes to support additional queries. For more complex queries, you must define composite indexes ahead of time.

This page focuses on the index merging feature, because it affects two important index optimization opportunities:

  - Speeding up queries
  - Reducing the number of composite indexes

The following example demonstrates the index merging feature.

## Filtering `     Photo    ` entities

Consider a Datastore mode database with entities of kind `  Photo  ` :

Photo

Property

Value type

Description

`  owner_id  `

String

User id

`  tag  `

Array of strings

Tokenized keywords

`  size  `

Integer

Enumeration:

  - `  1 icon  `
  - `  2 medium  `
  - `  3 large  `

`  coloration  `

Integer

Enumeration:

  - `  1 black & white  `
  - `  2 color  `

Imagine that you require an app feature that lets users query `  Photo  ` entities based on a logical `  AND  ` of the following:

  - Up to three filters based on the properties:
    
      - `  owner_id  `
      - `  size  `
      - `  coloration  `

  - A `  tag  ` search string. The app tokenizes the search string into tags and adds a filter for each tag.
    
    For example, the app turns the search string `  outside, family  ` into the query filters `  tag=outside  ` and `  tag=family  ` .

Using built-in indexes and Firestore in Datastore mode's index merging feature, you can meet the index requirements of this `  Photo  ` filter feature without adding additional composite indexes.

The built-in indexes for `  Photo  ` entities support single-filter queries like:

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_owner_id = client.query(kind="Photo", filters=[("owner_id", "=", "user1234")])

query_size = client.query(kind="Photo", filters=[("size", "=", 2)])

query_coloration = client.query(kind="Photo", filters=[("coloration", "=", 2)])
```

The `  Photo  ` filter feature also requires queries that combine multiple equality filters with a logical `  AND  ` :

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_all_properties = client.query(
    kind="Photo",
    filters=[
        ("owner_id", "=", "user1234"),
        ("size", "=", 2),
        ("coloration", "=", 2),
        ("tag", "=", "family"),
    ],
)
```

Firestore in Datastore mode can support these queries by merging built-in indexes.

## Index merging

Firestore in Datastore mode can use index merging when your query and your indexes meet all of the following constraints:

  - The query uses only equality ( `  =  ` ) filters
  - No composite index exists that perfectly matches the filters and ordering of the query
  - Each equality filter matches at least one existing index with the same ordering as the query

In this situation, Firestore in Datastore mode can use existing indexes to support the query instead of requiring you to configure an additional composite index.

When two or more indexes are sorted by the same criteria, Firestore in Datastore mode can merge the results of multiple index scans to find the results that are common to all such indexes. Firestore in Datastore mode can merge built-in indexes, because they all sort values by entity key.

By merging built-in indexes, Firestore in Datastore mode supports queries with equality filters on multiple properties:

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_all_properties = client.query(
    kind="Photo",
    filters=[
        ("owner_id", "=", "user1234"),
        ("size", "=", 2),
        ("coloration", "=", 2),
        ("tag", "=", "family"),
    ],
)
```

Firestore in Datastore mode can also merge index results from multiple sections of the same index. By merging different sections of the built-in index for the `  tag  ` property, Firestore in Datastore mode supports queries that combine multiple `  tag  ` filters in a logical `  AND  ` :

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_tag = client.query(
    kind="Photo",
    filters=[
        ("tag", "=", "family"),
        ("tag", "=", "outside"),
        ("tag", "=", "camping"),
    ],
)

query_owner_size_color_tags = client.query(
    kind="Photo",
    filters=[
        ("owner_id", "=", "user1234"),
        ("size", "=", 2),
        ("coloration", "=", 2),
        ("tag", "=", "family"),
        ("tag", "=", "outside"),
        ("tag", "=", "camping"),
    ],
)
```

The queries supported by merged built-in indexes complete the set of queries required by the `  Photo  ` filtering feature. Note that supporting the `  Photo  ` filtering feature did not require any additional composite indexes.

When selecting the optimal indexes for your app, it's important to understand the index merging feature. Index merging gives Firestore in Datastore mode greater query flexibility but with a possible trade-off to performance. The next section describes the performance of index merging, and how to improve performance by adding composite indexes.

## Finding the perfect index

The index is sorted first by ancestor and then by property values, in the order specified in the index definition. The *perfect composite index* for a query, which allows the query to be executed most efficiently, is defined on the following properties, in order:

1.  Properties used in equality filters
2.  Properties used in sort orders
3.  Properties used in `  distinctOn  ` filter
4.  Properties used in range & inequality filters (that are not already included in sort orders)
5.  Properties used in aggregations and [projections](/datastore/docs/concepts/queries#projection_queries) (that are not already included in sort orders and range & inequality filters)

This ensures that all results for every possible execution of the query are accounted. Firestore in Datastore mode databases execute a query using a perfect index using the following steps:

1.  Identifies the index corresponding to the query's kind, filter properties, filter operators, and sort orders
2.  Scans from the beginning of the index to the first entity that meets all or a subset of the query's filter conditions
3.  Continues scanning the index, returning each entity that satisfies all the filter conditions, until it
      - encounters an entity that does not meet the filter conditions, or
      - reaches the end of the index, or
      - has collected the maximum number of results requested by the query

For example, consider the following query:

``` text
SELECT * FROM Task
WHERE category = 'Personal'
  AND priority < 3
ORDER BY priority DESC
```

The perfect composite index for this query is an index of keys for entities of kind `  Task  ` , with columns for the values of the `  category  ` and `  priority  ` properties. The index is sorted first in ascending order by `  category  ` and then in descending order by `  priority  ` :

``` text
indexes:
- kind: Task
  properties:
  - name: category
    direction: asc
  - name: priority
    direction: desc
```

Two queries of the same form but with different filter values use the same index. For example, the following query uses the same index as the earlier query:

``` text
SELECT * FROM Task
WHERE category = 'Work'
  AND priority < 5
ORDER BY priority DESC
```

For this index

``` text
indexes:
- kind: Task
  properties:
  - name: category
    direction: asc
  - name: priority
    direction: asc
  - name: created
    direction: asc
```

The earlier index can satisfy both of the following queries:

``` text
SELECT * FROM Task
WHERE category = 'Personal'
  AND priority = 5
ORDER BY created ASC
```

and

``` text
SELECT * FROM Task
WHERE category = 'Work'
ORDER BY priority ASC, created ASC
```

**Caution:** Using a perfect index can significantly increase [storage size](/datastore/docs/concepts/storage-size) and write latency, especially in the case of [exploding indexes](/datastore/docs/concepts/indexes#index_limits) .

## Optimizing your index selection

This section describes the performance characteristics of index merging and two optimization opportunities related to index merging:

  - Add composite indexes to speed up queries that rely on merged indexes
  - Reduce the number of composite indexes by leveraging merged indexes

### Index merge performance

In an index merge, Firestore in Datastore mode efficiently merges indexes using a [zig-zag merge join algorithm](https://youtu.be/ofhEyDBpngM?t=584) . Using this algorithm, Datastore mode joins potential matches from multiple index scans to produce a result set that matches a query. Index merging combines filter components at read-time instead of write-time. Unlike most Firestore in Datastore mode queries where performance depends only on the size of the result set, performance for index-merge queries depends on the filters in the query and how many potential matches the database considers.

The best-case performance of an index merge happens when every potential match in an index satisfies the query filters. In this case, performance is `  O(R * I)  ` where `  R  ` is the size of the result set and `  I  ` is the number of indexes scanned.

The worst-case performance happens when the database must consider many potential matches but few of them satisfy the query filters. In this case, performance is `  O(S)  ` where `  S  ` is the size of the smallest set of potential entities from a single index scan.

The actual performance depends on the shape of the data. The average number of entities considered for each result returned is `  O(S/(R * I))  ` . Queries perform worse when many entities match each index scan but few entities match the query as a whole, meaning `  R  ` is small and `  S  ` is large.

Four things mitigate this risk:

  - The query planner does not look up an entity until it knows the entity matches the entire query.

  - The zig-zag algorithm does not need to find all results to return the next result. If you request the first 10 results, you only pay the latency for finding those 10 results.

  - The zig-zag algorithm skips large sections of false positive results. The worst-case performance happens only if false positive results are perfectly interwoven (in sort order) between scans.

  - Latency depends on the number of entities found in each index scan, not the number of entities that match each filter. As shown in the next section, you can add composite indexes to improve index merge performance.

### Speeding up an index-merge query

When Firestore in Datastore mode merges indexes, each index scan often maps to a single filter in the query. You can improve query performance by adding composite indexes that match multiple filters in the query.

**Note:** For brevity, this section uses a shorthand notation for index definitions. The following definition denotes an index of kind `  model  ` , with property `  prop1  ` ascending and `  prop2  ` descending:

``` text
Index(model, prop1, -prop2)
```

This is equivalent to the following configuration in `  index.yaml  ` :

``` text
indexes:
- kind: model
  ancestor: no
  properties:
  - name: prop1
  - name: prop2
    direction: desc
```

Consider this query:

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_owner_size_tag = client.query(
    kind="Photo",
    filters=[
        ("owner_id", "=", "username"),
        ("size", "=", 2),
        ("tag", "=", "family"),
    ],
)
```

Each filter maps to one index scan in the following built-in indexes:

``` text
Index(Photo, owner_id)
Index(Photo, size)
Index(Photo, tag)
```

If you add the composite index `  Index(Photo, owner_id, size)  ` , the query maps to two index scans instead of three:

``` text
#  Satisfies both 'owner_id=username' and 'size=2'
Index(Photo, owner_id, size)
Index(Photo, tag)
```

Consider a scenario with many large images, many black-and-white images, but few large, panoramic images. A query filtering for both panoramic and black-and-white images will be slow if it merges built-in indexes:

### Python

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_size_coloration = client.query(
    kind="Photo", filters=[("size", "=", 2), ("coloration", "=", 1)]
)
```

To improve query performance, you can lowers the value of `  S  ` (smallest set of entities in a single index scan) in `  O(S/(R * I))  ` by adding the following composite index:

``` text
Index(Photo, size, coloration)
```

Compared to using two built-in indexes, this composite index produces fewer potential results for the same two query filters. This approach substantially improves performance at the cost of one more index.

### Reducing the number of composite indexes with index merging

Although composite indexes that exactly match the filters in a query perform best, it's not always best or possible to add a composite index for every combination of filters. You must balance your composite indexes against the following:

  - Composite index limits:
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Limit</th>
    <th>Amount</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Maximum number of composite indexes for a database</td>
    <td><ul>
    <li><p>200 when you have not enabled billing for your Google Cloud project.</p>
    <p>If you need more quota, you must <a href="https://cloud.google.com/billing/docs/how-to/modify-project">enable billing for your Google Cloud project.</a></p></li>
    <li><p>1000 when you enable billing for your Google Cloud project.</p>
    <p>You can <a href="https://cloud.google.com/support-hub">contact support</a> to request an increase to this limit.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td>Maximum sum of the sizes of an entity's <a href="https://cloud.google.com/datastore/docs/concepts/indexes#composite_indexes">composite index</a> entries</td>
    <td>2 MiB</td>
    </tr>
    <tr class="odd">
    <td>Maximum sum of the following for an entity:
    <ul>
    <li>the number of indexed property values</li>
    <li>the number of composite index entries</li>
    </ul></td>
    <td>20,000</td>
    </tr>
    </tbody>
    </table>

  - Storage costs of each additional index.

  - Effects on write latency.

Indexing issues often arise with multi-value fields like the `  tag  ` property of the `  Photo  ` entities.

For example, imagine that the `  Photo  ` filtering feature now needs to support descending ordering clauses based on four additional properties:

Photo

Property

Value type

Description

`  date_added  `

Integer

Date/time

`  rating  `

Float

Aggregate user rating

`  comment_count  `

Integer

Number of comments

`  download_count  `

Integer

Number of downloads

If you disregard the `  tag  ` field, it's possible to select composite indexes that match every combination of `  Photo  ` filters:

``` text
Index(Photo, owner_id, -date_added)
Index(Photo, owner_id, -comments)
Index(Photo, size, -date_added)
Index(Photo, size, -comments)
...
Index(Photo, owner_id, size, -date_added)
Index(Photo, owner_id, size, -comments)
...
Index(Photo, owner_id, size, coloration, -date_added)
Index(Photo, owner_id, size, coloration, -comments)
```

The total number of composite indexes is:

``` text
2^(number of filters) * (number of different orders) = 2 ^ 3 * 4 = 32 composite indexes
```

If you try to support up to 3 `  tag  ` filters, the total number of composite indexes is:

``` text
2 ^ (3 + 3 tag filters) * 4 = 256 indexes.
```

Indexes that include multi-value properties like `  tag  ` also lead to [exploding index issues](/datastore/docs/concepts/indexes#index_limits) that increase storage costs and write latency.

To support filters on the `  tag  ` field for this feature, you can reduce the total number of indexes by relying on merged indexes. The following set of composite indexes is the minimum required to support the `  Photo  ` filtering feature with ordering:

``` text
Index(Photo, owner_id, -date_added)
Index(Photo, owner_id, -rating)
Index(Photo, owner_id, -comments)
Index(Photo, owner_id, -downloads)
Index(Photo, size, -date_added)
Index(Photo, size, -rating)
Index(Photo, size, -comments)
Index(Photo, size, -downloads)
...
Index(Photo, tag, -date_added)
Index(Photo, tag, -rating)
Index(Photo, tag, -comments)
Index(Photo, tag, -downloads)
```

The number of composite indexes defined is:

``` text
(number of filters + 1) * (number of orders) = 7 * 4 = 28
```

Index merging also provides the following benefits:

  - Allows a `  Photo  ` entity to support up to 1000 tags with no limit on the number of `  tag  ` filters per query.
  - Reduces the total number of indexes which reduces storage costs and write latency.

## Selecting indexes for your app

You can select optimal indexes for your Datastore mode database by using two approaches:

  - Use index merging to support additional queries
    
      - Requires less composite indexes
      - Reduces storage cost per entity
      - Improves write latency
      - Avoids exploding indexes
      - Performance depends on the shape of the data

  - Define a composite index that matches multiple filters in a query
    
      - Improves query performance
      - Consistent query performance that's not dependent on shape of data
      - Must stay under the [limit of composite indexes](/datastore/docs/concepts/limits#limits)
      - Increased storage cost per entity
      - Increased write latency

When figuring out the optimal indexes for your app, the answer can change as the shape of your data changes. Sampling query performance gives you a good idea of your app's common queries and its slow queries. With this information, you can add indexes to improve the performance of queries that are both common and slow.
