# Understanding your billing report

This page gives tips and resources to help you understand your Firestore billing report. This page covers the following common sources of billing questions:

  - Outside of app usage, sources of costs include import operations, export operations, and console usage.
  - Within your app, real-time updates, no-op writes, and query offsets can make your usage rise faster than expected.
  - As you use the usage dashboard in the console, note the discrepancies between the dashboard and the billing report.

## Import and Export Usage

When breaking down your billing report, make sure to review costs related to [import and export operations](/firestore/docs/manage-data/export-import) . These operations perform read and write operations which count towards your Firestore billing. Depending on how often you import and export data, these operations can make up a significant source of billed operations.

Note that the usage dashboard in the console does not reflect reads and writes from import and export operations. You can view import/export operations and related costs in the following ways:

### Billing Labels

Export and import operations apply the `  goog-firestoremanaged:exportimport  ` label to their read and write operations. In the Cloud Billing reports page, you can use this label to view costs related to import and export operations:

### List recent operations

You can view recent import and export operations using the console or `  gcloud  ` .

### Console

You can view a list of recent export and import operations in the **Firestore Import/Export** page of the Google Cloud console.

### gcloud

Use the [`  operations list  `](/sdk/gcloud/reference/firestore/operations/list) command to see all running and recently completed export and import operations:

``` text
gcloud firestore operations list
```

### Audit Logs for admin operations

Firestore writes audit logs for export operations, import operations, and indexing operations, see [Firestore audit logging information](/firestore/docs/audit-logging) .

## Console usage

Read operations performed by the Firestore data viewer in the Firebase Console and Cloud console count towards your billed Firestore usage. When you open or refresh the Firestore page, the console loads documents to populate the page. As long as the Firestore page remains open, the console uses real-time queries to update visible documents and collections.

As you breakdown your usage, factor in console usage as another source of Firestore operations. In your billing report, there is no way to distinguish console traffic from application traffic.

## Billed operations

In addition to the [pricing information](https://cloud.google.com/firestore/pricing) , review your app for the following operations which can lead to billing rising faster than expected:

  - **Real-time updates**
    
    When you [listen to the results of a query](/firestore/docs/query-data/listen) , you are charged for a read each time a document in the result set is added or updated. You are also charged for a read when a document is removed from the result set because the document has changed. (In contrast, when a document is deleted, you are not charged for a read.)
    
    Review the scope of your real-time listeners. Listening to the results of a very broad query or listening to an entire collection might result in more read operations than required.

  - **No-op writes and no-op deletes**
    
    A no-op is an operation that does not result in changes to any documents. You still incur charges for no-op writes and deletes.
    
    For a delete operation, you incur charges even if the given document doesn't exist.
    
    For a write operation, you still incur charges if the operations result in no changes. For example, an operation that updates a document field to the same field value incurs charges.

  - **Query offsets**
    
    [Query offsets](https://googleapis.dev/nodejs/firestore/latest/Query.html#offset) skip a specified number of query results but skipped results still count towards billing. Because of this additional cost, you should use [cursors](/firestore/docs/query-data/query-cursors) instead of offsets.

## Usage dashboard discrepancies

The Firestore usage dashboards in the Firebase and Cloud consoles provide an estimate of usage. They can help you identify spikes in usage. However, the dashboard is not an exact view of billed operations. Billed usage is likely higher. In all cases of discrepancy, the billing report takes precedence over the usage dashboard.

Operations that cause discrepancies between the usage dashboard and billed usage include:

  - Import and export operations. Reads and writes performed by these operations do not show up in the usage dashboard.

  - No-op verify-only writes. Writes that only verify the existence or non-existence of a document contribute to billed read operations, but they show as \`UPDATE\_NOOP\` and \`DELETE\_NOOP\` respectively in the write usage dashboard.

  - No-op writes. Operations that do not result in a change to the database, such as an update that does not change field values or a write to a deleted document may show in the usage dashboard as \`UPDATE\_NOOP\` or \`DELETE\_NOOP\`. Even though they show as \`NOOP\`, they still contribute to billed operations.

  - Collapsed writes. In cases with multiple writes to the same document in quick succession, the usage dashboard might collapse multiple writes together and count them as one. When billing usage, each write is still counted separately.
    
    The usage dashboard also collapses writes for field transforms like server timestamps, numeric increments, and array union operations. For field transforms, the usage dashboard might count multiple operations as a single operation.

  - Queries that return zero results. Queries with zero results incur a cost of one read operation. This usage is billed but does not appear in the usage dashboard.

  - Read operations from [index entries read](/firestore/pricing#index-reads) . This usage is billed but does not appear in the usage dashboard. For example, aggregation queries bill for index entries read but this usage does not appear in the usage dashboard.

## What's next

For more help with your billing report, contact [Cloud Billing Support](/support/billing) .
