# Security Rules for Pipeline operations

[Pipeline operations](/firestore/native/docs/query-data/understanding-core-pipelines#pipeline_operations) rules let you match the filtering capabilities of the existing Rules engine. While Pipeline operations offer a rich set of features, the Rules engine is restricted to recognizing simple filters to ensure query satisfiability and security.

### Edition and mode requirements

This document applies to Firestore Enterprise edition in Native mode.

## Supported Filter Expressions

For a query to be constrained by your rules, it must use standard comparison operators against constants. The following filter types are recognized by the Rules engine:

  - Equality and Inequality: `  eq  ` , `  neq  ` .
  - Comparisons: `  gt  ` , `  gte  ` , `  lt  ` , `  lte  ` .
  - Membership: `  in  ` , `  arrayContains  ` .

Here are some examples:

  - `  where(eq("foo", 2))  `
  - `  where(lt("foo", 2))  `
  - `  documents("/user/1", "/user/2").where(...)  `

**Note:** Complex expressions, such as arithmetic within a filter (for example, `  where(eq("foo" * 2, 10))  ` ) or string functions like `  strContains  ` , are not recognized for constraining queries.

## Request Properties

You can continue to use the `  request  ` object to validate authentication and query context, though some properties available in standard queries are not supported in pipelines.

### Supported properties

The new engine continues to support the following properties:

  - `  request.auth  ` : Access user uid and token data.
  - `  request.method  ` : Identifies the operation (For example, `  get  ` , `  list  ` ).
  - `  request.path  ` : The path of the resource being accessed.
  - `  request.time  ` : The server-side timestamp of the request.

### Unsupported properties

The `  request.query  ` properties such as `  limit  ` , `  offset  ` , and `  orderBy  ` are unsupported for Pipelines rule checks due to the complexity of determining these values in multi-stage queries.

## Pipeline stage handling and permissions

There are different pipeline stages that map to specific granular operations in security rules:

  - `  allow list  ` permissions: Triggered by `  collection()  ` , `  collectionGroup()  ` , and `  database()  ` stages.
  - `  allow get  ` permissions: Triggered by the `  documents()  ` stage, which is treated similarly to a batch `  get  ` operation.
  - Field modification stages: Rules only operate on stored data and not derived values. If a pipeline includes stages that modify fields (For example, `  AddFields  ` , `  ReplaceWith  ` , `  Select  ` ), the Rules engine stops applying filter constraints after that stage is encountered.
  - Literals stage: The `  literals()  ` stage does not read from the database but can incur costs. To prevent abuse, it must be paired with another stage (like `  collection()  ` ) that can be verified by rules.
