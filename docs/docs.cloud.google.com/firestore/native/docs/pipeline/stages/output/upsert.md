---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/upsert
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/upsert
title: Upsert (Output Stage)
description: Learn how to use the upsert stage in Firestore Pipeline Operations to upsert documents.
data_source: docs.cloud.google.com
---

# Upsert (Output Stage)

## Description

`upsert()` is a Data manipulation language (DML) stage that updates existing documents or inserts new documents if they don't exist. This stage can be attached to the end of a query.

The `upsert()` stage can take different arguments to determine the destination collection, document ID, and optional field transformations:

- `upsert(collectionName, documentIdExpression, ...transformations)` : Upserts documents into the specified collection, using the evaluated expression to determine the document ID, and applies optional transformations.
- `upsert(collectionName, ...transformations)` : Upserts documents into the specified collection, requiring a `__name__` field in the input document to determine the document ID, and applies optional transformations.
- `upsert(...transformations)` : Upserts documents, requiring a `__name__` field in the input document to determine the destination collection and document ID, and applies optional transformations.

## Examples

### Migrate active users

The following example queries the `users` collection where `age >= 25` , adds a `processed` field, and upserts into `new_users` using the `name` field as the document ID:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("users") .where(field("age").greaterThanOrEqual(25)) .addFields(constant(true).as("processed")) .upsert({ collection: "new_users", documentId: field("name") }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("users") .where(field("age").greaterThanOrEqual(25)) .addFields(constant(true).as("processed")) .upsert(new Upsert().withCollection("new_users").withDocumentId(field("name"))); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

## Behavior

The following sections describe the execution behavior, responses, transformations, and restrictions for the `upsert()` stage.

### Upsert in place with field transformations

The following example updates existing documents in the `users` collection in place by modifying or adding fields during the upsert:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("users") .upsert(\[constant(31).as("age")\]) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("users") .upsert(constant(31L).as("age")); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert into a different collection with explicit ID

The following example reads from `source_coll` and upserts documents into `target_coll` using an explicit document ID `"new_doc_id"` and applying a field transformation:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("source_coll") .upsert( \[constant(31).as("age")\], { collection: "target_coll", documentId: constant("new_doc_id") } ) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("source_coll") .upsert(new Upsert(constant(31L).as("age")) .withCollection("target_coll") .withDocumentId(constant("new_doc_id"))); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert into another collection using existing document ID ( `__name__` )

The following example reads documents from `source_coll` and upserts them into `target_coll` using each document's existing document ID ( `__name__` ):

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("source_coll") .upsert(\[constant("updated_val").as("status")\], { collection: "target_coll" }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("source_coll") .upsert(new Upsert(constant("updated_val").as("status")) .withCollection("target_coll")); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert with document references ( `__name__` )

The following example uses document references assigned to the `__name__` field to specify destination collection and document ID:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .literals(\[ { \_\_name\_\_: db.doc("users/bob"), name: "bob", age: 30 }, { \_\_name\_\_: db.doc("users/alice"), name: "alice", age: 25 } \]) .upsert() ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("\_\_name\_\_", db.document("users/bob"), "name", "bob", "age", 30), Map.of("\_\_name\_\_", db.document("users/alice"), "name", "alice", "age", 25)) .upsert(new Upsert()); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert with auto-generated document IDs

The following example upserts literals into the `users` collection with auto-generated document IDs and field transformations:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .literals(\[ { foo: "bar" }, { foo: "baz" } \]) .upsert(\[constant("active").as("status")\], { collection: "users" }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("foo", "bar"), Map.of("foo", "baz")) .upsert(new Upsert(constant("active").as("status")) .withCollection("users")); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert into a Subcollection

The `upsert()` stage can be used to insert or update documents directly into a subcollection using a full path.

##### Node.js

\`\`\`js const results = await db.pipeline() .literals(\[ { title: "post1" }, { title: "post2" } \]) .upsert(\[\], { collection: "users/u1/posts" }) .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("title", "post1"), Map.of("title", "post2")) .upsert(new Upsert().withCollection("users/u1/posts")); pipeline.execute(); \`\`\`

### Upsert from Advanced Queries (Search and Find Nearest)

The `upsert()` stage can be used with advanced query operations like `search` or `findNearest` to write the matching documents into an output collection or update them in place.

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("products") .search({ query: "shoes" }) .upsert(\[constant(true).as("is_shoes")\]) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("products") .search(searchOptionsBuilder().query(documentMatches("shoes"))) .upsert(new Upsert(constant(true).as("is_shoes"))); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Upsert from Aggregation Subqueries

The `upsert()` stage can be used with aggregation subqueries and scalar functions to update documents based on dynamically computed values, such as identifying if a user has the top score. This pattern must be executed within a user transaction.

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("users") .where( field("score").equal( scalar( db.pipeline() .collection("scores") .aggregate({ accumulators: \[max(field("points")).as("max_points")\] }) .select(field("max_points")) ) ) ) .upsert(\[constant(true).as("is_top_scorer")\]) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("users") .where( eq( field("score"), scalar( db.pipeline() .collection("scores") .aggregate(max(field("points")).as("max_points")) .select(field("max_points"))))) .upsert(new Upsert(constant(true).as("is_top_scorer"))); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Response

The `upsert()` stage always emits a single document like `{ documents_modified: 3 }` describing how many documents were inserted or updated.

### Final Stage

The `upsert()` stage must come at the end of a pipeline, no further stages can be provided.

### Transaction Required

The `upsert()` stage requires a transaction. It must be run within an active read-write transaction, or with the `atomic` (Node.js) or `auto_commit` option set to true when starting a new transaction.

### Response

The response includes a summary of the number of documents modified. For example, the following response confirms that the pipeline modified three documents:

```
{documents_modified: 3L}
```

### Limitations

- DML stages can now be run within transactions. The `insert()` and `upsert()` stages need to be run within a transaction in most cases.

- When executing a pipeline with DML stages within a new transaction, you can use the `atomic` option to automatically run within a transaction and commit upon successful execution of the pipeline.

- When running within a transaction, there are no restrictions on other stages (such as `where` , `addFields` , `union` , `findNearest` , and `aggregate` subqueries). Transactional DML operations are bounded by Firestore Enterprise edition transaction limits. Because transactions don't allow reads after the first write, you cannot call a DML pipeline multiple times within a single transaction or read documents after a DML pipeline executes. Attempting to execute a read after a DML write fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`

- When running outside of a transaction:

  - Each document is updated independently of each other, and writes are not atomic across documents. The pipeline halts on the first error, allowing for partial success to occur.
  - Advanced multi-query stages ( `aggregate` , `distinct` , `unnest` , `find_nearest` , `union` , joins, and subqueries) are not supported.

- Under Firebase Security Rules, each batch of documents re-evaluates rules and executes lookups. If rules use `get()` or `exists()` , the global 20-lookup limit is reached after writing approximately 200 documents, and the operation fails with `PERMISSION_DENIED` . Use Custom Claims instead of `get()` / `exists()` lookups to avoid this limit.

- If the stage preceding the DML stage produces multiple documents with the same `__name__` or evaluates to the same destination document ID, each mutation is processed sequentially:

  - For `upsert(...)` and `update(...)` : Multiple mutations targeting the same document follow "last one wins" semantics, where the last mutation processed determines the final state of the document.
  - For `delete(...)` : The first attempt deletes the document, and subsequent attempts for the same document are no-ops.
  - For `insert(...)` : The first attempt creates the document, and subsequent attempts targeting the same document ID fail with an `ALREADY_EXISTS` error.

### Transactional Execution

DML operations can be executed as part of a read-write transaction by either providing an explicit transaction to the pipeline execution call or by using the `atomic` option.

Firestore transactions require all reads to execute before any writes. Because a DML pipeline executes writes, you cannot perform reads (such as document lookups or query reads) after running a DML pipeline in the same transaction. For example, you cannot call a DML pipeline multiple times in a single transaction. Attempting to read after a DML pipeline executes fails with a `FAILED_PRECONDITION` error: `Cannot have reads after the first write in a Firestore transaction.`

#### Using an explicit transaction

##### Node.js

\`\`\`js // Execute a pipeline with DML stage within an explicit transaction const pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); await db.runTransaction(async (transaction) =\> { return transaction.execute(pipeline); }); \`\`\`

##### Java

\`\`\`java // Execute a pipeline with DML stage within an explicit transaction Pipeline pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

#### Using the `atomic` option

##### Node.js

\`\`\`js // Execute a pipeline const results = await db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update() .execute({ atomic: true }); \`\`\`

##### Java

\`\`\`java // Execute a pipeline passing atomic option to execute() Pipeline pipeline = db.pipeline() .collection("users") .where(field("active").equal(false)) .addFields(constant("inactive").as("status")) .update(); pipeline.execute(new PipelineExecuteOptions().withAtomic(true)); \`\`\`
