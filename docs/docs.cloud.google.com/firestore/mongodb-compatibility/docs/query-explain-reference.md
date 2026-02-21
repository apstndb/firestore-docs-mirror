# Query execution reference

This page explains the output of a query executed with Query Explain. To learn how to execute a query with Query Explain, see [Analyze query execution with Query Explain](/firestore/mongodb-compatibility/docs/query-explain) .

## Common Concepts

The following common concepts and terms are used throughout the execution tree.

### Rows and records

The terms ***row*** and ***record*** are used to generically refer to a document or index entry.

### Variables

`  $  ` denotes a variable, which is created or referenced in the execution tree. For example: `  $foo_1  ` . These variables are typically used to refer to the contents of a document or the value of an expression evaluated during the execution of a query.

The following internal variables can appear in the execution nodes:

  - `  $__key__  ` - the key is an internal identifier for a document. This is an absolute, unique identifier with the project, database, and the full path of the document.
  - `  $__id__  ` - the ID is a unique identifier for a document within its collection. This is unique within a single collection.
  - `  $rid  ` - the row ID is an internal identifier for a document in storage. This is unique within a single collection.

Consider an example where a `  Compute  ` node is used to compute the `  __id__  ` from the document `  __key__  ` :

``` text
Compute
    |  $__id__1: _id($__key__)
    |  records returned: 1
```

### Constraints and ranges

Some scan nodes use `  constraints  ` and `  ranges  ` attributes to describe the range of values that are scanned. These attributes use a range tree format which contains a list of values. These values correspond to the ordered list of keys which appear in the index definition. For example, the first range which appears in the tree, here `  (1..5]  ` , corresponds to the constraints on the first key, here `  a  ` , in the ordered list of keys:

``` text
| index: type=CollectionGroupIndex, id=CICAgOjXh#EK, keys=[a ASC, b ASC, __key__ ASC]
| constraints: /
               |----(1..5]
                    |----[1L]
```

Each level of indentation indicates the constraint applying to the next key in the list. Square brackets represent an inclusive range, rounded brackets are an exclusive range. In this case, the constraint translates to `  1 < "a" <= 5  ` , and `  "b" = 1  ` .

In the following example with multiple branches for `  a  ` , the constraint corresponds to `  1 < a <= 5 OR a = 10  ` :

``` text
| constraints: /
               |----(1L, 5L]
               |----[10L]
```

### Key Variables

In some scan nodes (such as `  SequentialScan  ` ), there is both a list of keys as part of the `  index  ` attribute, and a separate `  keys  ` attribute in the `  Scan  ` node. The `  keys  ` attribute in the `  Scan  ` node denotes the variable name of each key in the index definition, in order. The variables can be used to reference the runtime values of the scanned field further up in the execution tree.

In the following example, the value of the `  user  ` field for the current document maps to variable `  $user_1  ` and the value of `  date_placed  ` to `  $date_placed_1  ` .

``` text
index: type=CollectionGroupIndex, id=CICAgOjXh4EK, keys=[user ASC, date_placed ASC, __key__ ASC]
keys: [user ASC, date_placed ASC, __key__ ASC]
```

## Execution Nodes

A query execution tree can contain the following nodes.

### SeekingScan

Represents a dynamic scan where the rows returned may not be along a single sequential range of the index, and multiple distinct scans must be performed to satisfy the query.

For example, a query where `  a  ` exists and `  b  ` equals 1 working on an index of `  ["a" ASC, "b" ASC]  ` , would need to scan and return a separate, potentially non-sequential range for each distinct value of `  a  ` . This is more efficient than a full `  TableScan  ` , but less efficient than a single `  SequentialScan  ` on a composite index of `  ["b" ASC, "a" ASC]  ` .

``` text
• SeekingScan
| constraints: /
               |----(-∞..+∞)
                    |----[1L]
| index: type=CollectionGroupIndex, id=CAE, keys=[user ASC, quantity ASC, __key__ ASC]
| keys: [user ASC, quantity ASC, __key__ ASC]
| properties: Selection { user }
| records returned: 1
| records scanned: 1
```

### SequentialScan

Represents a scan of a static, sequential range of rows in storage that can be performed in a single read operation.

The `  key ordering length  ` refers to the number of keys that must be preserved and returned in original key order. For a schema of `  [k1, k2, k3]  ` , a key ordering length of 0 means the scan can return in any order, 1 means order by k1, but rows with the same k1 value can come with any order, 3 returns documents in exact sorted order.

``` text
• SequentialScan
| index: type=CollectionGroupIndex, id=CAE, keys=[user ASC, date_placed ASC, __key__ ASC]
| key ordering length: 3
| keys: [user ASC, date_placed ASC, __key__ ASC]
| limit: 10
| properties: Selection { a }
| ranges: /
| records returned: 1
| records scanned: 1
```

### UniqueScan

Represents a scan of a static, sequential range of rows in storage with in-memory deduplication of rows.

``` text
• UniqueScan
| index: type=CollectionGroupIndex, id=CAE, keys=[user ASC, date_placed ASC, __key__ ASC]
| keys: [user ASC, date_placed ASC, __key__ ASC]
| properties: Selection { a }
| ranges: /
          |----(-∞..+∞)
| records returned: 1
| records scanned: 1
```

### IndexSeek

