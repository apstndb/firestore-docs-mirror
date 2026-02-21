# Process data in bulk with Dataflow

This page gives examples of how to use [Dataflow](https://cloud.google.com/dataflow) to perform bulk Firestore operations in an Apache Beam [pipeline](https://cloud.google.com/dataflow/docs/concepts/beam-programming-model#concepts) . Apache Beam supports a connector for Firestore. You can use this connector to run batch and streaming operations in Dataflow.

We recommend using Dataflow and Apache Beam for large scale data processing workloads.

The Firestore connector for Apache Beam is available in Java. For more information about the Firestore connector, see the [Apache Beam SDK for Java](https://beam.apache.org/releases/javadoc/current/org/apache/beam/sdk/io/gcp/firestore/FirestoreV1.html) .

## Before you begin

Before you read this page, you should be familiar with the [Programming model for Apache Beam](https://cloud.google.com/dataflow/docs/concepts/beam-programming-model) .

To run the samples, you must enable the Dataflow API:

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Example Firestore pipelines

The examples below demonstrate a pipeline that writes data and one that reads and filters data. You can use these samples as a starting point for your own pipelines.

### Running the sample pipelines

The source code for the samples is available in the [*googleapis/java-firestore* GitHub repository](https://github.com/googleapis/java-firestore/tree/main/samples/snippets/src/main/java/com/example/firestore/beam) . To run these samples, download the source code and see the [README](https://github.com/googleapis/java-firestore/tree/main/samples/snippets/src/main/java/com/example/firestore/beam#readme) .

### Example `     Write    ` pipeline

The following example creates documents in the `  cities-beam-sample  ` collection:

``` java
public class ExampleFirestoreBeamWrite {
  private static final FirestoreOptions FIRESTORE_OPTIONS = FirestoreOptions.getDefaultInstance();

  public static void main(String[] args) {
    runWrite(args, "cities-beam-sample");
  }

  public static void runWrite(String[] args, String collectionId) {
    // create pipeline options from the passed in arguments
    PipelineOptions options =
        PipelineOptionsFactory.fromArgs(args).withValidation().as(PipelineOptions.class);
    Pipeline pipeline = Pipeline.create(options);

    RpcQosOptions rpcQosOptions =
        RpcQosOptions.newBuilder()
            .withHintMaxNumWorkers(options.as(DataflowPipelineOptions.class).getMaxNumWorkers())
            .build();

    // create some writes
    Write write1 =
        Write.newBuilder()
            .setUpdate(
                Document.newBuilder()
                    // resolves to
                    // projects/<projectId>/databases/<databaseId>/documents/<collectionId>/NYC
                    .setName(createDocumentName(collectionId, "NYC"))
                    .putFields("name", Value.newBuilder().setStringValue("New York City").build())
                    .putFields("state", Value.newBuilder().setStringValue("New York").build())
                    .putFields("country", Value.newBuilder().setStringValue("USA").build()))
            .build();

    Write write2 =
        Write.newBuilder()
            .setUpdate(
                Document.newBuilder()
                    // resolves to
                    // projects/<projectId>/databases/<databaseId>/documents/<collectionId>/TOK
                    .setName(createDocumentName(collectionId, "TOK"))
                    .putFields("name", Value.newBuilder().setStringValue("Tokyo").build())
                    .putFields("country", Value.newBuilder().setStringValue("Japan").build())
                    .putFields("capital", Value.newBuilder().setBooleanValue(true).build()))
            .build();

    // batch write the data
    pipeline
        .apply(Create.of(write1, write2))
        .apply(FirestoreIO.v1().write().batchWrite().withRpcQosOptions(rpcQosOptions).build());

    // run the pipeline
    pipeline.run().waitUntilFinish();
  }

  private static String createDocumentName(String collectionId, String cityDocId) {
    String documentPath =
        String.format(
            "projects/%s/databases/%s/documents",
            FIRESTORE_OPTIONS.getProjectId(), FIRESTORE_OPTIONS.getDatabaseId());

    return documentPath + "/" + collectionId + "/" + cityDocId;
  }
}ExampleFirestoreBeamWrite.java
```

The example uses the following arguments to configure and run a pipeline:

``` text
GOOGLE_CLOUD_PROJECT=project-id
REGION=region
TEMP_LOCATION=gs://temp-bucket/temp/
NUM_WORKERS=number-workers
MAX_NUM_WORKERS=max-number-workers
```

### Example `     Read    ` Pipeline

The following example pipeline reads documents from the `  cities-beam-sample  ` collection, applies a filter for documents where field `  country  ` is set to `  USA  ` , and returns the names of the matching documents.

``` java
public class ExampleFirestoreBeamRead {

  public static void main(String[] args) {
    runRead(args, "cities-beam-sample");
  }

  public static void runRead(String[] args, String collectionId) {
    FirestoreOptions firestoreOptions = FirestoreOptions.getDefaultInstance();

    PipelineOptions options =
        PipelineOptionsFactory.fromArgs(args).withValidation().as(PipelineOptions.class);
    Pipeline pipeline = Pipeline.create(options);

    RpcQosOptions rpcQosOptions =
        RpcQosOptions.newBuilder()
            .withHintMaxNumWorkers(options.as(DataflowPipelineOptions.class).getMaxNumWorkers())
            .build();

    pipeline
        .apply(Create.of(collectionId))
        .apply(
            new FilterDocumentsQuery(
                firestoreOptions.getProjectId(), firestoreOptions.getDatabaseId()))
        .apply(FirestoreIO.v1().read().runQuery().withRpcQosOptions(rpcQosOptions).build())
        .apply(
            ParDo.of(
                // transform each document to its name
                new DoFn<RunQueryResponse, String>() {
                  @ProcessElement
                  public void processElement(ProcessContext c) {
                    c.output(Objects.requireNonNull(c.element()).getDocument().getName());
                  }
                }))
        .apply(
            ParDo.of(
                // print the document name
                new DoFn<String, Void>() {
                  @ProcessElement
                  public void processElement(ProcessContext c) {
                    System.out.println(c.element());
                  }
                }));

    pipeline.run().waitUntilFinish();
  }

  private static final class FilterDocumentsQuery
      extends PTransform<PCollection<String>, PCollection<RunQueryRequest>> {

    private final String projectId;
    private final String databaseId;

    public FilterDocumentsQuery(String projectId, String databaseId) {
      this.projectId = projectId;
      this.databaseId = databaseId;
    }

    @Override
    public PCollection<RunQueryRequest> expand(PCollection<String> input) {
      return input.apply(
          ParDo.of(
              new DoFn<String, RunQueryRequest>() {
                @ProcessElement
                public void processElement(ProcessContext c) {
                  // select from collection "cities-collection-<uuid>"
                  StructuredQuery.CollectionSelector collection =
                      StructuredQuery.CollectionSelector.newBuilder()
                          .setCollectionId(Objects.requireNonNull(c.element()))
                          .build();
                  // filter where country is equal to USA
                  StructuredQuery.Filter countryFilter =
                      StructuredQuery.Filter.newBuilder()
                          .setFieldFilter(
                              StructuredQuery.FieldFilter.newBuilder()
                                  .setField(
                                      StructuredQuery.FieldReference.newBuilder()
                                          .setFieldPath("country")
                                          .build())
                                  .setValue(Value.newBuilder().setStringValue("USA").build())
                                  .setOp(StructuredQuery.FieldFilter.Operator.EQUAL))
                          .buildPartial();

                  RunQueryRequest runQueryRequest =
                      RunQueryRequest.newBuilder()
                          .setParent(DocumentRootName.format(projectId, databaseId))
                          .setStructuredQuery(
                              StructuredQuery.newBuilder()
                                  .addFrom(collection)
                                  .setWhere(countryFilter)
                                  .build())
                          .build();
                  c.output(runQueryRequest);
                }
              }));
    }
  }
}ExampleFirestoreBeamRead.java
```

The example uses the following arguments to configure and run a pipeline:

``` text
GOOGLE_CLOUD_PROJECT=project-id
REGION=region
TEMP_LOCATION=gs://temp-bucket/temp/
NUM_WORKERS=number-workers
MAX_NUM_WORKERS=max-number-workers
```

## Pricing

Running a Firestore workload in Dataflow incurs costs for Firestore usage and Dataflow usage. Dataflow usage is billed for resources that your jobs use. See the [Dataflow pricing page](https://cloud.google.com/dataflow/pricing) for details. For Firestore pricing, see the [Pricing page](/firestore/pricing) .

## What's next

  - See [Using Firestore and Apache Beam for data processing](https://cloud.google.com/blog/topics/developers-practitioners/using-firestore-and-apache-beam-data-processing) for another pipeline example.
  - For more about Dataflow and Apache Beam, see the [Dataflow documentation](https://cloud.google.com/dataflow#documentation) .
