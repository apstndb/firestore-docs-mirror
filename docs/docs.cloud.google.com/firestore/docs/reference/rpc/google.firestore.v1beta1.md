---
name: documents/docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1
uri: https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1
title: Package google.firestore.v1beta1
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Index

- [`Firestore`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore) (interface)
- [`AggregationResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.AggregationResult) (message)
- [`ArrayValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ArrayValue) (message)
- [`BatchGetDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchGetDocumentsRequest) (message)
- [`BatchGetDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchGetDocumentsResponse) (message)
- [`BatchWriteRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchWriteRequest) (message)
- [`BatchWriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchWriteResponse) (message)
- [`BeginTransactionRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BeginTransactionRequest) (message)
- [`BeginTransactionResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BeginTransactionResponse) (message)
- [`BitSequence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BitSequence) (message)
- [`BloomFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BloomFilter) (message)
- [`CommitRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CommitRequest) (message)
- [`CommitResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CommitResponse) (message)
- [`CreateDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CreateDocumentRequest) (message)
- [`Cursor`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Cursor) (message)
- [`DeleteDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DeleteDocumentRequest) (message)
- [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) (message)
- [`DocumentChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentChange) (message)
- [`DocumentDelete`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentDelete) (message)
- [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) (message)
- [`DocumentRemove`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentRemove) (message)
- [`DocumentTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform) (message)
- [`DocumentTransform.FieldTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform) (message)
- [`DocumentTransform.FieldTransform.ServerValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform.ServerValue) (enum)
- [`ExecutePipelineRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutePipelineRequest) (message)
- [`ExecutePipelineResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutePipelineResponse) (message)
- [`ExecutionStats`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutionStats) (message)
- [`ExistenceFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExistenceFilter) (message)
- [`ExplainMetrics`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainMetrics) (message)
- [`ExplainOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainOptions) (message)
- [`ExplainStats`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainStats) (message)
- [`Function`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Function) (message)
- [`GetDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.GetDocumentRequest) (message)
- [`ListCollectionIdsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListCollectionIdsRequest) (message)
- [`ListCollectionIdsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListCollectionIdsResponse) (message)
- [`ListDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListDocumentsRequest) (message)
- [`ListDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListDocumentsResponse) (message)
- [`ListenRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListenRequest) (message)
- [`ListenResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListenResponse) (message)
- [`MapValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.MapValue) (message)
- [`PartitionQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PartitionQueryRequest) (message)
- [`PartitionQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PartitionQueryResponse) (message)
- [`Pipeline`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Pipeline) (message)
- [`Pipeline.Stage`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Pipeline.Stage) (message)
- [`PlanSummary`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PlanSummary) (message)
- [`Precondition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Precondition) (message)
- [`RollbackRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RollbackRequest) (message)
- [`RunAggregationQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunAggregationQueryRequest) (message)
- [`RunAggregationQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunAggregationQueryResponse) (message)
- [`RunQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryRequest) (message)
- [`RunQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryResponse) (message)
- [`StructuredAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery) (message)
- [`StructuredAggregationQuery.Aggregation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation) (message)
- [`StructuredAggregationQuery.Aggregation.Avg`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Avg) (message)
- [`StructuredAggregationQuery.Aggregation.Count`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Count) (message)
- [`StructuredAggregationQuery.Aggregation.Sum`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Sum) (message)
- [`StructuredPipeline`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredPipeline) (message)
- [`StructuredQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery) (message)
- [`StructuredQuery.CollectionSelector`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CollectionSelector) (message)
- [`StructuredQuery.CompositeFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CompositeFilter) (message)
- [`StructuredQuery.CompositeFilter.Operator`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CompositeFilter.Operator) (enum)
- [`StructuredQuery.Direction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Direction) (enum)
- [`StructuredQuery.FieldFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldFilter) (message)
- [`StructuredQuery.FieldFilter.Operator`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldFilter.Operator) (enum)
- [`StructuredQuery.FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) (message)
- [`StructuredQuery.Filter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Filter) (message)
- [`StructuredQuery.FindNearest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FindNearest) (message)
- [`StructuredQuery.FindNearest.DistanceMeasure`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FindNearest.DistanceMeasure) (enum)
- [`StructuredQuery.Order`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Order) (message)
- [`StructuredQuery.Projection`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Projection) (message)
- [`StructuredQuery.UnaryFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.UnaryFilter) (message)
- [`StructuredQuery.UnaryFilter.Operator`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.UnaryFilter.Operator) (enum)
- [`Target`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target) (message)
- [`Target.DocumentsTarget`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target.DocumentsTarget) (message)
- [`Target.QueryTarget`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target.QueryTarget) (message)
- [`TargetChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TargetChange) (message)
- [`TargetChange.TargetChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TargetChange.TargetChangeType) (enum)
- [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) (message)
- [`TransactionOptions.ReadOnly`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions.ReadOnly) (message)
- [`TransactionOptions.ReadWrite`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions.ReadWrite) (message)
- [`UpdateDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.UpdateDocumentRequest) (message)
- [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) (message)
- [`Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) (message)
- [`WriteRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteRequest) (message)
- [`WriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResponse) (message)
- [`WriteResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResult) (message)

## Firestore

The Cloud Firestore service.

Cloud Firestore is a fast, fully managed, serverless, cloud-native NoSQL document database that simplifies storing, syncing, and querying data for your mobile, web, and IoT apps at global scale. Its client libraries provide live synchronization and offline support, while its security features and integrations with Firebase and Google Cloud Platform accelerate building truly serverless apps.

**BatchGetDocuments**

`rpc BatchGetDocuments( `[`BatchGetDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchGetDocumentsRequest)` ) returns ( `[`BatchGetDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchGetDocumentsResponse)` )`

Gets multiple documents.

Documents returned by this method are not guaranteed to be returned in the same order that they were requested.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**BatchWrite**

`rpc BatchWrite( `[`BatchWriteRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchWriteRequest)` ) returns ( `[`BatchWriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchWriteResponse)` )`

Applies a batch of write operations.

The BatchWrite method does not apply the write operations atomically and can apply them out of order. Method does not allow more than one write per document. Each write succeeds or fails independently. See the [`BatchWriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchWriteResponse) for the success status of each write.

If you require an atomically applied set of writes, use [`Commit`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Commit) instead.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**BeginTransaction**

`rpc BeginTransaction( `[`BeginTransactionRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BeginTransactionRequest)` ) returns ( `[`BeginTransactionResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BeginTransactionResponse)` )`

Starts a new transaction.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Commit**

`rpc Commit( `[`CommitRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CommitRequest)` ) returns ( `[`CommitResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CommitResponse)` )`

Commits a transaction, while optionally updating documents.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateDocument**

`rpc CreateDocument( `[`CreateDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.CreateDocumentRequest)` ) returns ( `[`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document)` )`

Creates a new document.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteDocument**

`rpc DeleteDocument( `[`DeleteDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DeleteDocumentRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a document.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ExecutePipeline**

`rpc ExecutePipeline( `[`ExecutePipelineRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutePipelineRequest)` ) returns ( `[`ExecutePipelineResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutePipelineResponse)` )`

Executes a pipeline query.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetDocument**

`rpc GetDocument( `[`GetDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.GetDocumentRequest)` ) returns ( `[`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document)` )`

Gets a single document.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListCollectionIds**

`rpc ListCollectionIds( `[`ListCollectionIdsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListCollectionIdsRequest)` ) returns ( `[`ListCollectionIdsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListCollectionIdsResponse)` )`

Lists all the collection IDs underneath a document.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListDocuments**

`rpc ListDocuments( `[`ListDocumentsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListDocumentsRequest)` ) returns ( `[`ListDocumentsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListDocumentsResponse)` )`

Lists documents.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Listen**

`rpc Listen( `[`ListenRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListenRequest)` ) returns ( `[`ListenResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListenResponse)` )`

Listens to changes. This method is only available via gRPC or WebChannel (not REST).

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**PartitionQuery**

`rpc PartitionQuery( `[`PartitionQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PartitionQueryRequest)` ) returns ( `[`PartitionQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PartitionQueryResponse)` )`

Partitions a query by returning partition cursors that can be used to run the query in parallel. The returned partition cursors are split points that can be used by RunQuery as starting/end points for the query results.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Rollback**

`rpc Rollback( `[`RollbackRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RollbackRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Rolls back a transaction.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RunAggregationQuery**

`rpc RunAggregationQuery( `[`RunAggregationQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunAggregationQueryRequest)` ) returns ( `[`RunAggregationQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunAggregationQueryResponse)` )`

Runs an aggregation query.

Rather than producing [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) results like [`Firestore.RunQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.RunQuery) , this API allows running an aggregation to produce a series of [`AggregationResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.AggregationResult) server-side.

High-Level Example:

```
-- Return the number of documents in table given a filter.
SELECT COUNT(*) FROM ( SELECT * FROM k where a = true );
```

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RunQuery**

`rpc RunQuery( `[`RunQueryRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryRequest)` ) returns ( `[`RunQueryResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryResponse)` )`

Runs a query.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateDocument**

`rpc UpdateDocument( `[`UpdateDocumentRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.UpdateDocumentRequest)` ) returns ( `[`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document)` )`

Updates or inserts a document.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**Write**

`rpc Write( `[`WriteRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteRequest)` ) returns ( `[`WriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResponse)` )`

Streams batches of document updates and deletes, in order. This method is only available via gRPC or WebChannel (not REST).

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## AggregationResult

The result of a single bucket from a Firestore aggregation query.

The keys of `aggregate_fields` are the same for all results in an aggregation query, unlike document queries which can have different fields present for each result.

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregate_fields` | `map<string, `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value)` >` The result of the aggregation functions, ex: `COUNT(*) AS total_docs` . The key is the [`alias`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.FIELDS.string.google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.alias) assigned to the aggregation function on input and the size of this map equals the number of aggregation functions in the query. |

## ArrayValue

An array value.

| Fields     |                                                                                                                                                    |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) Values in the array. |

## BatchGetDocumentsRequest

The request for [`Firestore.BatchGetDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BatchGetDocuments) .

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`                                                                                                                                                                           | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` .                                                                                                                                                                                                                      |
| `documents[]`                                                                                                                                                                        | `string` The names of the documents to retrieve. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` . The request will fail if any of the document is not a child resource of the given `database` . Duplicate names will be elided.                                                  |
| `mask`                                                                                                                                                                               | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to return. If not set, returns all fields. If a document has a field that is not present in this mask, that field will not be returned in the response.              |
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                             |
| `transaction`                                                                                                                                                                        | `bytes` Reads documents in a transaction.                                                                                                                                                                                                                                                                                   |
| `new_transaction`                                                                                                                                                                    | [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) Starts a new transaction and reads the documents. Defaults to a read-only transaction. The new transaction ID will be returned as the first response in the stream. |
| `read_time`                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads documents as they were at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.    |

## BatchGetDocumentsResponse

The streamed response for [`Firestore.BatchGetDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BatchGetDocuments) .