Represents a dynamic scan where the rows returned may be parametrized by runtime data and might not be along a single sequential range of the index, and multiple distinct scans may be performed to satisfy the query.

For example, a query where `  user  ` equals `  $user_id  ` and `  date_placed  ` equals `  "2025-08-10"  ` running on an index of `  ["user" ASC, "date_placed" ASC]  ` , would use the value of the `  $user_id  ` variable at runtime and the `  "2025-08-10"  ` constraint on `  date_placed  ` to restrict the scan ranges.

``` text
• IndexSeek
| index: type=CollectionGroupIndex, id=CAE, keys=[user ASC, date_placed ASC, __key__ ASC]
| fields: [$user_1 ASC, $date_placed_1 ASC, $rid ASC]
| key: $key_1
| filter: $eq($user_1, $user_id) AND $eq($date_placed_1, "2025-08-10")
| records returned: 1
| records scanned: 1
```

### Fetch

Back-joins the supplied row's identifier to the actual row contents from primary storage. `  Fetch  ` is required if a parent node (or the final query result) requires a subset of fields from the documents.

``` text
• Fetch
|  order: PRESERVE_INPUT_ORDER
|  peak memory usage: 4.00 KiB (4,096 B)
|  properties: *
|  records returned: 1
```

### LookupById

Performs a join by looking up documents in a foreign collection by their ID. The IDs to look up are sourced from a field in the input documents. The results of the lookup are added as a new field to the input documents.

``` text
• LookupById
|  local_field: $localField_1
|  foreign_datasource: (default)#/**/foreign
|  output: $output_1
```

### TableScan

A full, unordered scan of a collection. Used when a query is run without an associated index.

Order can be either `  STABLE  ` or `  UNDEFINED  ` , with `  STABLE  ` denoting a deterministic ordering.

``` text
• TableScan
|  order: STABLE
|  properties: *
|  records returned: 1
|  records scanned: 1
|  source: (default)#/**/collection
```

### Apply

Performs a join between two sets of data ( `  input  ` and `  map  ` ) by iterating through each row of the `  input  ` and, for each row, scanning and returning results from the `  map  ` side.

The `  join_type  ` indicates the type of join. For example, `  LEFT_OUTER  ` means all rows from the `  input  ` are included at least once in the output. If an `  input  ` row does not find any results from the `  map  ` side, it will still be included, with `  null  ` values for the columns from the `  map  ` side.

``` text
• Apply
|  join_type: LEFT_OUTER
|
└── • input tree
|     ...
└── • map tree
      ...
```

### HashAggregate

Hash-backed implementation of aggregate operations. Requires materializing the full group in-memory before returning the result and must not exceed the the [query memory limit](/firestore/mongodb-compatibility/quotas#reads_writes_and_transactions) .

``` text
• HashAggregate
|  aggregations: [sum($b_1) AS total]
|  groups: [$a_1]
|  peak memory usage: 4.00 KiB (4,096 B)
|  records returned: 0
```

### StreamAggregate

Specialized aggregate node which only maintains state for a single group at a time, reducing peak memory usage. Used when the underlying child node will return groups sequentially. For example, when grouping by distinct values of a field while using an index on that field.

``` text
• StreamAggregate
|  keys: [foo ASC, bar ASC]
|  properties: Selection { baz }
|  aggregations: [$sum($foo_1) AS baz]
```

### MajorSort

Performs a sort operation on a fixed set of properties. Materializes all records in memory at once and returns the sorted values in order, the size of the sort set is limited by the [query memory limit](/firestore/mongodb-compatibility/quotas#reads_writes_and_transactions) .

When a subsequent limit is provided, a top-k sorting algorithm is used to reduce the memory usage. With it, sorts can be performed on an arbitrarily large set of records so long as the memory used by storing the k considered elements does not exceed the limit.

``` text
• MajorSort
|  fields: [a ASC, b DESC]
|  limit: 10
|  peak memory usage: 4.00 KiB (4,096 B)
|  records returned: 1
```

### Concat

Concatenates the results of multiple child nodes and returns the result to the parent node. This node does not deduplicate results that appear in multiple children, and the order of returned results is nondeterministic.

``` text
• Concat
├── • Fetch
...
├── • Fetch
```

### Compute

Evaluates a set of expressions, assigning the results to a set of variables.

``` text
• Compute
|  $user_1: user
|  $full_name_1: str_concat($first_name_1, " ", $last_name_1)
|  $address_1: UNSET
|  records returned: 1
```

### Filter

Selectively returns rows if and only if they match the supplied expression.

``` text
• Filter
|  expression: $eq(foo, "bar")
|  records returned: 1
```

### RecordCount

Counts the number of rows produced by the child node and emits the current count to the variable specified in the `  count  ` attribute.

``` text
• RecordCount
|  count: $row_number_1
|  records returned: 1
```

### Values

Produces a sequence of literal values to work on. Used primarily when a set list of documents is provided as the input to a query.

``` text
• Values
| expression: [{__key__=/col/1}, {__key__=/col/2}]
```

### Unnest

Unnests the value produced by the child node.

``` text
• Unnest
|  expression: foo AS unnested_foo
```

### Limit

Limits the number of rows returned to the parent node.

``` text
• Limit
|  limit: 10
|  records returned: 1
```

### Offset

Skips a set number of rows produced by the child node.

``` text
• Offset
|  offset: 10
|  records returned: 1
```
