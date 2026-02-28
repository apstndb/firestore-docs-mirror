# Literals (Input Stage)

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Description

Returns documents from a fixed set of predefined document objects.

This stage is commonly used for testing other stages in isolation, though it can also be used as input to join conditions.

## Syntax

### Node.js

``` text
const results = await db.pipeline()
  .literals({ name: "joe", age: 10 }, { name: "bob", age: 30 }, { name: "alice", age: 40 })
  .where(field("age").lessThan(35))
  .execute();

...

[
  { name: "joe", age: 10 },
  { name: "bob", age: 30 }
]
```

## Behavior

The `  literals(...)  ` stage can only be used as the first stage in a pipeline (or sub-pipeline). The order of documents returned from the `  literals  ` matches the order in which they are defined.

While literal values are the most common, it is also possible to pass in expressions, which will be evaluated and returned, making it possible to test out different query / expression behavior without first needing to create some test data.

For example, the following shows how to quickly test out the `  length(...)  ` function on some constant test sets:

### Node.js

``` text
const results = await db.pipeline()
  .literals({ x: constant("foo-bar-baz").length() }, { x: constant("bar").length() })
  .execute();

...

[
  { x: 11 },
  { x: 3 }
]
```