| Fields                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction`                                                                                                                                       | `bytes` The transaction that was started as part of this request. Will only be set in the first response, and only if [`BatchGetDocumentsRequest.new_transaction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BatchGetDocumentsRequest.FIELDS.google.firestore.v1beta1.TransactionOptions.google.firestore.v1beta1.BatchGetDocumentsRequest.new_transaction) was set in the request. |
| `read_time`                                                                                                                                         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the document was read. This may be monotically increasing, in this case the previous documents in the result stream are guaranteed not to have changed between their read_time and this one.                                                                                                                                                       |
| Union field `result` . A single result. This can be empty if the server is just returning a transaction. `result` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `found`                                                                                                                                             | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) A document that was requested.                                                                                                                                                                                                                                                                                     |
| `missing`                                                                                                                                           | `string` A document name that was requested but does not exist. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` .                                                                                                                                                                                                                                                                                             |

## BatchWriteRequest

The request for [`Firestore.BatchWrite`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BatchWrite) .

| Fields     |                                                                                                                                                                                                                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database` | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` .                                                                                                                                                                                                                                    |
| `writes[]` | [`Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) The writes to apply. Method does not apply writes atomically and does not guarantee ordering. Each write succeeds or fails independently. You cannot write to the same document more than once per request. |
| `labels`   | `map<string, string>` Labels associated with this batch write.                                                                                                                                                                                                                                                                            |

## BatchWriteResponse

The response from [`Firestore.BatchWrite`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BatchWrite) .

| Fields            |                                                                                                                                                                                                                                                   |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `write_results[]` | [`WriteResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResult) The result of applying the writes. This i-th write result corresponds to the i-th write in the request. |
| `status[]`        | [`Status`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.rpc#google.rpc.Status) The status of applying the writes. This i-th write status corresponds to the i-th write in the request.                                       |

## BeginTransactionRequest

The request for [`Firestore.BeginTransaction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BeginTransaction) .

| Fields     |                                                                                                                                                                                                                                |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database` | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` .                                                                                                                         |
| `options`  | [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) The options for the transaction. Defaults to a read-write transaction. |

## BeginTransactionResponse

The response for [`Firestore.BeginTransaction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.BeginTransaction) .

| Fields        |                                           |
|---------------|-------------------------------------------|
| `transaction` | `bytes` The transaction that was started. |

## BitSequence

A sequence of bits, encoded in a byte array.

Each byte in the `bitmap` byte array stores 8 bits of the sequence. The only exception is the last byte, which may store 8 *or fewer* bits. The `padding` defines the number of bits of the last byte to be ignored as "padding". The values of these "padding" bits are unspecified and must be ignored.

To retrieve the first bit, bit 0, calculate: `(bitmap[0] & 0x01) != 0` . To retrieve the second bit, bit 1, calculate: `(bitmap[0] & 0x02) != 0` . To retrieve the third bit, bit 2, calculate: `(bitmap[0] & 0x04) != 0` . To retrieve the fourth bit, bit 3, calculate: `(bitmap[0] & 0x08) != 0` . To retrieve bit n, calculate: `(bitmap[n / 8] & (0x01 << (n % 8))) != 0` .

The "size" of a `BitSequence` (the number of bits it contains) is calculated by this formula: `(bitmap.length * 8) - padding` .

| Fields    |                                                                                                                                                                                                            |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `bitmap`  | `bytes` The bytes that encode the bit sequence. May have a length of zero.                                                                                                                                 |
| `padding` | `int32` The number of bits of the last byte in `bitmap` to ignore as "padding". If the length of `bitmap` is zero, then this value must be `0` . Otherwise, this value must be between 0 and 7, inclusive. |

## BloomFilter

A bloom filter ( <https://en.wikipedia.org/wiki/Bloom_filter)> .

The bloom filter hashes the entries with MD5 and treats the resulting 128-bit hash as 2 distinct 64-bit hash values, interpreted as unsigned integers using 2's complement encoding.

These two hash values, named `h1` and `h2` , are then used to compute the `hash_count` hash values using the formula, starting at `i=0` :

```
h(i) = h1 + (i * h2)
```

These resulting values are then taken modulo the number of bits in the bloom filter to get the bits of the bloom filter to test for the given entry.

| Fields       |                                                                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `bits`       | [`BitSequence`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BitSequence) The bloom filter data. |
| `hash_count` | `int32` The number of hashes used by the algorithm.                                                                                                              |

## CommitRequest

The request for [`Firestore.Commit`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Commit) .

| Fields        |                                                                                                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`    | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` .                                                                                      |
| `writes[]`    | [`Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) The writes to apply. Always executed atomically and in order. |
| `transaction` | `bytes` If set, applies all writes in this transaction, and commits it.                                                                                                                     |

## CommitResponse

The response for [`Firestore.Commit`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Commit) .

| Fields            |                                                                                                                                                                                                                                                   |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `write_results[]` | [`WriteResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResult) The result of applying the writes. This i-th write result corresponds to the i-th write in the request. |
| `commit_time`     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the commit occurred. Any read with an equal or greater `read_time` is guaranteed to see the effects of the commit.                            |

## CreateDocumentRequest

The request for [`Firestore.CreateDocument`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.CreateDocument) .

| Fields          |                                                                                                                                                                                                                                                                                                                  |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`        | `string` Required. The parent resource. For example: `projects/{project_id}/databases/{database_id}/documents` or `projects/{project_id}/databases/{database_id}/documents/chatrooms/{chatroom_id}`                                                                                                              |
| `collection_id` | `string` Required. The collection ID, relative to `parent` , to list. For example: `chatrooms` .                                                                                                                                                                                                                 |
| `document_id`   | `string` The client-assigned document ID to use for this document. Optional. If not specified, an ID will be assigned by the service.                                                                                                                                                                            |
| `document`      | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) Required. The document to create. `name` must not be set.                                                                                                                    |
| `mask`          | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to return. If not set, returns all fields. If the document has a field that is not present in this mask, that field will not be returned in the response. |

## Cursor

A position in a query result set.

| Fields     |                                                                                                                                                                                                                                                                                                 |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) The values that represent a position, in the order they appear in the order by clause of a query. Can contain fewer values than specified in the order by clause. |
| `before`   | `bool` If the position is just before or just after the given values, relative to the sort order defined by the query.                                                                                                                                                                          |

## DeleteDocumentRequest

The request for [`Firestore.DeleteDocument`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.DeleteDocument) .

| Fields             |                                                                                                                                                                                                                                                                |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Required. The resource name of the Document to delete. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` .                                                                                                     |
| `current_document` | [`Precondition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Precondition) An optional precondition on the document. The request will fail if this is set and not met by the target document. |

## Document

A Firestore document.

Must not exceed 1 MiB - 4 bytes.

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`        | `string` The resource name of the document, for example `projects/{project_id}/databases/{database_id}/documents/{document_path}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `fields`      | `map<string, `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value)` >` The document's fields. The map keys represent field names. Field names matching the regular expression `__.*__` are reserved. Reserved field names are forbidden except in certain documented contexts. The field names, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty. Field paths may be used in other contexts to refer to structured fields defined here. For `map_value` , the field path is represented by a dot-delimited ( `.` ) string of segments. Each segment is either a simple field name (defined below) or a quoted field name. For example, the structured field `"foo" : { map_value: { "x&y" : { string_value: "hello" }}}` would be represented by the field path `` foo.`x&y` `` . A simple field name contains only characters `a` to `z` , `A` to `Z` , `0` to `9` , or `_` , and must not start with `0` to `9` . For example, `foo_bar_17` . A quoted field name starts and ends with `` ` `` and may contain any character. Some characters, including `` ` `` , must be escaped using a `\` . For example, `` `x&y` `` represents `x&y` and `` `bak\`tik` `` represents `` bak`tik `` . |
| `create_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time at which the document was created. This value increases monotonically when a document is deleted then recreated. It can also be compared to values from other documents and the `read_time` of a query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `update_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time at which the document was last changed. This value is initially set to the `create_time` then increases monotonically with each change to the document. It can also be compared to values from other documents and the `read_time` of a query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## DocumentChange

A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has changed.

May be the result of multiple [`writes`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) , including deletes, that ultimately resulted in a new value for the [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) .

Multiple [`DocumentChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentChange) messages may be returned for the same logical change, if multiple targets are affected.

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`             | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) The new state of the [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) . If `mask` is set, contains only fields that were updated or added. |
| `target_ids[]`         | `int32` A set of target IDs of targets that match this document.                                                                                                                                                                                                                                                                                                  |
| `removed_target_ids[]` | `int32` A set of target IDs for targets that no longer match this document.                                                                                                                                                                                                                                                                                       |

## DocumentDelete

A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has been deleted.

May be the result of multiple [`writes`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) , including updates, the last of which deleted the [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) .

Multiple [`DocumentDelete`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentDelete) messages may be returned for the same logical delete, if multiple targets are affected.

| Fields                 |                                                                                                                                                                                             |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`             | `string` The resource name of the [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) that was deleted.     |
| `removed_target_ids[]` | `int32` A set of target IDs for targets that previously matched this entity.                                                                                                                |
| `read_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The read timestamp at which the delete was observed. Greater or equal to the `commit_time` of the delete. |

