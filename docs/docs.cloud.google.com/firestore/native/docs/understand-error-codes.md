# Understand error codes

This page lists error codes that you might encounter and provides suggestions for how to fix each of them.

### DEADLINE\_EXCEEDED

The following can increase `  DEADLINE_EXCEEDED  ` errors:

  - An increase in latency caused an operation take longer than the deadline (60 seconds by default) to complete.

<!-- end list -->

``` text
DEADLINE_EXCEEDED

A deadline was exceeded on the server.
```

To resolve this issue, see the [guide to troubleshooting latency](/firestore/docs/resolve-latency) .

### ABORTED

The following situations can increase `  ABORTED  ` errors:

  - A document receiving too many updates per second.
  - Contention from overlapping transactions.
  - Traffic increases that exceed the 500-50-5 rule or encounter hot-spots.

<!-- end list -->

``` text
ABORTED

Too much contention on these datastore entities. Please try again.
```

Or

``` text
ABORTED

Aborted due to cross-transaction contention. This occurs when multiple
transactions attempt to access the same data, requiring Firestore to abort at
least one in order to enforce serializability.
```

To resolve this issue:

  - For rapid traffic increases, Firestore attempts to automatically scale to meet the increased demand. When Firestore scales, latency begins to decrease.
  - Hot-spots limit the ability of Firestore to scale up, review [designing for scale](./best-practices#designing_for_scale) to identify hot-spots.
  - Review [data contention in transactions](./transaction-data-contention) and your usage of transactions.
  - Reduce the write rate to individual documents.

### RESOURCE\_EXHAUSTED

The following situations can lead to `  RESOURCE_EXHAUSTED  ` errors:

  - You exceeded the [free tier quota](https://cloud.google.com/firestore/quotas#free-quota) and billing is not enabled for your project.

  - Traffic increases not following best practices

<!-- end list -->

``` text
RESOURCE_EXHAUSTED

Some resource has been exhausted, perhaps a per-user quota.
```

Or

``` text
RESOURCE_EXHAUSTED

This database has exceeded their daily quota or the ramp up limit for writes, please retry with exponential backoff. To learn more about limits, see 'Usage and limits' section of the support documentation.
```

To resolve this issue:

  - If you are at your free tier quota, wait for the daily reset of your free tier quota or [enable billing for your project](/billing/docs/how-to/modify-project#enable_billing_for_a_project) .

  - For rapid traffic increases, Firestore attempts to automatically scale to meet the increased demand. When Firestore scales errors might decrease.

  - Hot-spots limit the ability of Firestore to scale up. Review [designing for scale](./best-practices#designing_for_scale) to identify hot-spots.

  - For real-time listener queries, make sure the queries are not unnecessarily broad. Use filters to reduce the number of updates.

### INVALID\_ARGUMENT

The following situations can cause `  INVALID_ARGUMENT  ` errors:

  - Attempting to commit a document with an **indexed** field value greater than 1,500 bytes. This limits applies to the UTF-8 encoding of the field value.
  - Attempting to commit a document with **un-indexed** field values greater than 1,048,487 bytes (1 MiB - 89 bytes). This limit applies to the sum of the field values in a document. For example, four fields of 256 KiB each exceed the limit.

1,500 bytes (indexed) and 1,048,487 bytes (un-indexed) are [limits](/datastore/docs/concepts/limits) for field values. You cannot exceed these limits and they are not quotas that can be adjusted.

``` text
INVALID_ARGUMENT: The value of property field-name is longer than 1500 bytes
```

or

``` text
INVALID_ARGUMENT: The value of property field_name is longer than 1048487 bytes
```

To resolve this issue:

  - For indexed field values, split the field into multiple fields. If possible, create an un-indexed field and move data that doesn't need to be indexed into the un-indexed field.
  - For un-indexed field values, split the field into multiple fields or implement compression for the field value.
