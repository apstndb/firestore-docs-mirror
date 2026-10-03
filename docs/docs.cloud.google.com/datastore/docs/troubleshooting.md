---
name: documents/docs.cloud.google.com/datastore/docs/troubleshooting
uri: https://docs.cloud.google.com/datastore/docs/troubleshooting
title: Troubleshooting
description: Resolve issues with Firestore in Datastore mode
data_source: docs.cloud.google.com
---

This page shows you how to resolve issues with Firestore in Datastore mode.

## Latency

The table below describes possible causes of increased latency:

| Latency cause                                                                                                                     | Types of operations affected                                        | Resolution                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sustained traffic exceeding the [500-50-5 rule](https://docs.cloud.google.com/datastore/docs/best-practices#ramping_up_traffic) . | read, write                                                         | For rapid traffic increases, Datastore mode attempts to automatically scale to meet the increased demand. When Datastore mode scales, latency begins to decrease. Hot-spots (high read, write, and delete rates to a narrow entity range) limit the ability of Datastore mode to scale. Review [designing for scale](https://docs.cloud.google.com/datastore/docs/best-practices#designing_for_scale) and identify hot-spots in your application. |
| Contention, either from updating a single entity too frequently or from transactions.                                             | read, write                                                         | Reduce the write rate to individual entities. Review [transaction isolation and consistency](https://docs.cloud.google.com/datastore/docs/concepts/transactions#isolation_and_consistency) and how you use transactions.                                                                                                                                                                                                                          |
| Slow merge-join queries.                                                                                                          | read                                                                | For example, queries with multiple equality filters ( `==` ) but not backed by composite indexes can result in slow merge-join queries. To improve performance, add composite indexes for these queries, see [Optimizing indexes](https://docs.cloud.google.com/datastore/docs/concepts/optimize-indexes) .                                                                                                                                       |
| Large reads that return many entities.                                                                                            | read                                                                | Use [query cursors](https://docs.cloud.google.com/datastore/docs/concepts/queries#cursors_limits_and_offsets) to split large reads.                                                                                                                                                                                                                                                                                                               |
| Too many recent deletes.                                                                                                          | read This greatly affects operations that list kinds in a database. | If latency is caused by too many recent deletes, the issue should automatically resolve after some time. If the issue does not resolve, [contact support](https://cloud.google.com/support-hub) .                                                                                                                                                                                                                                                 |
| Index fanout, especially for array properties.                                                                                    | write                                                               | Review [exploding indexes](https://docs.cloud.google.com/datastore/docs/concepts/indexes#exploding_index) and your usage of array properties.                                                                                                                                                                                                                                                                                                     |

## Error Codes

This section lists issues that you might encounter and provides suggestions for how to fix each of them.

### DEADLINE_EXCEEDED

```
DEADLINE_EXCEEDED

A deadline was exceeded on the server.
```

To resolve this issue, see the [guide to troubleshooting latency](https://docs.cloud.google.com/datastore/docs/troubleshooting#latency) .

### ABORTED

The following situations can increase `ABORTED` errors:

- An entity receiving too many updates per second.
- Contention from overlapping transactions.
- Traffic increases that exceed the 500-50-5 rule or encounter hot-spots.

```
ABORTED

Too much contention on these datastore entities. Please try again.
```

Or

```
ABORTED

Aborted due to cross-transaction contention. This occurs when multiple
transactions attempt to access the same data, requiring Datastore mode
to abort at least one in order to enforce serializability.
```

To resolve this issue:

- For rapid traffic increases, Datastore mode attempts to automatically scale to meet the increased demand. When Datastore mode scales, latency begins to decrease.
- Hot-spots limit the ability of Datastore mode to scale up, review [designing for scale](https://docs.cloud.google.com/datastore/docs/best-practices#designing_for_scale) to identify hot-spots.
- Review [data contention in transactions](https://docs.cloud.google.com/datastore/docs/concepts/transactions#isolation_and_consistency) and your usage of transactions.
- Reduce the write rate to individual entities.

### RESOURCE_EXHAUSTED

The following situations can lead to `RESOURCE_EXHAUSTED` errors:

You exceeded the [free tier quota](https://docs.cloud.google.com/datastore/pricing#free_quota) and billing is not enabled for your project.

```
RESOURCE_EXHAUSTED

Some resource has been exhausted, perhaps a per-user quota, or perhaps the entire file system is out of space.
```

To resolve this issue:

- Wait for the daily reset of your free tier quota or [enable billing for your project](https://docs.cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project) .

### INVALID_ARGUMENT

The following situations can cause `INVALID_ARGUMENT` errors:

- Attempting to commit an entity with an **indexed** property value greater than 1500 bytes. This limit applies to the UTF-8 encoding of the property value.
- Attempting to commit an entity with **un-indexed** property values greater than 1,048,487 bytes (1 MiB - 89 bytes). This limit applies to the sum of the property values in an entity. For example, four properties of 256 KiB each exceed the limit.

1,500 bytes (indexed) and 1,048,487 bytes (un-indexed) are [limits](https://docs.cloud.google.com/datastore/docs/concepts/limits) for property values. You cannot exceed these limits and they are not quotas that can be adjusted.

```
INVALID_ARGUMENT: The value of property property-name is longer than 1500 bytes
```

or

```
INVALID_ARGUMENT: The value of property property_name is longer than 1048487 bytes
```

To resolve this issue:

- For indexed property values, split the property into multiple properties. If possible, create an un-indexed property and move data that doesn't need to be indexed into the un-indexed property.
- For un-indexed property values, split the property into multiple properties or implement compression for the property value.
