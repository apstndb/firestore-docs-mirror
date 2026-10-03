---
name: documents/docs.cloud.google.com/firestore/native/docs/keyvis-patterns-index
uri: https://docs.cloud.google.com/firestore/native/docs/keyvis-patterns-index
title: Heatmap patterns for index keys
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Heatmap patterns for index keys

This page shows examples of patterns that you might see in a Key Visualizer heatmap. These patterns can help you troubleshoot specific performance issues.

### Edition and mode requirements

This document applies to Firestore Standard edition in Firestore in Native mode.

## Evenly distributed usage

![Heatmap showing evenly distributed reads and writes](https://docs.cloud.google.com/static/firestore/native/docs/images/keyvis-patterns-ideal.png)

If a heatmap shows a fine-grained mix of dark and bright colors, then write/delete operations for index keys are evenly distributed throughout the database. This heatmap likely represents an effective usage pattern for Firestore.

## Indexes on sequential keys

A heatmap with a single bright diagonal line can indicate an index that is on a key that is strictly increasing or decreasing, such as timestamp. Indexes on sequential keys are not recommended and can create hotspots. When hotspotting, you might observe corresponding elevated latencies.

Some examples of common hotspots on index are as follows:

> **Note:** In the following heatmap example, for Firestore, the x-axis of the heatmap represents time, and the y-axis represents index keys.

### Hotspotting due to increasing timestamp

![Heatmap showing hotspotting due to increasing timestamp](https://docs.cloud.google.com/static/firestore/native/docs/images/keyvis-patterns-timestamp.png)

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on a timestamp field name.

### Hotspotting due to increasing field names

![Heatmap showing hotspotting due to increasing field](https://docs.cloud.google.com/static/firestore/native/docs/images/keyvis-patterns-property.png)

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on an incremental field, such as auto-generated invoice numbers.

To identify the hotspotting issue, use the Key Visualizer tool and [understand the index key structure](https://docs.cloud.google.com/firestore/docs/keyvis-patterns-index#understand_the_index_key_structure) to determine which index causes the issue and exempt those indexes with [best practices](https://docs.cloud.google.com/firestore/native/docs/best-practices#high_read_write_and_delete_rates_to_a_narrow_document_range) .

## Understand the index key structure

Before you understand the structure of index keys that you see in Key Visualizer tool, learn about [indexes](https://docs.cloud.google.com/firestore/native/docs/concepts/index-overview) in Firestore.

The following code shows an example index key format that you see when you hover over the affected key-range on the heatmap.

```
COLLECTION: projects/PROJECT_ID/databases/(default)/documents/Users
  PROPERTIES: (Timestamp: DESC) 
  VALUES: (16500000000000001)
  DOCUMENT: projects/PROJECT_ID/databases/(default)/documents/Users/5000000000000001
```

Where:

- **COLLECTION** : location of the collection in your database. Based on the [scope](https://docs.cloud.google.com/firestore/native/docs/concepts/index-overview#query_scopes) , it can be collection path for collection scope or collection name for collection group scope.
- **PROPERTIES** : fields used to create the index. The [`__name__` ordering property](https://docs.cloud.google.com/firestore/docs/concepts/index-overview#default_ordering_and_the_name_field) is only shown for index definitions that modify the default ordering.
- **VALUES** : value of each property.
- **DOCUMENT** : ID of the document updated in an operation.

From the earlier example, identify the fields from the **PROPERTIES** value to find the affected index.

To find the index, complete the following steps:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Indexes** .

4.  Go to the **Composite** or **Single Field** tab.

    You can identify the type of index by analyzing the **PROPERTIES** field. See [examples of index keys](https://docs.cloud.google.com/firestore/native/docs/keyvis-patterns-index#examples_of_index_key_entries_on_the_heatmap) for more information.

5.  Click **Filter** , select **Fields** , and enter the name of the field.

    Use the **OR** operator to add more fields in case of composite indexes.

After you have identified the index that is causing issues, you can use the following solutions:

- Composite index: Either modify the index to ensure that the field whose value monotonically increases or decreases is not selected as the first field for indexing, or delete the index.

- Single-field index: Add an exemption for the field and the sorting order that you want to exempt. See [Adding a single-field exemption](https://docs.cloud.google.com/firestore/native/docs/concepts/index-overview#single-field_index_exemptions) for more information.

### Examples of index key entries on the heatmap

| Type                                                                      | Description                                                                                                                                                                                                                                                                                                                                                                                         | Example                                                                                                                                                                                                                                                                              |
|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Collection scope single-field Indexes ASC, DESC                           | Firestore creates indexes with collection scope by default. Index entry for the single-field Index on the `Timestamp` field, in descending order for the `Users/5000000000000001` document.                                                                                                                                                                                                         | `COLLECTION: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users` `PROPERTIES: (Timestamp: DESC)` `VALUES: (16500000000000001)` `DOCUMENT: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001`                                             |
| Collection scope single-field Indexes for array fields                    | For each array field in a document, Firestore creates and maintains a collection scope array-contains index. Index entry for array-contains mode single-field indexes that will be created when a field `Country: [USA, Japan]` is added to the document. Note that ASC,DESC indexes will also be created by default for this field. The example shows the ASC index for the `Country` field.       | `COLLECTION: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users` `PROPERTIES:(Country: ASC)` `VALUES:([USA, Japan]) DOCUMENT:(projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001)`                                                        |
| Collection group single-field Indexes ASC, DESC, ARRAY                    | A collection group includes all collections with the same collection ID. Index entry for the collection group single-field Index on the `Timestamp` field, in descending order.                                                                                                                                                                                                                     | `COLLECTION GROUP: Users` `PROPERTIES: (Timestamp: DESC)` `VALUES: (16500000000000001L)` `DOCUMENT: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001`                                                                                                |
| Collection group single-field Indexes ASC, DESC, ARRAY                    | Index entry for the collection group single-field Index on `Country` field in the `array-contains` mode                                                                                                                                                                                                                                                                                             | `COLLECTION GROUP: Users PROPERTIES: (Country: ARRAY ASC) VALUES: (USA) DOCUMENT: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001`                                                                                                                  |
| Collection composite index entry with ASC, ASC, ARRAY properties          | Composite index entries with parent are created when nested documents are created with collection scope index definition. Index entry for composite index with `Timestamp` and `Name` field in ascending order, and `Country` in `array-contains` mode.                                                                                                                                             | `COLLECTION: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users` `PROPERTIES: (Timestamp: ASC, Name: ASC,Country: ARRAY)` `VALUES: (16500000000000001L, 'Alice', 'USA')` `DOCUMENT: (projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001)` |
| Collection group scope composite index entry with ASC, ASC properties     | Index entry for the composite index on the `Timestamp` field, in ascending order and `Name` field in ascending order                                                                                                                                                                                                                                                                                | `COLLECTION GROUP: Users` `PROPERTIES: (Timestamp: ASC, Name: ASC)` `VALUES: (16500000000000001L, 'Alice')` `DOCUMENT: (projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001)`                                                                           |
| Collection scope composite Index entry with ASC and `__name__` properties | Index entry for the composite Index on the `Timestamp` field in ascending order and with `__name__` sorting in descending order for the `Users/5000000000000001` document. You can use `__name__` as the final field in an index definition to change the [default ordering of results](https://docs.cloud.google.com/firestore/docs/concepts/index-overview#default_ordering_and_the_name_field) . | `COLLECTION: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users` `PROPERTIES: (Timestamp: ASC, __name__ DESC)` `VALUES: (16500000000000001)` `DOCUMENT: projects/ `` PROJECT_ID `` /databases/(default)/documents/Users/5000000000000001`                               |

## What's next

- Learn how to [get started with Key Visualizer](https://docs.cloud.google.com/firestore/native/docs/keyvis-getting-started) .
- Find out how to [explore a heatmap in detail](https://docs.cloud.google.com/firestore/native/docs/keyvis-exploring-heatmaps) .
- Read about the [metrics you can view in a heatmap](https://docs.cloud.google.com/firestore/native/docs/key-visualizer#metrics) .
