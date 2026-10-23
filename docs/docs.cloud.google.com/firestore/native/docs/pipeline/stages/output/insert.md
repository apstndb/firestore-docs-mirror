---
name: documents/docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/insert
uri: https://docs.cloud.google.com/firestore/native/docs/pipeline/stages/output/insert
title: Insert (Output Stage)
description: Learn how to use the insert stage in Firestore Pipeline Operations to insert documents.
data_source: docs.cloud.google.com
---

# Insert (Output Stage)

## Description

`insert()` is a Data manipulation language (DML) stage that adds new documents to Firestore. This stage can be attached to the end of a query to insert the results of that query into a collection.

The `insert()` stage can take different arguments to determine the destination collection and document ID:

- `insert(collectionName, documentIdExpression)` : Inserts documents into the specified collection, using the evaluated expression to determine the document ID.
- `insert(collectionName)` : Inserts documents into the specified collection, automatically generating document IDs.
- `insert()` : Inserts documents, requiring a `__name__` field in the input document to determine the destination collection and document ID.

## Examples

### Insert static documents

The following example inserts new documents into the `users` collection, using the `id` field from the input to define the document IDs:

##### Node.js

\`\`\`js const results = await db.pipeline() .literals(\[ { foo: "bar", id: "doc1" }, { foo: "baz", id: "doc2" } \]) .insert({ collection: "users", documentId: field("id") }) .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("foo", "bar", "id", "doc1"), Map.of("foo", "baz", "id", "doc2")) .insert(new Insert().withCollection("users").withDocumentId(field("id"))); pipeline.execute(); \`\`\`

## Behavior

The following sections describe the execution behavior, responses, and restrictions for the `insert()` stage.

### Evaluated Document ID Expression

The following example computes new document IDs using a string concatenation expression `stringConcat(...)` and inserts the results into `new_users` inside an explicit transaction:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("users") .distinct(field("name")) .insert({ collection: "new_users", documentId: stringConcat(constant("new\_"), field("name")), }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("users") .distinct(field("name")) .insert(new Insert() .withCollection("new_users") .withDocumentId(stringConcat(constant("new\_"), field("name")))); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Document References ( `__name__` )

The following example uses document references assigned to the `__name__` field to specify both destination collection and document ID:

##### Node.js

\`\`\`js const results = await db.pipeline() .literals(\[ { \_\_name\_\_: db.doc("users/doc1"), foo: "bar" }, { \_\_name\_\_: db.doc("users/doc2"), foo: "baz" } \]) .insert() .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("\_\_name\_\_", db.document("users/doc1"), "foo", "bar"), Map.of("\_\_name\_\_", db.document("users/doc2"), "foo", "baz")) .insert(new Insert()); pipeline.execute(); \`\`\`

### Auto-Generated IDs

The following example inserts new documents into the `users` collection, allowing Firestore to auto-generate the document IDs:

##### Node.js

\`\`\`js const results = await db.pipeline() .literals(\[ { foo: "bar" }, { foo: "baz" } \]) .insert({ collection: "users" }) .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("foo", "bar"), Map.of("foo", "baz")) .insert(new Insert().withCollection("users")); pipeline.execute(); \`\`\`

### Insert Into a Subcollection

The `insert()` stage can be used to insert documents directly into a subcollection using a full path.

##### Node.js

\`\`\`js const results = await db.pipeline() .literals(\[ { title: "post1" }, { title: "post2" } \]) .insert({ collection: "users/u1/posts" }) .execute(); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .literals( Map.of("title", "post1"), Map.of("title", "post2")) .insert(new Insert().withCollection("users/u1/posts")); pipeline.execute(); \`\`\`

### Insert Into a Different Collection

The `insert()` stage can read from one collection, apply transformations, and write into another collection within a transaction:

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("source_coll") .where(field("active").equal(true)) .addFields(constant("val").as("new_field")) .insert({ collection: "target_coll" }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("source_coll") .where(field("active").equal(true)) .addFields(constant("val").as("new_field")) .insert(new Insert().withCollection("target_coll")); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Insert from Advanced Queries (Search and Find Nearest)

The `insert()` stage can be used with advanced query operations like `search` or `findNearest` to write the matching documents into an output collection.

##### Node.js

\`\`\`js const results = await db.runTransaction(async (transaction) =\> { return transaction.execute( db.pipeline() .collection("products") .search({ query: "shoes" }) .insert({ collection: "matched_products" }) ); }); \`\`\`

##### Java

\`\`\`java Pipeline pipeline = db.pipeline() .collection("products") .search(searchOptionsBuilder().query(documentMatches("shoes"))) .insert(new Insert().withCollection("matched_products")); db.runTransaction(transaction -\> { transaction.execute(pipeline); return null; }); \`\`\`

### Response

The `insert()` stage always emits a single document like `{ documents_modified: 2 }` describing how many documents were inserted.

### Final Stage

The `insert()` stage must come at the end of a pipeline, no further stages can be provided.

### Transaction Required

The `insert()` stage requires a transaction. It must be run within an active read-write transaction, or with the `atomic` (Node.js) or `auto_commit` option set to true when starting a new transaction.

### Already Exists

The `insert()` stage will fail with an `ALREADY_EXISTS` error if any document to be inserted already exists in the destination.

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
