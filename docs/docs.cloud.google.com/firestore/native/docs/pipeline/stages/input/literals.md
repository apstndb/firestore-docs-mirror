# Literals (Input Stage)

## Description

Returns documents from a fixed set of predefined document objects.

This stage is commonly used for testing other stages in isolation, though it can also be used as input to join conditions.

## Examples

### Node.js

    const results = await db.pipeline()
      .literals({ name: "joe", age: 10 }, { name: "bob", age: 30 }, { name: "alice", age: 40 })
      .where(field("age").lessThan(35))
      .execute();

## Behavior

The `literals(...)` stage can only be used as the first stage in a pipeline (or sub-pipeline). The order of documents returned from the `literals(...)` matches the order in which they are defined.

While literal values are the most common, it is also possible to pass in expressions, which will be evaluated and returned, making it possible to test out different query / expression behavior without first needing to create some test data.

For example, the following shows how to quickly test out the `length(...)` function on some constant test sets:

### Node.js

    const results = await db.pipeline()
      .literals({ x: constant("foo-bar-baz").length() }, { x: constant("bar").length() })
      .execute();
    
    ...
    
    [
      { x: 11 },
      { x: 3 }
    ]