## DocumentMask

A set of field paths on a document. Used to restrict a get or update operation on a document to a subset of its fields. This is different from standard field masks, as this is always scoped to a [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) , and takes in account the dynamic nature of [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) .

| Fields          |                                                                                                                                                                                                                                                                                                                                        |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field_paths[]` | `string` The list of field paths in the mask. See [`Document.fields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.repeated.google.firestore.v1beta1.Document.FieldsEntry.google.firestore.v1beta1.Document.fields) for a field path syntax reference. |

## DocumentRemove

A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has been removed from the view of the targets.

Sent if the document is no longer relevant to a target and is out of view. Can be sent instead of a DocumentDelete or a DocumentChange if the server can not send the new value of the document.

Multiple [`DocumentRemove`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentRemove) messages may be returned for the same logical write or delete, if multiple targets are affected.

| Fields                 |                                                                                                                                                                                                           |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`             | `string` The resource name of the [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) that has gone out of view.          |
| `removed_target_ids[]` | `int32` A set of target IDs for targets that previously matched this document.                                                                                                                            |
| `read_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The read timestamp at which the remove was observed. Greater or equal to the `commit_time` of the change/delete/remove. |

## DocumentTransform

A transformation of a document.

| Fields               |                                                                                                                                                                                                                                                                         |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`           | `string` The name of the document to transform.                                                                                                                                                                                                                         |
| `field_transforms[]` | [`FieldTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform) The list of transformations to apply to the fields of the document, in order. This must not be empty. |

## FieldTransform

A transformation of a field of the document.

| Fields                                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field_path`                                                                                                                | `string` The path of the field. See [`Document.fields`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.repeated.google.firestore.v1beta1.Document.FieldsEntry.google.firestore.v1beta1.Document.fields) for the field path syntax reference.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Union field `transform_type` . The transformation to apply on the field. `transform_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `set_to_server_value`                                                                                                       | [`ServerValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform.ServerValue) Sets the field to the given server value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `increment`                                                                                                                 | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) Adds the given value to the field's current value. This must be an integer or a double value. If the field is not an integer or double, or if the field does not yet exist, the transformation will set the field to the given value. If either of the given value or the current field value are doubles, both values will be interpreted as doubles. Double arithmetic and representation of double values follow IEEE 754 semantics. If there is positive/negative integer overflow, the field is resolved to the largest magnitude positive/negative integer.                                                                                                                                           |
| `maximum`                                                                                                                   | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) Sets the field to the maximum of its current value and the given value. This must be an integer or a double value. If the field is not an integer or double, or if the field does not yet exist, the transformation will set the field to the given value. If a maximum operation is applied where the field and the input value are of mixed types (that is - one is an integer and one is a double) the field takes on the type of the larger operand. If the operands are equivalent (e.g. 3 and 3.0), the field does not change. 0, 0.0, and -0.0 are all zero. The maximum of a zero stored value and zero input value is always the stored value. The maximum of any numeric value x and NaN is NaN.  |
| `minimum`                                                                                                                   | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) Sets the field to the minimum of its current value and the given value. This must be an integer or a double value. If the field is not an integer or double, or if the field does not yet exist, the transformation will set the field to the input value. If a minimum operation is applied where the field and the input value are of mixed types (that is - one is an integer and one is a double) the field takes on the type of the smaller operand. If the operands are equivalent (e.g. 3 and 3.0), the field does not change. 0, 0.0, and -0.0 are all zero. The minimum of a zero stored value and zero input value is always the stored value. The minimum of any numeric value x and NaN is NaN. |
| `append_missing_elements`                                                                                                   | [`ArrayValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ArrayValue) Append the given elements in order if they are not already present in the current field value. If the field is not an array, or if the field does not yet exist, it is first set to the empty array. Equivalent numbers of different types (e.g. 3L and 3.0) are considered equal when checking if a value is missing. NaN is equal to NaN, and Null is equal to Null. If the input contains multiple equivalent values, only the first will be considered. The corresponding transform_result will be the null value.                                                                                                                                                                            |
| `remove_all_from_array`                                                                                                     | [`ArrayValue`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ArrayValue) Remove all of the given elements from the array in the field. If the field is not an array, or if the field does not yet exist, it is set to the empty array. Equivalent numbers of the different types (e.g. 3L and 3.0) are considered equal when deciding whether an element should be removed. NaN is equal to NaN, and Null is equal to Null. This will remove all equivalent values if there are duplicates. The corresponding transform_result will be the null value.                                                                                                                                                                                                                     |

## ServerValue

A value that is calculated by the server.

| Enums                      |                                                                                                                                                                                                               |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SERVER_VALUE_UNSPECIFIED` | Unspecified. This value must not be used.                                                                                                                                                                     |
| `REQUEST_TIME`             | The time at which the server processed the request, with millisecond precision. If used on multiple fields (same or different documents) in a transaction, all the fields will get the same server timestamp. |

## ExecutePipelineRequest

The request for [`Firestore.ExecutePipeline`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.ExecutePipeline) .

| Fields                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`                                                                                                                                                    | `string` Required. Database identifier, in the form `projects/{project}/databases/{database}` .                                                                                                                                                                                                                                                    |
| Union field `pipeline_type` . `pipeline_type` can be only one of the following:                                                                               |                                                                                                                                                                                                                                                                                                                                                    |
| `structured_pipeline`                                                                                                                                         | [`StructuredPipeline`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredPipeline) A pipelined operation.                                                                                                                                                                     |
| Union field `consistency_selector` . Optional consistency arguments, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                    |
| `transaction`                                                                                                                                                 | `bytes` Run the query within an already active transaction. The value here is the opaque transaction ID to execute the query in.                                                                                                                                                                                                                   |
| `new_transaction`                                                                                                                                             | [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) Execute the pipeline in a new transaction. The identifier of the newly created transaction will be returned in the first response on the stream. This defaults to a read-only transaction. |
| `read_time`                                                                                                                                                   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Execute the pipeline in a snapshot transaction at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.         |

## ExecutePipelineResponse

The response for \[Firestore.Execute\]\[\].

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction`    | `bytes` Newly created transaction identifier. This field is only specified as part of the first response from the server, alongside the `results` field when the original request specified \[ExecuteRequest.new_transaction\]\[\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `results[]`      | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) An ordered batch of results returned executing a pipeline. The batch size is variable, and can even be zero for when only a partial progress message is returned. The fields present in the returned documents are only those that were explicitly requested in the pipeline, this includes those like [`__name__`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.string.google.firestore.v1beta1.Document.name) and [`__update_time__`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.google.protobuf.Timestamp.google.firestore.v1beta1.Document.update_time) . This is explicitly a divergence from `Firestore.RunQuery` / `Firestore.GetDocument` RPCs which always return such fields even when they are not specified in the [`mask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) . |
| `execution_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the results are valid. This is a (not strictly) monotonically increasing value across multiple responses in the same stream. The API guarantees that all previously returned results are still valid at the latest `execution_time` . This allows the API consumer to treat the query if it ran at the latest `execution_time` returned. If the query returns no results, a response with `execution_time` and no `results` will be sent, and this represents the time at which the operation was run.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `explain_stats`  | [`ExplainStats`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainStats) Query explain stats. This is present on the **last** response if the request configured explain to run in 'analyze' or 'explain' mode in the pipeline options. If the query does not return any results, a response with `explain_stats` and no `results` will still be sent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## ExecutionStats

Execution statistics for the query.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results_returned`   | `int64` Total number of results returned, including documents, projections, aggregation results, keys.                                                                                                                                                                                                                                                                                                      |
| `execution_duration` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Total time to execute the query in the backend.                                                                                                                                                                                                                                                                             |
| `read_operations`    | `int64` Total billable read operations.                                                                                                                                                                                                                                                                                                                                                                     |
| `debug_stats`        | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Debugging statistics from the execution of the query. Note that the debugging stats are subject to change as Firestore evolves. It could include: { "indexes_entries_scanned": "1000", "documents_scanned": "20", "billing_details" : { "documents_billable": "20", "index_entries_billable": "1000", "min_query_cost": "0" } } |

## ExistenceFilter

