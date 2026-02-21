This page shows examples of patterns that you might see in a Key Visualizer heatmap. These patterns can help you troubleshoot specific performance issues.

## Evenly distributed usage

If a heatmap shows a fine-grained mix of dark and bright colors, then write/delete operations for index keys are evenly distributed throughout the database. This heatmap likely represents an effective usage pattern for Datastore mode.

## Indexes on sequential keys

A heatmap with a single bright diagonal line can indicate an index that is on a key that is strictly increasing or decreasing, such as timestamp. Indexes on sequential keys are not recommended and can create hotspots. When hotspotting, you might observe corresponding elevated latencies.

Some examples of common hotspots on index are as follows:

**Note:** In the following heatmap example, for Datastore mode, the x-axis of the heatmap represents time, and the y-axis represents index keys.

### Hotspotting due to increasing timestamp

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on a timestamp property.

### Hotspotting due to increasing property names

In this example, a heatmap with a single bright diagonal line can indicate a database that uses strictly increasing or decreasing index write/delete operations on an incremental property, such as auto-generated invoice numbers.

To identify the hotspotting issue, use the Key Visualizer tool and [understand the index key structure](/datastore/docs/keyvis-patterns-index#understand_index_key_structure) to determine which index causes the issue and exempt those indexes with [best practices](./best-practices#high_read_write_and_delete_rates_to_a_narrow_document_range) .

## Understand the index key structure

Before you understand the structure of index keys that you see in Key Visualizer tool, learn about [indexes](./concepts/indexes) in Datastore mode.

The following code shows an example index key format that you see when you hover over the affected key-range on the heatmap.

``` text
NAMESPACE: NS KIND: Users 
PROPERTIES: (Timestamp: DESC, Name: DESC)
ANCESTOR: KEY(PROJECT('PROJECT_ID'),NAMESPACE('NS'),`UserList`,1)
VALUES: (16500000000000001,'Alice')
ENTITY:KEY(PROJECT('PROJECT_ID'),NAMESPACE(''),`UserList`,1,`User`,5000000000000001)
```

Where:

  - **NAMESPACE** : [namespace](./concepts/multitenancy) of the entity.
  - **KIND** : [kind](./concepts/entities#kinds_and_identifiers) of entity that categorizes the entities.
  - **PROPERTIES** : [properties](./concepts/entities#properties_and_value_types) related to the entity. The `  __key__  ` ordering property is only shown for index definitions that modify the default ordering.
  - **ANCESTOR** : optional [ancestor path](./concepts/entities#ancestor_paths) to locate the entity within the database hierarchy.
  - **VALUES** : value of each property.
  - **ENTITY** : ID of the entity updated in an operation.

From the earlier example, identify the properties from the **PROPERTIES** value to find the affected index.

To find the index, complete the following steps:

1.  Go to the **Datastore mode Indexes** page in Google Cloud console.
    
    You can identify the type of index by analyzing the **PROPERTIES** field. See [examples of index keys](./keyvis-patterns-index#examples_of_index_key_entries_on_the_heatmap) for more information.

2.  Click **Filter** , select **Fields** , and enter the name of the field.
    
    Use the **OR** operator to add more properties in case of composite indexes.

After you have identified the index that is causing issues, you can use the following solutions:

  - Built-in index: Exclude the property such that the index doesn't maintain index entries for that property. See [Excluded properties](./concepts/indexes#unindexed_properties) for more information.
  - Composite index: Either modify the index in the `  index.yaml  ` file to ensure that the field whose value monotonically increases or decreases is not selected as the first field for indexing, or delete the index. See [About index.yaml](./tools/indexconfig#Datastore_About_index_yaml) for more information.

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
<td>Built-in index entry</td>
<td>Index entry for the single property index on the <code dir="ltr" translate="no">       Timestamp      </code> property, in descending order for the <code dir="ltr" translate="no">       NS      </code> namespace.</td>
<td><code dir="ltr" translate="no">       NAMESPACE: NS      </code><br />
<code dir="ltr" translate="no">       KIND: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC)      </code><br />
<code dir="ltr" translate="no">       ANCESTOR: NONE      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001)      </code><br />
<code dir="ltr" translate="no">       ENTITY: KEY(PROJECT('               PROJECT_ID              '), NAMESPACE('NS'),      </code> Users <code dir="ltr" translate="no">       , 5000000000000001)      </code></td>
</tr>
<tr class="even">
<td>Built-in index entry</td>
<td>Index entry for the single property index in the default namespace.</td>
<td><code dir="ltr" translate="no">       NAMESPACE: ' '      </code><br />
<code dir="ltr" translate="no">       KIND: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC)      </code><br />
<code dir="ltr" translate="no">       ANCESTOR: NONE      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001)      </code><br />
<code dir="ltr" translate="no">       ENTITY: KEY(PROJECT('               PROJECT_ID              '), NAMESPACE('NS'),      </code> Users <code dir="ltr" translate="no">       , 5000000000000001)      </code></td>
</tr>
<tr class="odd">
<td>Composite index entry</td>
<td>Index entry for the composite index on the <code dir="ltr" translate="no">       Timestamp      </code> property and the <code dir="ltr" translate="no">       Name      </code> property in descending order without ancestor enabled.</td>
<td><code dir="ltr" translate="no">       NAMESPACE: NS      </code><br />
<code dir="ltr" translate="no">       KIND: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC, Name: DESC)      </code><br />
<code dir="ltr" translate="no">       ANCESTOR: NONE      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001, 'Alice')      </code><br />
<code dir="ltr" translate="no">       ENTITY: KEY(PROJECT('               PROJECT_ID              '),NAMESPACE('NS'),      </code> Users <code dir="ltr" translate="no">       ,5000000000000001)      </code></td>
</tr>
<tr class="even">
<td>Composite index entry with ancestor</td>
<td>Index entry for the composite index on the <code dir="ltr" translate="no">       Timestamp      </code> property in descending order and the <code dir="ltr" translate="no">       Name      </code> property in descending order with ancestor enabled.</td>
<td><code dir="ltr" translate="no">       NAMESPACE: NS      </code><br />
<code dir="ltr" translate="no">       KIND: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: DESC, Name: ASC)      </code><br />
<code dir="ltr" translate="no">       ANCESTOR: KEY(PROJECT('               PROJECT_ID              '),NAMESPACE('NS'),      </code> UserList <code dir="ltr" translate="no">       ,1,      </code> User <code dir="ltr" translate="no">       ,5000000000000001      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001, 'Alice')      </code><br />
<code dir="ltr" translate="no">       ENTITY: KEY(PROJECT('               PROJECT_ID              '),NAMESPACE('NS'),      </code> UserList <code dir="ltr" translate="no">       ,1,      </code> User <code dir="ltr" translate="no">       ,5000000000000001)      </code></td>
</tr>
<tr class="odd">
<td>Composite index entry with <code dir="ltr" translate="no">       __key__      </code></td>
<td>Index entry for the composite index on the <code dir="ltr" translate="no">       Timestamp      </code> property in ascending order and the <code dir="ltr" translate="no">       __key__      </code> in descending order without ancestor enabled. You can use <code dir="ltr" translate="no">       __key__      </code> as the final property in an index definition to change the default ordering of results.</td>
<td><code dir="ltr" translate="no">       NAMESPACE: NS      </code><br />
<code dir="ltr" translate="no">       KIND: Users      </code><br />
<code dir="ltr" translate="no">       PROPERTIES: (Timestamp: ASC, __key__ DESC)      </code><br />
<code dir="ltr" translate="no">       ANCESTOR: NONE      </code><br />
<code dir="ltr" translate="no">       VALUES: (16500000000000001)      </code><br />
<code dir="ltr" translate="no">       ENTITY: KEY(PROJECT('               PROJECT_ID              '),NAMESPACE('NS'),      </code> UserList <code dir="ltr" translate="no">       ,1,      </code> User <code dir="ltr" translate="no">       ,5000000000000001)      </code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn how to [get started with Key Visualizer](./keyvis-getting-started) .
  - Find out how to [explore a heatmap in detail](./keyvis-exploring-heatmaps) .
  - Read about the [metrics you can view in a heatmap](./key-visualizer#metrics) .
