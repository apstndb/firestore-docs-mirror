# Query with range and inequality filters on multiple fields overview

Firestore supports using range and inequality filters on multiple fields in a single query. You can have range and inequality conditions on multiple fields and simplify your application development by delegating implementation of post-filtering logic to Firestore.

## Range and inequality filters on multiple fields

The following query uses range filters on population and density to return all cities where population is higher than 1,000,000 people and population density is less than 10,000 people per unit of area.

### Web version 9 modular

``` text
const q = query(
    collection(db, "cities"),
    where('population', '>', 1000000),
    where('density', '<', 10000),
  );
```

### Swift

``` text
let query = db.collection("cities")
  .whereField("population", isGreaterThan: 1000000)
  .whereField("density", isLessThan: 10000)
```

### Objective-C

``` text
FIRQuery *query =
 [[[[self.db collectionWithPath:@"cities"]
queryWhereField:@"population" isGreaterThan:@1000000]
   queryWhereField:@"density" isLessThan:@10000];
```

### Java Android

``` text
Query query = db.collection("cities")
 .whereGreaterThan("population", 1000000)
 .whereLessThan("density", 10000);
```

### Kotlin+KTX Android

``` text
val query = db.collection("cities")
 .whereGreaterThan("population", 1000000)
 .whereLessThan("density", 10000)
```

### Go

``` text
   query := client.Collection("cities").
      Where("population", ">", 1000000).
      Where("density", "<", 10000)
```

### Java

``` text
db.collection("cities")
  .whereGreaterThan("population", 1000000)
  .whereLessThan("density", 10000);
```

### Node.js

``` text
db.collection("cities")
  .where('population', '>', 1000000),
  .where('density', '<', 10000)
```

### Python

``` text
from google.cloud import firestore

db = firestore.Client()
query = db.collection("cities")
.where("population", ">", 1000000)
.where("density", "<", 10000)
```

### PHP

``` php
$collection = $db->collection('samples/php/cities');
$chainedQuery = $collection
    ->where('population', '>', 1000000)
    ->where('density', '<', 10000);
```

### C\#

``` csharp
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef
    .WhereGreaterThan("Population", 1000000)
    .WhereLessThan("Density", 10000);
QuerySnapshot querySnapshot = await query.GetSnapshotAsync();
foreach (DocumentSnapshot documentSnapshot in querySnapshot)
{
    var name = documentSnapshot.GetValue<string>("Name");
    var population = documentSnapshot.GetValue<int>("Population");
    var density = documentSnapshot.GetValue<int>("Density");
    Console.WriteLine($"City '{name}' returned by query. Population={population}; Density={density}");
}
```

### Ruby

``` text
query = cities_ref.where("population", ">", "1000000")
                  .where("density", "<", 10000)
```

### C++

``` text
CollectionReference cities_ref = db->Collection("cities");
Query query = cities_ref.WhereGreaterThan("population", FieldValue::Integer(1000000))
                       .WhereLessThan("density", FieldValue::Integer(10000));
```

### Unity

``` text
CollectionReference citiesRef = db.Collection("cities");
Query query = citiesRef.WhereGreaterThan("population", 1000000)
                      .WhereLessThan("density", 10000);
```

### Dart

``` text
final citiesRef = FirebaseFirestore.instance.collection('cities')
final query = citiesRef.where("population", isGreaterThan: 1000000)
                  .where("density", isLessThan: 10000);
```

## Indexing considerations

Before you run your queries, read about [queries](/firestore/native/docs/query-data/get-data) and the Firestore [data model](/firestore/native/docs/data-model) .

In Firestore, the `  ORDER BY  ` clause of a query determines which indexes can be used to serve the query. For example, an `  ORDER BY a ASC, b ASC  ` query requires a composite index on the `  a ASC, b ASC  ` fields.

To optimize the performance and cost of Firestore queries, optimize the order of fields in the index. To do this, ensure that your index is ordered from left to right such that the query distills to a dataset that prevents scanning of unnecessary index entries.

Suppose you want to search through a collection of employees and find United States employees whose salary is more than $100,000 and whose number of years of experience is greater than 0. Based on your understanding of the dataset, you know that the salary constraint is more selective than the experience constraint. The ideal index that would reduce the number of index scans would be the `  (salary [...], experience [...])  ` . Thus, the query that would be fast and cost-efficient would order `  salary  ` before `  experience  ` and look as follows:

### Java

``` text
db.collection("employees")
  .whereGreaterThan("salary", 100000)
  .whereGreaterThan("experience", 0)
  .orderBy("salary")
  .orderBy("experience");
```

### Node.js

``` text
db.collection("employees")
  .where("salary", ">", 100000)
  .where("experience", ">", 0)
  .orderBy("salary")
  .orderBy("experience");
```

### Python

``` text
db.collection("employees")
  .where("salary", ">", 100000)
  .where("experience", ">", 0)
  .order_by("salary")
  .order_by("experience");
```

## Best practices for optimizing indexes

When optimizing indexes, note the following best practices.

#### Order index fields by equalities followed by most selective range or inequality field

Firestore uses the leftmost fields of a composite index to satisfy the equality constraints and the range or inequality constraint, if any, on the first field of the `  orderBy()  ` query. These constraints can reduce the number of index entries that Firestore scans. Firestore uses the remaining fields of the index to satisfy other range or inequality constraints of the query. These constraints don't reduce the number of index entries that Firestore scans but filter out unmatched documents so that the number of documents that are returned to the clients are reduced.

For more information about creating efficient indexes, see [index properties](/firestore/native/docs/concepts/index-overview#index_properties) .

#### Order fields in decreasing order of query constraint selectivity

To ensure that Firestore selects the optimal index for your query, specify an `  orderBy()  ` clause that orders fields in decreasing order of query constraint selectivity. Higher selectivity matches a smaller subset of documents, while lower selectivity matches a larger subset of documents. Ensure that you select range or inequality fields with higher selectivity earlier in the index ordering than fields with lower selectivity.

To minimize the number of documents that Firestore scans and returns over the network, you should always order fields in the decreasing order of query constraint selectivity. If the result set is not in the required order and the result set is expected to be small, you can implement client-side logic to reorder it as per your ordering expectation.

For example, suppose you want to search through a collection of employees to find United States employees whose salary is more than $100,000 and order the results by the year of experience of the employee. If you expect only a small number of employees will have salaries greater than $100,000, then the most efficient way to write the query is as follows:

### Java

``` text
db.collection("employees")
  .whereGreaterThan("salary", 100000)
  .orderBy("salary")
  .get()
  .addOnSuccessListener(new OnSuccessListener<QuerySnapshot>() {
        @Override
        public void onSuccess(QuerySnapshot queryDocumentSnapshots) {
          // Order results by `experience`
        }
    });;
```

### Node.js

``` text
const querySnapshot = await db.collection('employees')
                              .where("salary", ">", 100000)
                              .orderBy("salary")
                              .get();

// Order results by `experience`
```

### Python

``` text
results = db.collection("employees")
            .where("salary", ">", 100000)
            .order_by("salary")
            .stream()

// Order results by `experience`
```

While adding an ordering on `  experience  ` to the query will yield the same set of documents and obviate re-ordering the results on the clients, the query may read many more extraneous index entries than the earlier query. This is because Firestore always prefers an index whose index fields prefix match the order by clause of the query. If `  experience  ` were added to the order by clause, then Firestore will select the `  (experience [...], salary [...])  ` index for computing query results. Since there are no other constraints on `  experience  ` , Firestore will read **all** index entries of the `  employees  ` collection before applying the `  salary  ` filter to find the final result set. This means that index entries which don't satisfy the `  salary  ` filter are still read, thus increasing the latency and cost of the query.

## Pricing

Queries with range and inequality filters on multiple fields are billed based on documents read and index entries read.

For detailed information, see the [Pricing](/firestore/native/docs/pricing) page.

## Limitations

Apart from the [query limitations](/firestore/native/docs/query-data/queries#query_limitations) , note the following limitations before using queries with range and inequality filters on multiple fields:

  - Queries with range or inequality filters on document fields and only equality constraints on the document key `  (__name__)  ` aren't supported.
  - Firestore limits the number of range or inequality fields to 10. This is to prevent queries from becoming too expensive to run.

## What's next

  - Learn about [optimizing your queries](/firestore/native/docs/query-data/multiple-range-optimize-indexes) .
  - Learn more about [performing simple and compound queries](/firestore/native/docs/query-data/queries) .
  - Understand how [Firestore uses indexes](/firestore/native/docs/concepts/index-overview) .