A digest of all the documents that match a given target.

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `target_id`       | `int32` The target ID to which this filter applies.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `count`           | `int32` The total count of documents that match [`target_id`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExistenceFilter.FIELDS.int32.google.firestore.v1beta1.ExistenceFilter.target_id) . If different from the count of documents in the client that match, the client must manually determine which documents no longer match the target. The client can use the `unchanged_names` bloom filter to assist with this determination by testing ALL the document names against the filter; if the document name is NOT in the filter, it means the document no longer matches the target.                                                                                                                                                                                                                                                                                                                                                               |
| `unchanged_names` | [`BloomFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.BloomFilter) A bloom filter that, despite its name, contains the UTF-8 byte encodings of the resource names of ALL the documents that match [`target_id`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExistenceFilter.FIELDS.int32.google.firestore.v1beta1.ExistenceFilter.target_id) , in the form `projects/{project_id}/databases/{database_id}/documents/{document_path}` . This bloom filter may be omitted at the server's discretion, such as if it is deemed that the client will not make use of it or if it is too computationally expensive to calculate or transmit. Clients must gracefully handle this field being absent by falling back to the logic used before this field existed; that is, re-add the target without a resume token to figure out which documents in the client's cache are out of sync. |

## ExplainMetrics

Explain metrics for the query.

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `plan_summary`    | [`PlanSummary`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.PlanSummary) Planning phase information for the query.                                                                                                                                                                                                                                                                     |
| `execution_stats` | [`ExecutionStats`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExecutionStats) Aggregated stats from the execution of the query. Only present when [`ExplainOptions.analyze`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainOptions.FIELDS.bool.google.firestore.v1beta1.ExplainOptions.analyze) is set to true. |

## ExplainOptions

Explain options for the query.

| Fields    |                                                                                                                                                                                                                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `analyze` | `bool` Optional. Whether to execute this query. When false (the default), the query will be planned, returning only metrics from the planning stages. When true, the query will be planned and executed, returning the full query results along with both planning and execution stage metrics. |

## ExplainStats

Pipeline explain stats.

Depending on the explain options in the original request, this can contain the optimized plan and / or execution stats.

| Fields |                                                                                                                                                                                                                                                      |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `data` | [`Any`](https://protobuf.dev/reference/protobuf/google.protobuf/#any) The format depends on the `output_format` options in the request. Currently there are two supported options: `TEXT` and `JSON` . Both supply a `google.protobuf.StringValue` . |

## Function

Represents an unevaluated scalar expression.

For example, the expression `like(user_name, "%alice%")` is represented as:

```
name: "like"
args { field_reference: "user_name" }
args { string_value: "%alice%" }
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the function to evaluate.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>must be in snake case (lower case with underscore separator).</li>
</ul></td>
</tr>
<tr class="even">
<td><code>args[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value"><code>Value</code></a></p>
<p>Optional. Ordered list of arguments the given function expects.</p></td>
</tr>
<tr class="odd">
<td><code>options</code></td>
<td><p><code>map&lt;string, </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value"><code>Value</code></a><code> &gt;</code></p>
<p>Optional. Optional named arguments that certain functions may support.</p></td>
</tr>
</tbody>
</table>

## GetDocumentRequest

The request for [`Firestore.GetDocument`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.GetDocument) .

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                               | `string` Required. The resource name of the Document to get. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` .                                                                                                                                                                       |
| `mask`                                                                                                                                                                               | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to return. If not set, returns all fields. If the document has a field that is not present in this mask, that field will not be returned in the response.              |
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                               |
| `transaction`                                                                                                                                                                        | `bytes` Reads the document in a transaction.                                                                                                                                                                                                                                                                                  |
| `read_time`                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads the version of the document at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. |

## ListCollectionIdsRequest

The request for [`Firestore.ListCollectionIds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.ListCollectionIds) .

| Fields                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                          |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                                                                                                         | `string` Required. The parent document. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` . For example: `projects/my-project/databases/my-database/documents/chatrooms/my-chatroom` Use `projects/{project_id}/databases/{database_id}/documents` to list top-level collections. |
| `page_size`                                                                                                                                                                      | `int32` The maximum number of results to return.                                                                                                                                                                                                                                                                         |
| `page_token`                                                                                                                                                                     | `string` A page token. Must be a value from [`ListCollectionIdsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ListCollectionIdsResponse) .                                                                                                      |
| Union field `consistency_selector` . The consistency mode for this request. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                          |
| `read_time`                                                                                                                                                                      | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads documents as they were at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. |

## ListCollectionIdsResponse

The response from [`Firestore.ListCollectionIds`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.ListCollectionIds) .

| Fields             |                                                              |
|--------------------|--------------------------------------------------------------|
| `collection_ids[]` | `string` The collection ids.                                 |
| `next_page_token`  | `string` A page token that may be used to continue the list. |

## ListDocumentsRequest

The request for [`Firestore.ListDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.ListDocuments) .

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                                                                                                             | `string` Required. The parent resource name. In the format: `projects/{project_id}/databases/{database_id}/documents` or `projects/{project_id}/databases/{database_id}/documents/{document_path}` . For example: `projects/my-project/databases/my-database/documents` or `projects/my-project/databases/my-database/documents/chatrooms/my-chatroom`                                                                                                                                                                                                                                                                                                                                                                                                             |
| `collection_id`                                                                                                                                                                      | `string` Optional. The collection ID, relative to `parent` , to list. For example: `chatrooms` or `messages` . This is optional, and when not provided, Firestore will list documents from all collections under the provided `parent` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `page_size`                                                                                                                                                                          | `int32` Optional. The maximum number of documents to return in a single response. Firestore may return fewer than this value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `page_token`                                                                                                                                                                         | `string` Optional. A page token, received from a previous `ListDocuments` response. Provide this to retrieve the subsequent page. When paginating, all other parameters (with the exception of `page_size` ) must match the values set in the request that generated the page token.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `order_by`                                                                                                                                                                           | `string` Optional. The optional ordering of the documents to return. For example: `priority desc, __name__ desc` . This mirrors the [`ORDER BY`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FIELDS.repeated.google.firestore.v1beta1.StructuredQuery.Order.google.firestore.v1beta1.StructuredQuery.order_by) used in Firestore queries but in a string representation. When absent, documents are ordered based on `__name__ ASC` .                                                                                                                                                                                                                                             |
| `mask`                                                                                                                                                                               | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) Optional. The fields to return. If not set, returns all fields. If a document has a field that is not present in this mask, that field will not be returned in the response.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `show_missing`                                                                                                                                                                       | `bool` If the list should show missing documents. A document is missing if it does not exist, but there are sub-documents nested underneath it. When true, such missing documents will be returned with a key but will not have fields, [`create_time`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.google.protobuf.Timestamp.google.firestore.v1beta1.Document.create_time) , or [`update_time`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.google.protobuf.Timestamp.google.firestore.v1beta1.Document.update_time) set. Requests with `show_missing` may not specify `where` or `order_by` . |
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `transaction`                                                                                                                                                                        | `bytes` Perform the read as part of an already active transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `read_time`                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Perform the read at the provided time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## ListDocumentsResponse

The response for [`Firestore.ListDocuments`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.ListDocuments) .

| Fields            |                                                                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]`     | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) The Documents found. |
| `next_page_token` | `string` A token to retrieve the next page of documents. If this field is omitted, there are no subsequent pages.                                        |

## ListenRequest

A request for [`Firestore.Listen`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Listen)

| Fields                                                                                                        |                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`                                                                                                    | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` .                                                          |
| `labels`                                                                                                      | `map<string, string>` Labels associated with this target change.                                                                                                |
| Union field `target_change` . The supported target changes. `target_change` can be only one of the following: |                                                                                                                                                                 |
| `add_target`                                                                                                  | [`Target`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target) A target to add to this stream. |
| `remove_target`                                                                                               | `int32` The ID of a target to remove from this stream.                                                                                                          |

## ListenResponse

The response for [`Firestore.Listen`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Listen) .

| Fields                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `response_type` . The supported responses. `response_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                         |
| `target_change`                                                                                          | [`TargetChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TargetChange) Targets have changed.                                                                                                                                                                                                       |
| `document_change`                                                                                        | [`DocumentChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentChange) A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has changed.                                                                      |
| `document_delete`                                                                                        | [`DocumentDelete`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentDelete) A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has been deleted.                                                                 |
| `document_remove`                                                                                        | [`DocumentRemove`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentRemove) A [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) has been removed from a target (because it is no longer relevant to that target). |
| `filter`                                                                                                 | [`ExistenceFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExistenceFilter) A filter to apply to the set of documents previously returned for the given target. Returned when documents may have been removed from the given target, but the exact documents are unknown.                         |

## MapValue

A map value.

| Fields   |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map<string, `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value)` >` The map's fields. The map keys represent field names. Field names matching the regular expression `__.*__` are reserved. Reserved field names are forbidden except in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty. |

## PartitionQueryRequest

The request for [`Firestore.PartitionQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.PartitionQuery) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The parent resource name. In the format: <code>projects/{project_id}/databases/{database_id}/documents</code> . Document resource names are not supported; only database resource names can be specified.</p></td>
</tr>
<tr class="even">
<td><code>partition_count</code></td>
<td><p><code>int64</code></p>
<p>The desired maximum number of partition points. The partitions may be returned across multiple pages of results. The number must be positive. The actual number of partitions returned may be fewer.</p>
<p>For example, this may be set to one fewer than the number of parallel queries to be run, or in running a data pipeline job, one fewer than the number of workers or compute instances available.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The <code>next_page_token</code> value returned from a previous call to PartitionQuery that may be used to get an additional set of results. There are no ordering guarantees between sets of results. Thus, using multiple sets of results will require merging the different result sets.</p>
<p>For example, two subsequent calls using a page_token may return:</p>
<ul>
<li>cursor B, cursor M, cursor Q</li>
<li>cursor A, cursor U, cursor W</li>
</ul>
<p>To obtain a complete result set ordered with respect to the results of the query supplied to PartitionQuery, the results sets should be merged: cursor A, cursor B, cursor M, cursor Q, cursor U, cursor W</p></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of partitions to return in this call, subject to <code>partition_count</code> .</p>
<p>For example, if <code>partition_count</code> = 10 and <code>page_size</code> = 8, the first call to PartitionQuery will return up to 8 partitions and a <code>next_page_token</code> if more results exist. A second call to PartitionQuery will return up to 2 partitions, to complete the total of 10 specified in <code>partition_count</code> .</p></td>
</tr>
<tr class="odd">
<td>Union field <code>query_type</code> . The query to partition. <code>query_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>structured_query</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery"><code>StructuredQuery</code></a></p>
<p>A structured query. Query must specify collection with all descendants and be ordered by name ascending. Other filters, order bys, limits, offsets, and start/end cursors are not supported.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>consistency_selector</code> . The consistency mode for this request. If not set, defaults to strong consistency. <code>consistency_selector</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>read_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Reads documents as they were at the given time.</p>
<p>This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.</p></td>
</tr>
</tbody>
</table>

## PartitionQueryResponse

