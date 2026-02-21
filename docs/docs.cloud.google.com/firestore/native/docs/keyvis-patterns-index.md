# Heatmap patterns for index keys

This page shows examples of patterns that you might see in a Key Visualizer heatmap. These patterns can help you troubleshoot specific performance issues.

### Edition and mode requirements

This document applies to Firestore Standard edition in Native mode.

## Evenly distributed usage

If a heatmap shows a fine-grained mix of dark and bright colors, then write/delete operations for index keys are evenly distributed throughout the database. This heatmap likely represents an effective usage pattern for Firestore.

## Indexes on sequential keys

A heatmap with a single bright diagonal line can indicate an index that is on a key that is strictly increasing or decreasing, such as timestamp. Indexes on sequential keys are not recommended and can create hotspots. When hotspotting, you might observe corresponding elevated latencies.

Some examples of common hotspots on index are as follows:

**Note:** In the following heatmap example, for Firestore, the x-axis of the heatmap represents time, and the y-axis represents index keys.

### Hotspotting due to increasing timestamp

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on a timestamp field name.

### Hotspotting due to increasing field names

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on an incremental field, such as auto-generated invoice numbers.

To identify the hotspotting issue, use the Key Visualizer tool and [understand the index key structure](/firestore/docs/keyvis-patterns-index#understand_the_index_key_structure) to determine which index causes the issue and exempt those indexes with [best practices](./best-practices#high_read_write_and_delete_rates_to_a_narrow_document_range) .

## Understand the index key structure

Before you understand the structure of index keys that you see in Key Visualizer tool, learn about [indexes](./concepts/index-overview) in Firestore.

The following code shows an example index key format that you see when you hover over the affected key-range on the heatmap.

``` text
COLLECTION: projects/PROJECT_ID/databases/(default)/documents/Users
  PROPERTIES: (Timestamp: DESC) 
  VALUES: (16500000000000001)
  DOCUMENT: projects/PROJECT_ID/databases/(default)/documents/Users/5000000000000001
```

Where:

  - **COLLECTION** : location of the collection in your database. Based on the [scope](./concepts/index-overview#query_scopes) , it can be collection path for collection scope or collection name for collection group scope.
  - **PROPERTIES** : fields used to create the index. The [`  __name__  ` ordering property](/firestore/docs/concepts/index-overview#default_ordering_and_the_name_field) is only shown for index definitions that modify the default ordering.
  - **VALUES** : value of each property.
  - **DOCUMENT** : ID of the document updated in an operation.

From the earlier example, identify the fields from the **PROPERTIES** value to find the affected index.

To find the index, complete the following steps:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Indexes** .

4.  Go to the **Composite** or **Single Field** tab.
    
    You can identify the type of index by analyzing the **PROPERTIES** field. See [examples of index keys](./keyvis-patterns-index#examples_of_index_key_entries_on_the_heatmap) for more information.

5.  Click **Filter** , select **Fields** , and enter the name of the field.
    
    Use the **OR** operator to add more fields in case of composite indexes.

After you have identified the index that is causing issues, you can use the following solutions:

  - Composite index: Either modify the index to ensure that the field whose value monotonically increases or decreases is not selected as the first field for indexing, or delete the index.

  - Single-field index: Add an exemption for the field and the sorting order that you want to exempt. See [Adding a single-field exemption](./concepts/index-overview#single-field_index_exemptions) for more information.

### Examples of index key entries on the heatmap

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Collection scope single-field Indexes ASC, DESC</td>
<td>Firestore creates indexes with collection scope by default.<br />
<br />
Index entry for the single-field Index on the <code dir="ltr" translate="no">       Timestamp      </code> field, in descending order for the <code dir="ltr" translate="no">       Users/5000000000000001      </code> document.</td>
<td><code dir="ltr" translate="no">       COLLECTION: projects/               PROJECT_ID              /databases/(default)/documents/Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC)      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001)      </code><br />
<code dir="ltr" translate="no">       DOCUMENT: projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001      </code></td>
</tr>
<tr class="even">
<td>Collection scope single-field Indexes for array fields</td>
<td>For each array field in a document, Firestore creates and maintains a collection scope array-contains index.<br />
<br />
Index entry for array-contains mode single-field indexes that will be created when a field <code dir="ltr" translate="no">       Country: [USA, Japan]      </code> is added to the document. Note that ASC,DESC indexes will also be created by default for this field. The example shows the ASC index for the <code dir="ltr" translate="no">       Country      </code> field.</td>
<td><code dir="ltr" translate="no">       COLLECTION: projects/               PROJECT_ID              /databases/(default)/documents/Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES:(Country: ASC)      </code><br />
<code dir="ltr" translate="no">       VALUES:([USA, Japan]) DOCUMENT:(projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001)      </code></td>
</tr>
<tr class="odd">
<td>Collection group single-field Indexes ASC, DESC, ARRAY</td>
<td>A collection group includes all collections with the same collection ID.<br />
Index entry for the collection group single-field Index on the <code dir="ltr" translate="no">       Timestamp      </code> field, in descending order.</td>
<td><code dir="ltr" translate="no">       COLLECTION GROUP: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC)      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001L)      </code><br />
<code dir="ltr" translate="no">       DOCUMENT: projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001      </code></td>
</tr>
<tr class="even">
<td>Collection group single-field Indexes ASC, DESC, ARRAY</td>
<td>Index entry for the collection group single-field Index on <code dir="ltr" translate="no">       Country      </code> field in the <code dir="ltr" translate="no">       array-contains      </code> mode</td>
<td><code dir="ltr" translate="no">       COLLECTION GROUP: Users PROPERTIES: (Country: ARRAY ASC) VALUES: (USA) DOCUMENT: projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001      </code></td>
</tr>
<tr class="odd">
<td>Collection composite index entry with ASC, ASC, ARRAY properties</td>
<td>Composite index entries with parent are created when nested documents are created with collection scope index definition.<br />
<br />
Index entry for composite index with <code dir="ltr" translate="no">       Timestamp      </code> and <code dir="ltr" translate="no">       Name      </code> field in ascending order, and <code dir="ltr" translate="no">       Country      </code> in <code dir="ltr" translate="no">       array-contains      </code> mode.</td>
<td><code dir="ltr" translate="no">       COLLECTION: projects/               PROJECT_ID              /databases/(default)/documents/Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: ASC, Name: ASC,Country: ARRAY)      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001L, 'Alice', 'USA')      </code><br />
<code dir="ltr" translate="no">       DOCUMENT: (projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001)      </code></td>
</tr>
<tr class="even">
<td>Collection group scope composite index entry with ASC, ASC properties</td>
<td>Index entry for the composite index on the <code dir="ltr" translate="no">       Timestamp      </code> field, in ascending order and <code dir="ltr" translate="no">       Name      </code> field in ascending order</td>
<td><code dir="ltr" translate="no">       COLLECTION GROUP: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: ASC, Name: ASC)      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001L, 'Alice')      </code><br />
<code dir="ltr" translate="no">       DOCUMENT: (projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001)      </code></td>
</tr>
<tr class="odd">
<td>Collection scope composite Index entry with ASC and <code dir="ltr" translate="no">       __name__      </code> properties</td>
<td>Index entry for the composite Index on the <code dir="ltr" translate="no">       Timestamp      </code> field in ascending order and with <code dir="ltr" translate="no">       __name__      </code> sorting in descending order for the <code dir="ltr" translate="no">       Users/5000000000000001      </code> document. You can use <code dir="ltr" translate="no">       __name__      </code> as the final field in an index definition to change the <a href="/firestore/docs/concepts/index-overview#default_ordering_and_the_name_field">default ordering of results</a> .</td>
<td><code dir="ltr" translate="no">       COLLECTION: projects/               PROJECT_ID              /databases/(default)/documents/Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: ASC, __name__ DESC)      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001)      </code><br />
<code dir="ltr" translate="no">       DOCUMENT: projects/               PROJECT_ID              /databases/(default)/documents/Users/5000000000000001      </code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn how to [get started with Key Visualizer](./keyvis-getting-started) .
  - Find out how to [explore a heatmap in detail](./keyvis-exploring-heatmaps) .
  - Read about the [metrics you can view in a heatmap](./key-visualizer#metrics) .
