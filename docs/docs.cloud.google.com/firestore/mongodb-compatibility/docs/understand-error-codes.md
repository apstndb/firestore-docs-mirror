# Understand error codes

This page lists error codes that you might encounter and provides suggestions for how to fix each of them.

### DeadlineExceeded (262)

The following can increase `  DeadlineExceeded (262)  ` errors:

  - An increase in latency caused an operation to take longer than the deadline (60 seconds by default) to complete.

<!-- end list -->

``` text
DeadlineExceeded (262): Deadline exceeded.
```

To resolve this issue, see the [guide to troubleshooting latency](/firestore/mongodb-compatibility/docs/resolve-latency) .

### Aborted (112)

The following situations can increase `  Aborted (112)  ` errors:

  - A document receiving too many updates per second.
  - Contention from overlapping transactions.
  - Traffic that increases rapidly or encounters hot-spots.

<!-- end list -->

``` text
Aborted (112): Too much contention on these documents. Please try again
```

Or

``` text
Aborted (112): Aborted due to cross-transaction contention. This occurs when
multiple transactions attempt to access the same data, requiring at least one
to be aborted in order to enforce serializability.
```

To resolve this issue:

  - For rapid traffic increases, Firestore with MongoDB compatibility attempts to automatically scale to meet the increased demand. When Firestore with MongoDB compatibility scales, latency begins to decrease.
  - Hot-spots limit the ability of Firestore with MongoDB compatibility to scale up. Review [designing for scale](/firestore/mongodb-compatibility/docs/understand-reads-writes-scale#avoid_hotspots) to identify hot-spots.
  - Review [data contention in transactions](/firestore/mongodb-compatibility/docs/understand-reads-writes-scale#high-level_steps_in_a_write_transaction) and your usage of transactions.
  - Reduce the write rate to individual documents.

### InvalidArgument (2)

The following situations can cause `  InvalidArgument (2)  ` errors:

  - Attempting to commit a document with that exceeds the 7.5 KiB limit for an index entry.

7.5 KiB is a [limit](/firestore/mongodb-compatibility/quotas) for index entries. You cannot exceed this limit and it's not a quota that can be adjusted.

``` text
InvalidArgument (2): Index entry on field_name is larger than 7680 bytes.
```

To resolve this issue:

For indexed field values, split the field into multiple fields. If possible, create an un-indexed field and move data that doesn't need to be indexed into the un-indexed field.