The response for [`Firestore.PartitionQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.PartitionQuery) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>partitions[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Cursor"><code>Cursor</code></a></p>
<p>Partition results. Each partition is a split point that can be used by RunQuery as a starting or end point for the query results. The RunQuery requests must be made with the same query supplied to this PartitionQuery request. The partition cursors will be ordered according to same ordering as the results of the query supplied to PartitionQuery.</p>
<p>For example, if a PartitionQuery request returns partition cursors A and B, running the following three queries will return the entire result set of the original query:</p>
<ul>
<li>query, end_at A</li>
<li>query, start_at A, end_at B</li>
<li>query, start_at B</li>
</ul>
<p>An empty result may indicate that the query has too few results to be partitioned, or that the query is not yet supported for partitioning.</p></td>
</tr>
<tr class="even">
<td><code>next_page_token</code></td>
<td><p><code>string</code></p>
<p>A page token that may be used to request an additional set of results, up to the number specified by <code>partition_count</code> in the PartitionQuery request. If blank, there are no more results.</p></td>
</tr>
</tbody>
</table>

## Pipeline

A Firestore query represented as an ordered list of operations / stages.

| Fields     |                                                                                                                                                                                      |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stages[]` | [`Stage`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Pipeline.Stage) Required. Ordered list of stages to evaluate. |

## Stage

A single operation within a pipeline.

A stage is made up of a unique name, and a list of arguments. The exact number of arguments & types is dependent on the stage type.

To give an example, the stage `filter(state = "MD")` would be encoded as:

```
name: "filter"
args {
  function_value {
    name: "eq"
    args { field_reference_value: "state" }
    args { string_value: "MD" }
  }
}
```

See public documentation for the full list.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the stage to evaluate.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>must be in snake case (lower case with underscore separator).</li>
</ul></td>
</tr>
<tr class="even">
<td><code>args[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value"><code>Value</code></a></p>
<p>Optional. Ordered list of arguments the given stage expects.</p></td>
</tr>
<tr class="odd">
<td><code>options</code></td>
<td><p><code>map&lt;string, </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value"><code>Value</code></a><code> &gt;</code></p>
<p>Optional. Optional named arguments that certain functions may support.</p></td>
</tr>
</tbody>
</table>

## PlanSummary

Planning phase information for the query.

| Fields           |                                                                                                                                                                                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexes_used[]` | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) The indexes selected for the query. For example: \[ {"query_scope": "Collection", "properties": "(foo ASC, **name** ASC)"}, {"query_scope": "Collection", "properties": "(bar ASC, **name** ASC)"} \] |

## Precondition

A precondition on a document, used for conditional operations.

| Fields                                                                                                      |                                                                                                                                                                                                            |
|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `condition_type` . The type of precondition. `condition_type` can be only one of the following: |                                                                                                                                                                                                            |
| `exists`                                                                                                    | `bool` When set to `true` , the target document must exist. When set to `false` , the target document must not exist.                                                                                      |
| `update_time`                                                                                               | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) When set, the target document must exist and have been last updated at that time. Timestamp must be microsecond aligned. |

## RollbackRequest

The request for [`Firestore.Rollback`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Rollback) .

| Fields        |                                                                                                        |
|---------------|--------------------------------------------------------------------------------------------------------|
| `database`    | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` . |
| `transaction` | `bytes` Required. The transaction to roll back.                                                        |

## RunAggregationQueryRequest

The request for [`Firestore.RunAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.RunAggregationQuery) .

| Fields                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                                                                                          | `string` Required. The parent resource name. In the format: `projects/{project_id}/databases/{database_id}/documents` or `projects/{project_id}/databases/{database_id}/documents/{document_path}` . For example: `projects/my-project/databases/my-database/documents` or `projects/my-project/databases/my-database/documents/chatrooms/my-chatroom` |
| `explain_options`                                                                                                                                                 | [`ExplainOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainOptions) Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.                                                            |
| Union field `query_type` . The query to run. `query_type` can be only one of the following:                                                                       |                                                                                                                                                                                                                                                                                                                                                        |
| `structured_aggregation_query`                                                                                                                                    | [`StructuredAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery) An aggregation query.                                                                                                                                                          |
| Union field `consistency_selector` . The consistency mode for the query, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                        |
| `transaction`                                                                                                                                                     | `bytes` Run the aggregation within an already active transaction. The value here is the opaque transaction ID to execute the query in.                                                                                                                                                                                                                 |
| `new_transaction`                                                                                                                                                 | [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) Starts a new transaction as part of the query, defaulting to read-only. The new transaction ID will be returned as the first response in the stream.                                           |
| `read_time`                                                                                                                                                       | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Executes the query at the given timestamp. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.                                    |

## RunAggregationQueryResponse

The response for [`Firestore.RunAggregationQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.RunAggregationQuery) .

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result`          | [`AggregationResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.AggregationResult) A single aggregation result. Not present when reporting partial progress.                                                                                                                                                                                                                                                                                                                                                             |
| `transaction`     | `bytes` The transaction that was started as part of this request. Only present on the first response when the request requested to start a new transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `read_time`       | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the aggregate result was computed. This is always monotonically increasing; in this case, the previous AggregationResult in the result stream are guaranteed not to have changed between their `read_time` and this one. If the query returns no results, a response with `read_time` and no `result` will be sent, and this represents the time at which the query was run.                                                                                                            |
| `explain_metrics` | [`ExplainMetrics`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainMetrics) Query explain metrics. This is only present when the [`RunAggregationQueryRequest.explain_options`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunAggregationQueryRequest.FIELDS.google.firestore.v1beta1.ExplainOptions.google.firestore.v1beta1.RunAggregationQueryRequest.explain_options) is provided, and it is sent only once with the last response in the stream. |

## RunQueryRequest

The request for [`Firestore.RunQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.RunQuery) .

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                                                                                                             | `string` Required. The parent resource name. In the format: `projects/{project_id}/databases/{database_id}/documents` or `projects/{project_id}/databases/{database_id}/documents/{document_path}` . For example: `projects/my-project/databases/my-database/documents` or `projects/my-project/databases/my-database/documents/chatrooms/my-chatroom` |
| `explain_options`                                                                                                                                                                    | [`ExplainOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainOptions) Optional. Explain options for the query. If set, additional query statistics will be returned. If not, only query results will be returned.                                                            |
| Union field `query_type` . The query to run. `query_type` can be only one of the following:                                                                                          |                                                                                                                                                                                                                                                                                                                                                        |
| `structured_query`                                                                                                                                                                   | [`StructuredQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery) A structured query.                                                                                                                                                                                  |
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                        |
| `transaction`                                                                                                                                                                        | `bytes` Run the query within an already active transaction. The value here is the opaque transaction ID to execute the query in.                                                                                                                                                                                                                       |
| `new_transaction`                                                                                                                                                                    | [`TransactionOptions`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions) Starts a new transaction and reads the documents. Defaults to a read-only transaction. The new transaction ID will be returned as the first response in the stream.                            |
| `read_time`                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads documents as they were at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.                               |

## RunQueryResponse

The response for [`Firestore.RunQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.RunQuery) .

| Fields                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `transaction`                                                                                                                                                                                                                                                                                                   | `bytes` The transaction that was started as part of this request. Can only be set in the first response, and only if [`RunQueryRequest.new_transaction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryRequest.FIELDS.google.firestore.v1beta1.TransactionOptions.google.firestore.v1beta1.RunQueryRequest.new_transaction) was set in the request. If set, no other fields will be set in this response.                                                                           |
| `document`                                                                                                                                                                                                                                                                                                      | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) A query result, not set when reporting partial progress.                                                                                                                                                                                                                                                                                                                                                               |
| `read_time`                                                                                                                                                                                                                                                                                                     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the document was read. This may be monotonically increasing; in this case, the previous documents in the result stream are guaranteed not to have changed between their `read_time` and this one. If the query returns no results, a response with `read_time` and no `document` will be sent, and this represents the time at which the query was run.                                                                                                |
| `skipped_results`                                                                                                                                                                                                                                                                                               | `int32` The number of results that have been skipped due to an offset between the last response and the current response.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `explain_metrics`                                                                                                                                                                                                                                                                                               | [`ExplainMetrics`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ExplainMetrics) Query explain metrics. This is only present when the [`RunQueryRequest.explain_options`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.RunQueryRequest.FIELDS.google.firestore.v1beta1.ExplainOptions.google.firestore.v1beta1.RunQueryRequest.explain_options) is provided, and it is sent only once with the last response in the stream. |
| Union field `continuation_selector` . The continuation mode for the query. If present, it indicates the current query response stream has finished. This can be set with or without a `document` present, but when set, no more results are returned. `continuation_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `done`                                                                                                                                                                                                                                                                                                          | `bool` If present, Firestore has completely finished the request and no more documents will be returned.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## StructuredAggregationQuery

Firestore query for running an aggregation over a [`StructuredQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>aggregations[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation"><code>Aggregation</code></a></p>
<p>Optional. Series of aggregations to apply over the results of the <code>structured_query</code> .</p>
<p>Requires:</p>
<ul>
<li>A minimum of one and maximum of five aggregations per query.</li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>query_type</code> . The base query to aggregate over. <code>query_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>structured_query</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery"><code>StructuredQuery</code></a></p>
<p>Nested structured query.</p></td>
</tr>
</tbody>
</table>

## Aggregation

Defines an aggregation that produces a single result.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>alias</code></td>
<td><p><code>string</code></p>
<p>Optional. Optional name of the field to store the result of the aggregation into.</p>
<p>If not provided, Firestore will pick a default name following the format <code>field_&lt;incremental_id++&gt;</code> . For example:</p>
<pre data-fenced=""><code>AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2),
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*)
OVER (
  ...
);</code></pre>
<p>becomes:</p>
<pre data-fenced=""><code>AGGREGATE
  COUNT_UP_TO(1) AS count_up_to_1,
  COUNT_UP_TO(2) AS field_1,
  COUNT_UP_TO(3) AS count_up_to_3,
  COUNT(*) AS field_2
OVER (
  ...
);</code></pre>
<p>Requires:</p>
<ul>
<li>Must be unique across all aggregation aliases.</li>
<li>Conform to <a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.repeated.google.firestore.v1beta1.Document.FieldsEntry.google.firestore.v1beta1.Document.fields"><code>document field name</code></a> limitations.</li>
</ul></td>
</tr>
<tr class="even">
<td>Union field <code>operator</code> . The type of aggregation to perform, required. <code>operator</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>count</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Count"><code>Count</code></a></p>
<p>Count aggregator.</p></td>
</tr>
<tr class="even">
<td><code>sum</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Sum"><code>Sum</code></a></p>
<p>Sum aggregator.</p></td>
</tr>
<tr class="odd">
<td><code>avg</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredAggregationQuery.Aggregation.Avg"><code>Avg</code></a></p>
<p>Average aggregator.</p></td>
</tr>
</tbody>
</table>

## Avg

Average of the values of the requested field.

- Only numeric values will be aggregated. All non-numeric values including `NULL` are skipped.

- If the aggregated values contain `NaN` , returns `NaN` . Infinity math follows IEEE-754 standards.

- If the aggregated value set is empty, returns `NULL` .

- Always returns the result as a double.

| Fields  |                                                                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The field to aggregate on. |

## Count

Count of documents that match the query.

The `COUNT(*)` aggregation function operates on the entire document so it does not require a field reference.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>up_to</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int64-value"><code>Int64Value</code></a></p>
<p>Optional. Optional constraint on the maximum number of documents to count.</p>
<p>This provides a way to set an upper bound on the number of documents to scan, limiting latency, and cost.</p>
<p>Unspecified is interpreted as no bound.</p>
<p>High-Level Example:</p>
<pre data-fenced=""><code>AGGREGATE COUNT_UP_TO(1000) OVER ( SELECT * FROM k );</code></pre>
<p>Requires:</p>
<ul>
<li>Must be greater than zero when present.</li>
</ul></td>
</tr>
</tbody>
</table>

## Sum

Sum of the values of the requested field.

- Only numeric values will be aggregated. All non-numeric values including `NULL` are skipped.

- If the aggregated values contain `NaN` , returns `NaN` . Infinity math follows IEEE-754 standards.

- If the aggregated value set is empty, returns 0.

- Returns a 64-bit integer if all aggregated numbers are integers and the sum result does not overflow. Otherwise, the result is returned as a double. Note that even if all the aggregated values are integers, the result is returned as a double if it cannot fit within a 64-bit signed integer. When this occurs, the returned value will lose precision.

- When underflow occurs, floating-point aggregation is non-deterministic. This means that running the same query repeatedly without any changes to the underlying values could produce slightly different results each time. In those cases, values should be stored as integers over floating-point numbers.

| Fields  |                                                                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The field to aggregate on. |

## StructuredPipeline

A Firestore query represented as an ordered list of operations / stages.

This is considered the top-level function which plans and executes a query. It is logically equivalent to `query(stages, options)` , but prevents the client from having to build a function wrapper.

| Fields     |                                                                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pipeline` | [`Pipeline`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Pipeline) Required. The pipeline query to execute.              |
| `options`  | `map<string, `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value)` >` Optional. Optional query-level arguments. |

## StructuredQuery

A Firestore query.

The query stages are executed in the following order: 1. from 2. where 3. select 4. order_by + start_at + end_at 5. offset 6. limit 7. find_nearest

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>select</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Projection"><code>Projection</code></a></p>
<p>Optional sub-set of the fields to return.</p>
<p>This acts as a <a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask"><code>DocumentMask</code></a> over the documents returned from a query. When not set, assumes that the caller wants all fields returned.</p></td>
</tr>
<tr class="even">
<td><code>from[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CollectionSelector"><code>CollectionSelector</code></a></p>
<p>The collections to query.</p></td>
</tr>
<tr class="odd">
<td><code>where</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Filter"><code>Filter</code></a></p>
<p>The filter to apply.</p></td>
</tr>
<tr class="even">
<td><code>order_by[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Order"><code>Order</code></a></p>
<p>The order to apply to the query results.</p>
<p>Callers can provide a full ordering, a partial ordering, or no ordering at all. While Firestore will always respect the provided order, the behavior for queries without a full ordering is different per database edition:</p>
<p>In Standard edition, Firestore guarantees a stable ordering through the following rules:</p>
<ul>
<li>The <code>order_by</code> is required to reference all fields used with an inequality filter.</li>
<li>All fields that are required to be in the <code>order_by</code> but are not already present are appended in lexicographical ordering of the field name.</li>
<li>If an order on <code>__name__</code> is not specified, it is appended by default.</li>
</ul>
<p>Fields are appended with the same sort direction as the last order specified, or 'ASCENDING' if no order was specified. For example:</p>
<ul>
<li><code>ORDER BY a</code> becomes <code>ORDER BY a ASC, __name__ ASC</code></li>
<li><code>ORDER BY a DESC</code> becomes <code>ORDER BY a DESC, __name__ DESC</code></li>
<li><code>WHERE a &gt; 1</code> becomes <code>WHERE a &gt; 1 ORDER BY a ASC, __name__ ASC</code></li>
<li><code>WHERE __name__ &gt; ... AND a &gt; 1</code> becomes <code>WHERE __name__ &gt; ... AND a &gt; 1 ORDER BY a ASC, __name__ ASC</code></li>
</ul>
<p>In Enterprise edition, Firestore does not guarantee a stable ordering. Instead it will pick the most efficient ordering based on the indexes available at the time of query execution. This will result in a different ordering for queries that are otherwise identical. To ensure a stable ordering, always include a unique field in the <code>order_by</code> clause, such as <code>__name__</code> .</p></td>
</tr>
<tr class="odd">
<td><code>start_at</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Cursor"><code>Cursor</code></a></p>
<p>A potential prefix of a position in the result set to start the query at.</p>
<p>The ordering of the result set is based on the <code>ORDER BY</code> clause of the original query.</p>
<pre data-fenced=""><code>SELECT * FROM k WHERE a = 1 AND b &gt; 2 ORDER BY b ASC, __name__ ASC;</code></pre>
<p>This query's results are ordered by <code>(b ASC, __name__ ASC)</code> .</p>
<p>Cursors can reference either the full ordering or a prefix of the location, though it cannot reference more fields than what are in the provided <code>ORDER BY</code> .</p>
<p>Continuing off the example above, attaching the following start cursors will have varying impact:</p>
<ul>
<li><code>START BEFORE (2, /k/123)</code> : start the query right before <code>a = 1 AND b &gt; 2 AND __name__ &gt; /k/123</code> .</li>
<li><code>START AFTER (10)</code> : start the query right after <code>a = 1 AND b &gt; 10</code> .</li>
</ul>
<p>Unlike <code>OFFSET</code> which requires scanning over the first N results to skip, a start cursor allows the query to begin at a logical position. This position is not required to match an actual result, it will scan forward from this position to find the next document.</p>
<p>Requires:</p>
<ul>
<li>The number of values cannot be greater than the number of fields specified in the <code>ORDER BY</code> clause.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>end_at</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Cursor"><code>Cursor</code></a></p>
<p>A potential prefix of a position in the result set to end the query at.</p>
<p>This is similar to <code>START_AT</code> but with it controlling the end position rather than the start position.</p>
<p>Requires:</p>
<ul>
<li>The number of values cannot be greater than the number of fields specified in the <code>ORDER BY</code> clause.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>offset</code></td>
<td><p><code>int32</code></p>
<p>The number of documents to skip before returning the first result.</p>
<p>This applies after the constraints specified by the <code>WHERE</code> , <code>START AT</code> , &amp; <code>END AT</code> but before the <code>LIMIT</code> clause.</p>
<p>Requires:</p>
<ul>
<li>The value must be greater than or equal to zero if specified.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>limit</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int32-value"><code>Int32Value</code></a></p>
<p>The maximum number of results to return.</p>
<p>Applies after all other constraints.</p>
<p>Requires:</p>
<ul>
<li>The value must be greater than or equal to zero if specified.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>find_nearest</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FindNearest"><code>FindNearest</code></a></p>
<p>Optional. A potential nearest neighbors search.</p>
<p>Applies after all other filters and ordering.</p>
<p>Finds the closest vector embeddings to the given query vector.</p></td>
</tr>
</tbody>
</table>

## CollectionSelector

A selection of a collection, such as `messages as m1` .

| Fields            |                                                                                                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `collection_id`   | `string` The collection ID. When set, selects only collections with this ID.                                                                                                           |
| `all_descendants` | `bool` When false, selects only collections that are immediate children of the `parent` specified in the containing `RunQueryRequest` . When true, selects all descendant collections. |

## CompositeFilter

A filter that merges multiple other filters using the given operator.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>op</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CompositeFilter.Operator"><code>Operator</code></a></p>
<p>The operator for combining multiple filters.</p></td>
</tr>
<tr class="even">
<td><code>filters[]</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Filter"><code>Filter</code></a></p>
<p>The list of filters to combine.</p>
<p>Requires:</p>
<ul>
<li>At least one filter is present.</li>
</ul></td>
</tr>
</tbody>
</table>

## Operator

A composite filter operator.

| Enums                  |                                                                         |
|------------------------|-------------------------------------------------------------------------|
| `OPERATOR_UNSPECIFIED` | Unspecified. This value must not be used.                               |
| `AND`                  | Documents are required to satisfy all of the combined filters.          |
| `OR`                   | Documents are required to satisfy at least one of the combined filters. |

## Direction

A sort direction.

| Enums                   |              |
|-------------------------|--------------|
| `DIRECTION_UNSPECIFIED` | Unspecified. |
| `ASCENDING`             | Ascending.   |
| `DESCENDING`            | Descending.  |

## FieldFilter

A filter on a specific field.

| Fields  |                                                                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The field to filter by.    |
| `op`    | [`Operator`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldFilter.Operator) The operator to filter by. |
| `value` | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) The value to compare to.                                     |

## Operator

A field filter operator.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>OPERATOR_UNSPECIFIED</code></td>
<td>Unspecified. This value must not be used.</td>
</tr>
<tr class="even">
<td><code>LESS_THAN</code></td>
<td><p>The given <code>field</code> is less than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>LESS_THAN_OR_EQUAL</code></td>
<td><p>The given <code>field</code> is less than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>GREATER_THAN</code></td>
<td><p>The given <code>field</code> is greater than the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>GREATER_THAN_OR_EQUAL</code></td>
<td><p>The given <code>field</code> is greater than or equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>That <code>field</code> come first in <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>EQUAL</code></td>
<td>The given <code>field</code> is equal to the given <code>value</code> .</td>
</tr>
<tr class="odd">
<td><code>NOT_EQUAL</code></td>
<td><p>The given <code>field</code> is not equal to the given <code>value</code> .</p>
<p>Requires:</p>
<ul>
<li>No other <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>ARRAY_CONTAINS</code></td>
<td>The given <code>field</code> is an array that contains the given <code>value</code> .</td>
</tr>
<tr class="odd">
<td><code>IN</code></td>
<td><p>The given <code>field</code> is equal to at least one value in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> , subject to disjunction limits.</li>
<li>No <code>NOT_IN</code> filters in the same query.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>ARRAY_CONTAINS_ANY</code></td>
<td><p>The given <code>field</code> is an array that contains any of the values in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> , subject to disjunction limits.</li>
<li>No other <code>ARRAY_CONTAINS_ANY</code> filters within the same disjunction.</li>
<li>No <code>NOT_IN</code> filters in the same query.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>NOT_IN</code></td>
<td><p>The value of the <code>field</code> is not in the given array.</p>
<p>Requires:</p>
<ul>
<li>That <code>value</code> is a non-empty <code>ArrayValue</code> with at most 10 values.</li>
<li>No other <code>OR</code> , <code>IN</code> , <code>ARRAY_CONTAINS_ANY</code> , <code>NOT_IN</code> , <code>NOT_EQUAL</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

## FieldReference

A reference to a field in a document, ex: `stats.operations` .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>field_path</code></td>
<td><p><code>string</code></p>
<p>A reference to a field in a document.</p>
<p>Requires:</p>
<ul>
<li>MUST be a dot-delimited ( <code>.</code> ) string of segments, where each segment conforms to <a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.repeated.google.firestore.v1beta1.Document.FieldsEntry.google.firestore.v1beta1.Document.fields"><code>document field name</code></a> limitations.</li>
</ul></td>
</tr>
</tbody>
</table>

## Filter

A filter.

| Fields                                                                                          |                                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `filter_type` . The type of filter. `filter_type` can be only one of the following: |                                                                                                                                                                                                     |
| `composite_filter`                                                                              | [`CompositeFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.CompositeFilter) A composite filter.               |
| `field_filter`                                                                                  | [`FieldFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldFilter) A filter on a document field.             |
| `unary_filter`                                                                                  | [`UnaryFilter`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.UnaryFilter) A filter that takes exactly one argument. |

## FindNearest

Nearest Neighbors search config. The ordering provided by FindNearest supersedes the order_by stage. If multiple documents have the same vector distance, the returned document order is not guaranteed to be stable between queries.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>vector_field</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference"><code>FieldReference</code></a></p>
<p>Required. An indexed vector field to search upon. Only documents which contain vectors whose dimensionality match the query_vector can be returned.</p></td>
</tr>
<tr class="even">
<td><code>query_vector</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value"><code>Value</code></a></p>
<p>Required. The query vector that we are searching on. Must be a vector of no more than 2048 dimensions.</p></td>
</tr>
<tr class="odd">
<td><code>distance_measure</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FindNearest.DistanceMeasure"><code>DistanceMeasure</code></a></p>
<p>Required. The distance measure to use, required.</p></td>
</tr>
<tr class="even">
<td><code>limit</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#int32-value"><code>Int32Value</code></a></p>
<p>Required. The number of nearest neighbors to return. Must be a positive integer of no more than 1000.</p></td>
</tr>
<tr class="odd">
<td><code>distance_result_field</code></td>
<td><p><code>string</code></p>
<p>Optional. Optional name of the field to output the result of the vector distance calculation. Must conform to <a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document.FIELDS.repeated.google.firestore.v1beta1.Document.FieldsEntry.google.firestore.v1beta1.Document.fields"><code>document field name</code></a> limitations.</p></td>
</tr>
<tr class="even">
<td><code>distance_threshold</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#double-value"><code>DoubleValue</code></a></p>
<p>Optional. Option to specify a threshold for which no less similar documents will be returned. The behavior of the specified <code>distance_measure</code> will affect the meaning of the distance threshold. Since DOT_PRODUCT distances increase when the vectors are more similar, the comparison is inverted.</p>
<ul>
<li>For EUCLIDEAN, COSINE: <code>WHERE distance &lt;= distance_threshold</code></li>
<li>For DOT_PRODUCT: <code>WHERE distance &gt;= distance_threshold</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DistanceMeasure

The distance measure to use when comparing vectors.

| Enums                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DISTANCE_MEASURE_UNSPECIFIED` | Should not be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `EUCLIDEAN`                    | Measures the EUCLIDEAN distance between the vectors. See [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance) to learn more. The resulting distance decreases the more similar two vectors are.                                                                                                                                                                                                                                                                                                              |
| `COSINE`                       | COSINE distance compares vectors based on the angle between them, which allows you to measure similarity that isn't based on the vectors magnitude. We recommend using DOT_PRODUCT with unit normalized vectors instead of COSINE distance, which is mathematically equivalent with better performance. See [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity) to learn more about COSINE similarity and COSINE distance. The resulting COSINE distance decreases the more similar two vectors are. |
| `DOT_PRODUCT`                  | Similar to cosine but is affected by the magnitude of the vectors. See [Dot Product](https://en.wikipedia.org/wiki/Dot_product) to learn more. The resulting distance increases the more similar two vectors are.                                                                                                                                                                                                                                                                                                     |

## Order

An order on a field.

| Fields      |                                                                                                                                                                                                            |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field`     | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The field to order by.                     |
| `direction` | [`Direction`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.Direction) The direction to order by. Defaults to `ASCENDING` . |

## Projection

The projection of document's fields to return.

| Fields     |                                                                                                                                                                                                                                                                                        |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The fields to return. If empty, all fields are returned. To only return the name of the document, use `['__name__']` . |

## UnaryFilter

A filter with a single operand.

| Fields                                                                                                    |                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `op`                                                                                                      | [`Operator`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.UnaryFilter.Operator) The unary operator to apply.              |
| Union field `operand_type` . The argument to the filter. `operand_type` can be only one of the following: |                                                                                                                                                                                                           |
| `field`                                                                                                   | [`FieldReference`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery.FieldReference) The field to which to apply the operator. |

## Operator

A unary operator.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>OPERATOR_UNSPECIFIED</code></td>
<td>Unspecified. This value must not be used.</td>
</tr>
<tr class="even">
<td><code>IS_NAN</code></td>
<td>The given <code>field</code> is equal to <code>NaN</code> .</td>
</tr>
<tr class="odd">
<td><code>IS_NULL</code></td>
<td>The given <code>field</code> is equal to <code>NULL</code> .</td>
</tr>
<tr class="even">
<td><code>IS_NOT_NAN</code></td>
<td><p>The given <code>field</code> is not equal to <code>NaN</code> .</p>
<p>Requires:</p>
<ul>
<li>No other <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>IS_NOT_NULL</code></td>
<td><p>The given <code>field</code> is not equal to <code>NULL</code> .</p>
<p>Requires:</p>
<ul>
<li>A single <code>NOT_EQUAL</code> , <code>NOT_IN</code> , <code>IS_NOT_NULL</code> , or <code>IS_NOT_NAN</code> .</li>
<li>That <code>field</code> comes first in the <code>order_by</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

## Target

A specification of a set of documents to listen to.

| Fields                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `target_id`                                                                                                                                                                                                                                                                                                   | `int32` The target ID that identifies the target on the stream. Must be a positive number and non-zero. If `target_id` is 0 (or unspecified), the server will assign an ID for this target and return that in a `TargetChange::ADD` event. Once a target with `target_id=0` is added, all subsequent targets must also have `target_id=0` . If an `AddTarget` request with `target_id != 0` is sent to the server after a target with `target_id=0` is added, the server will immediately send a response with a `TargetChange::Remove` event. Note that if the client sends multiple `AddTarget` requests without an ID, the order of IDs returned in `TargetChange.target_ids` are undefined. Therefore, clients should provide a target ID instead of relying on the server to assign one. If `target_id` is non-zero, there must not be an existing active target on this stream with the same ID. |
| `once`                                                                                                                                                                                                                                                                                                        | `bool` If the target should be removed once it is current and consistent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `expected_count`                                                                                                                                                                                                                                                                                              | [`Int32Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#int32-value) The number of documents that last matched the query at the resume token or read time. This value is only relevant when a `resume_type` is provided. This value being present and greater than zero signals that the client wants `ExistenceFilter.unchanged_names` to be included in the response.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Union field `target_type` . The type of target to listen to. `target_type` can be only one of the following:                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `query`                                                                                                                                                                                                                                                                                                       | [`QueryTarget`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target.QueryTarget) A target specified by a query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `documents`                                                                                                                                                                                                                                                                                                   | [`DocumentsTarget`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Target.DocumentsTarget) A target specified by a set of document names.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Union field `resume_type` . When to start listening. If specified, only the matching Documents that have been updated AFTER the `resume_token` or `read_time` will be returned. Otherwise, all matching Documents are returned before any subsequent changes. `resume_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `resume_token`                                                                                                                                                                                                                                                                                                | `bytes` A resume token from a prior [`TargetChange`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TargetChange) for an identical target. Using a resume token with a different target is unsupported and may fail.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `read_time`                                                                                                                                                                                                                                                                                                   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Start listening after a specific `read_time` . The client must know the state of matching documents at this time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## DocumentsTarget

A target specified by a set of documents names.

| Fields        |                                                                                                                                                                                                                                                                            |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]` | `string` The names of the documents to retrieve. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` . The request will fail if any of the document is not a child resource of the given `database` . Duplicate names will be elided. |

## QueryTarget

A target specified by a query.

| Fields                                                                                      |                                                                                                                                                                                                                                                                                                                                              |
|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                    | `string` The parent resource name. In the format: `projects/{project_id}/databases/{database_id}/documents` or `projects/{project_id}/databases/{database_id}/documents/{document_path}` . For example: `projects/my-project/databases/my-database/documents` or `projects/my-project/databases/my-database/documents/chatrooms/my-chatroom` |
| Union field `query_type` . The query to run. `query_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                              |
| `structured_query`                                                                          | [`StructuredQuery`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.StructuredQuery) A structured query.                                                                                                                                                                        |

## TargetChange

Targets being watched have changed.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `target_change_type` | [`TargetChangeType`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TargetChange.TargetChangeType) The type of change that occurred.                                                                                                                                                                                                                                                                                                                                                                            |
| `target_ids[]`       | `int32` The target IDs of targets that have changed. If empty, the change applies to all targets. The order of the target IDs is not defined.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `cause`              | [`Status`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.rpc#google.rpc.Status) The error that resulted in this change, if applicable.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `resume_token`       | `bytes` A token that can be used to resume the stream for the given `target_ids` , or all targets if `target_ids` is empty. Not set on every target change.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `read_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The consistent `read_time` for the given `target_ids` (omitted when the target_ids are not at a consistent snapshot). The stream is guaranteed to send a `read_time` with `target_ids` empty whenever the entire stream reaches a new consistent snapshot. ADD, CURRENT, and RESET messages are guaranteed to (eventually) result in a new consistent snapshot (while NO_CHANGE and REMOVE messages are not). For a given stream, `read_time` is guaranteed to be monotonically increasing. |

## TargetChangeType

The type of change.

| Enums       |                                                                                                                                                                                                                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `NO_CHANGE` | No change has occurred. Used only to send an updated `resume_token` .                                                                                                                                                                                                                         |
| `ADD`       | The targets have been added.                                                                                                                                                                                                                                                                  |
| `REMOVE`    | The targets have been removed.                                                                                                                                                                                                                                                                |
| `CURRENT`   | The targets reflect all changes committed before the targets were added to the stream. This will be sent after or with a `read_time` that is greater than or equal to the time at which the targets were added. Listeners can wait for this change if read-after-write semantics are desired. |
| `RESET`     | The targets have been reset, and a new initial state for the targets will be returned in subsequent changes. After the initial state is complete, `CURRENT` will be returned even if the target was previously indicated to be `CURRENT` .                                                    |

## TransactionOptions

Options for creating a new transaction.

| Fields                                                                                     |                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `mode` . The mode of the transaction. `mode` can be only one of the following: |                                                                                                                                                                                                                          |
| `read_only`                                                                                | [`ReadOnly`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions.ReadOnly) The transaction can only be used for read operations.             |
| `read_write`                                                                               | [`ReadWrite`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.TransactionOptions.ReadWrite) The transaction can be used for both read and write operations. |

## ReadOnly

Options for a transaction that can only be used to read documents.

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `consistency_selector` . The consistency mode for this transaction. If not set, defaults to strong consistency. `consistency_selector` can be only one of the following: |                                                                                                                                                                                                                                                                                                             |
| `read_time`                                                                                                                                                                          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Reads documents at the given time. This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days. |

## ReadWrite

Options for a transaction that can be used to read and write documents.

Firestore does not allow 3rd party auth requests to create read-write. transactions.

| Fields              |                                           |
|---------------------|-------------------------------------------|
| `retry_transaction` | `bytes` An optional transaction to retry. |

## UpdateDocumentRequest

The request for [`Firestore.UpdateDocument`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.UpdateDocument) .

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`         | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) Required. The updated document. Creates the document if it does not already exist.                                                                                                                                                                                                                                         |
| `update_mask`      | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to update. None of the field paths in the mask may contain a reserved name. If the document exists on the server and has fields not referenced in the mask, they are left unchanged. Fields referenced in the mask, but not present in the input document, are deleted from the document on the server. |
| `mask`             | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to return. If not set, returns all fields. If the document has a field that is not present in this mask, that field will not be returned in the response.                                                                                                                                               |
| `current_document` | [`Precondition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Precondition) An optional precondition on the document. The request will fail if this is set and not met by the target document.                                                                                                                                                                                                 |

## Value

A message that can hold any of the supported value types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Union field <code>value_type</code> . Must have a value set. <code>value_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>null_value</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#null-value"><code>NullValue</code></a></p>
<p>A null value.</p></td>
</tr>
<tr class="odd">
<td><code>boolean_value</code></td>
<td><p><code>bool</code></p>
<p>A boolean value.</p></td>
</tr>
<tr class="even">
<td><code>integer_value</code></td>
<td><p><code>int64</code></p>
<p>An integer value.</p></td>
</tr>
<tr class="odd">
<td><code>double_value</code></td>
<td><p><code>double</code></p>
<p>A double value.</p></td>
</tr>
<tr class="even">
<td><code>timestamp_value</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>A timestamp value.</p>
<p>Precise only to microseconds. When stored, any additional precision is rounded down.</p></td>
</tr>
<tr class="odd">
<td><code>string_value</code></td>
<td><p><code>string</code></p>
<p>A string value.</p>
<p>The string, represented as UTF-8, must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes of the UTF-8 representation are considered by queries.</p></td>
</tr>
<tr class="even">
<td><code>bytes_value</code></td>
<td><p><code>bytes</code></p>
<p>A bytes value.</p>
<p>Must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes are considered by queries.</p></td>
</tr>
<tr class="odd">
<td><code>reference_value</code></td>
<td><p><code>string</code></p>
<p>A reference to a document. For example: <code>projects/{project_id}/databases/{database_id}/documents/{document_path}</code> .</p></td>
</tr>
<tr class="even">
<td><code>geo_point_value</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.type#google.type.LatLng"><code>LatLng</code></a></p>
<p>A geo point value representing a point on the surface of Earth.</p></td>
</tr>
<tr class="odd">
<td><code>array_value</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.ArrayValue"><code>ArrayValue</code></a></p>
<p>An array value.</p>
<p>Cannot directly contain another array value, though can contain a map which contains another array.</p></td>
</tr>
<tr class="even">
<td><code>map_value</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.MapValue"><code>MapValue</code></a></p>
<p>A map value.</p></td>
</tr>
<tr class="odd">
<td><code>field_reference_value</code></td>
<td><p><code>string</code></p>
<p>Value which references a field.</p>
<p>This is considered relative (vs absolute) since it only refers to a field and not a field within a particular document.</p>
<p><strong>Requires:</strong></p>
<ul>
<li><p>Must follow [field reference][FieldReference.field_path] limitations.</p></li>
<li><p>Not allowed to be used when writing documents.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code>variable_reference_value</code></td>
<td><p><code>string</code></p>
<p>Pointer to a variable defined elsewhere in a pipeline.</p>
<p>Unlike <code>field_reference_value</code> which references a field within a document, this refers to a variable, defined in a separate namespace than the fields of a document.</p></td>
</tr>
<tr class="odd">
<td><code>function_value</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Function"><code>Function</code></a></p>
<p>A value that represents an unevaluated expression.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>Not allowed to be used when writing documents.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>pipeline_value</code></td>
<td><p><a href="https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Pipeline"><code>Pipeline</code></a></p>
<p>A value that represents an unevaluated pipeline.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>Not allowed to be used when writing documents.</li>
</ul></td>
</tr>
</tbody>
</table>

## Write

A write on a document.

| Fields                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `update_mask`                                                                                     | [`DocumentMask`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentMask) The fields to update in this write. This field can be set only when the operation is `update` . If the mask is not set for an `update` and the document exists, any existing data will be overwritten. If the mask is set and the document on the server has fields not covered by the mask, they are left unchanged. Fields referenced in the mask, but not present in the input document, are deleted from the document on the server. The field paths in this mask must not contain a reserved field name. |
| `update_transforms[]`                                                                             | [`FieldTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform) The transforms to perform after update. This field can be set only when the operation is `update` . If present, this write is equivalent to performing `update` and `transform` to the same document atomically and in order.                                                                                                                                                                                                                                                           |
| `current_document`                                                                                | [`Precondition`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Precondition) An optional precondition on the document. The write will fail if this is set and not met by the target document.                                                                                                                                                                                                                                                                                                                                                                                              |
| Union field `operation` . The operation to execute. `operation` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `update`                                                                                          | [`Document`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Document) A document to write.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `delete`                                                                                          | `string` A document name to delete. In the format: `projects/{project_id}/databases/{database_id}/documents/{document_path}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `transform`                                                                                       | [`DocumentTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform) Applies a transformation to a document.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

## WriteRequest

The request for [`Firestore.Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Write) .

The first request creates a stream, or resumes an existing one from a token.

When creating a new stream, the server replies with a response containing only an ID and a token, to use in the next request.

When resuming a stream, the server first streams any responses later than the given token, then a response containing only an up-to-date token, to use in the next request.

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`     | `string` Required. The database name. In the format: `projects/{project_id}/databases/{database_id}` . This is only required in the first message.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `stream_id`    | `string` The ID of the write stream to resume. This may only be set in the first message. When left empty, a new write stream will be created.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `writes[]`     | [`Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Write) The writes to apply. Always executed atomically and in order. This must be empty on the first request. This may be empty on the last request. This must not be empty on all other requests.                                                                                                                                                                                                                                                                                                                                                                                             |
| `stream_token` | `bytes` A stream token that was previously sent by the server. The client should set this field to the token from the most recent [`WriteResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResponse) it has received. This acknowledges that the client has received responses up to this token. After sending this token, earlier tokens may not be used anymore. The server may close the stream if there are too many unacknowledged responses. Leave this field unset when creating a new stream. To resume a stream at a specific point, set this field and the `stream_id` field. Leave this field unset when creating a new stream. |
| `labels`       | `map<string, string>` Labels associated with this write request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## WriteResponse

The response for [`Firestore.Write`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Firestore.Write) .

| Fields            |                                                                                                                                                                                                                                                   |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stream_id`       | `string` The ID of the stream. Only set on the first message, when a new stream was created.                                                                                                                                                      |
| `stream_token`    | `bytes` A token that represents the position of this response in the stream. This can be used by a client to resume the stream at this point. This field is always set.                                                                           |
| `write_results[]` | [`WriteResult`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.WriteResult) The result of applying the writes. This i-th write result corresponds to the i-th write in the request. |
| `commit_time`     | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time at which the commit occurred. Any read with an equal or greater `read_time` is guaranteed to see the effects of the write.                             |

## WriteResult

The result of applying a write.

| Fields                |                                                                                                                                                                                                                                                                                                                                                                     |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `update_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The last update time of the document after applying the write. Not set after a `delete` . If the write did not actually change the document, this will be the previous update_time.                                                                                               |
| `transform_results[]` | [`Value`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.Value) The results of applying each [`DocumentTransform.FieldTransform`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.firestore.v1beta1#google.firestore.v1beta1.DocumentTransform.FieldTransform) , in the same order. |
