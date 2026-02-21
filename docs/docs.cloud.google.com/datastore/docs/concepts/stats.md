Firestore in Datastore mode (Datastore) maintains statistics about the data that you store in an application, such as how many entities there are, of what kind, or how much space is used by property values of a given type.

You can view these statistics in the Google Cloud console in one of the following ways:

  - On the [Dashboard](https://console.cloud.google.com/project/_/datastore/stats) page.
  - On the [Entities](https://console.cloud.google.com/project/_/datastore/entities/query/gql) page, run a GQL query in the form of `  SELECT * FROM __Stat_Kind__  ` .
  - Programmatically within the application by querying for specially named entities using the Datastore API. For more information about the Datastore API, see [APIs & Reference](/datastore/docs/apis) .

Datastore uses *kind names* that begin and end with two underscores to identify special entities that provide statistics about your data. These are called *statistics entities* . For example, each app has one entity of the kind `  __Stat_Total__  ` , which represents statistics about all of the entities in a Datastore mode database.

Statistics entities track information about your data and give you insights into your data usage. They are automatically created. Each statistic entity has the following properties:

  - `  count  ` : the number of items considered by the statistic (a long integer)
  - `  bytes  ` : the total size of the items for this statistic (a long integer)
  - `  timestamp  ` : the time of the most recent update to the statistic (a date-time value)

Each entity belongs to a specific kind. *Statistics kind* indicates the category of statistics being collected or used. Use the kind to identify the purpose of a statistic, such as optimizing a query, improving performance, or data analysis.

Some statistic kinds also have additional properties listed in the [List of statistics](#stats-list) section of this document.

When the statistics system creates new statistic entities, it doesn't delete the previous statistic entities right away. The best way to get a consistent view of the statistics is to query for the statistic entity with the most recent `  timestamp  ` , then use that timestamp value as a filter when you fetch other statistic entities.

The statistics system also creates statistics that are specific to each namespace. The kind names of namespace-specific statistics are prefixed with `  __Stat_Ns__  ` , followed by the same suffixes as the kind names of statistics that apply to the whole application.

If an application doesn't use namespaces, the statistics system won't create namespace-specific statistics. You can only find namespace-specific statistics in the namespace that they're relevant to.

## List of statistics

The following is a list of available statistics:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Statistic</th>
<th>Stat Entity Kind</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>all entities</td>
<td><code dir="ltr" translate="no">       __Stat_Total__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_Total__      </code></td>
<td>All entities. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.<br />
• <code dir="ltr" translate="no">       composite_index_bytes      </code> : the storage in composite index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       composite_index_count      </code> : the count of composite index entries.</td>
</tr>
<tr class="even">
<td>all entities in a namespace</td>
<td><code dir="ltr" translate="no">       __Stat_Namespace__      </code><br />
Note that <code dir="ltr" translate="no">       __Stat_Namespace__      </code> entities are created for each namespace encountered and are only found in the empty string namespace.</td>
<td>All entities in a namespace.<br />
<br />
• <code dir="ltr" translate="no">       subject_namespace      </code> : the namespace represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.<br />
• <code dir="ltr" translate="no">       composite_index_bytes      </code> : the storage in composite index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       composite_index_count      </code> : the count of composite index entries.<br />
<br />
For more information, see the <a href="#stats-limitations">Statistics limitations</a> section of this document.<br />
</td>
</tr>
<tr class="odd">
<td>all entries in application defined indexes</td>
<td><code dir="ltr" translate="no">       __Stat_Kind_CompositeIndex__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_Kind_CompositeIndex__      </code><br />
</td>
<td>Entries in the composite index table; one stat entity for each kind of entity stored. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       alphanumeric_id      </code> : the alphanumeric identifier of the index. The same identifier used in <code dir="ltr" translate="no">       gcloud      </code> and the API.<br />
• <code dir="ltr" translate="no">       index_id      </code> : internal integer representation of the index ID. For <code dir="ltr" translate="no">       gcloud      </code> and API methods, use the <code dir="ltr" translate="no">       alphanumeric_id      </code> instead.<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       last_known_usage_timestamp      </code> : the last time this index served a query. Will always be a time between <code dir="ltr" translate="no">       stat_tracked_since_time      </code> and timestamp. Set to <code dir="ltr" translate="no">       null      </code> if no usage was recorded in that time window. Not present for <code dir="ltr" translate="no">       __Stat_Ns_Kind_CompositeIndex__      </code> .<br />
• <code dir="ltr" translate="no">       stat_tracked_since_time      </code> : the start of the time window where index usage is known. Not present for <code dir="ltr" translate="no">       __Stat_Ns_Kind_CompositeIndex__      </code> .</td>
</tr>
<tr class="even">
<td>all entries in built-in indexes</td>
<td><code dir="ltr" translate="no">       __Stat_Kind_BuiltinIndex__      </code></td>
<td>Information about the built-in indexes in the database. One stat entity for each built-in index. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       property_name      </code> : the name of the indexed property.<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string).<br />
• <code dir="ltr" translate="no">       api_scope      </code> : either <code dir="ltr" translate="no">       Firestore      </code> or <code dir="ltr" translate="no">       Datastore      </code> .<br />
• <code dir="ltr" translate="no">       query_scope      </code> : the index query scope. Always set to <code dir="ltr" translate="no">       COLLECTION_GROUP      </code> (kind) for Datastore databases.<br />
• <code dir="ltr" translate="no">       value_mode      </code> : the mode for the query scope such as <code dir="ltr" translate="no">       ASC      </code> or <code dir="ltr" translate="no">       DESC      </code> .<br />
• <code dir="ltr" translate="no">       last_known_usage_timestamp      </code> : the last time this index served a query. Will always be a time between <code dir="ltr" translate="no">       stat_tracked_since_time      </code> and timestamp. Set to <code dir="ltr" translate="no">       null      </code> if no usage was recorded in that time window.<br />
• <code dir="ltr" translate="no">       stat_tracked_since_time      </code> : the start of the time window where index usage is known.</td>
</tr>
<tr class="odd">
<td>entities of a kind</td>
<td><code dir="ltr" translate="no">       __Stat_Kind__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_Kind__      </code></td>
<td>Entities of a kind; one stat entity for each kind of entity stored. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.<br />
• <code dir="ltr" translate="no">       composite_index_bytes      </code> : the storage in composite index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       composite_index_count      </code> : the count of composite index entries.</td>
</tr>
<tr class="even">
<td>root entities of a kind</td>
<td><code dir="ltr" translate="no">       __Stat_Kind_IsRootEntity__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_Kind_IsRootEntity__      </code></td>
<td>Entities of a kind that are entity group root entities (have no ancestor parent); one stat entity for each kind of entity stored. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.</td>
</tr>
<tr class="odd">
<td>non-root entities of a kind</td>
<td><code dir="ltr" translate="no">       __Stat_Kind_NotRootEntity__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_Kind_NotRootEntity__      </code></td>
<td>Entities of a kind that are not entity group root entities (have an ancestor parent); one stat entity for each kind of entity stored. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.</td>
</tr>
<tr class="even">
<td>properties of a type</td>
<td><code dir="ltr" translate="no">       __Stat_PropertyType__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_PropertyType__      </code></td>
<td>Properties of a value type across all entities; one stat entity per value type. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       property_type      </code> : the name of the value type (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.</td>
</tr>
<tr class="odd">
<td>properties of a type per kind</td>
<td><code dir="ltr" translate="no">       __Stat_PropertyType_Kind__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_PropertyType_Kind__      </code></td>
<td>Properties of a value type across entities of a given kind; one stat entity per combination of property type and kind.<br />
<br />
Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       property_type      </code> : the name of the value type (a string)<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in the built-in index measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.<br />
<br />
For more information, see the <a href="#stats-limitations">Statistics limitations</a> section of this document.<br />
</td>
</tr>
<tr class="even">
<td>properties with a name</td>
<td><code dir="ltr" translate="no">       __Stat_PropertyName_Kind__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_PropertyName_Kind__      </code></td>
<td>Properties with a given name across entities of a given kind; one stat entity per combination of unique property name and kind. Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       property_name      </code> : the name of the property (a string)<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string)<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.</td>
</tr>
<tr class="odd">
<td>properties of a type and with a name</td>
<td><code dir="ltr" translate="no">       __Stat_PropertyType_PropertyName_Kind__      </code><br />
Namespace specific entry:<br />
<code dir="ltr" translate="no">       __Stat_Ns_PropertyType_PropertyName_Kind__      </code></td>
<td>Properties with a given name and of a given value type across entities of a given kind; one stat entity per combination of property name, value type and kind that exists in the database.<br />
<br />
Additional properties:<br />
<br />
• <code dir="ltr" translate="no">       property_type      </code> : the name of the value type (a string)<br />
• <code dir="ltr" translate="no">       property_name      </code> : the name of the property (a string).<br />
• <code dir="ltr" translate="no">       kind_name      </code> : the name of the kind represented (a string).<br />
• <code dir="ltr" translate="no">       entity_bytes      </code> : the storage in the entities table measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_bytes      </code> : the storage in built-in index entries measured in bytes.<br />
• <code dir="ltr" translate="no">       builtin_index_count      </code> : the count of built-in index entries.<br />
<br />
For more information, see the <a href="#stats-limitations">Statistics limitations</a> section of this document.<br />
</td>
</tr>
</tbody>
</table>

Some statistics refer to property value types by name, as strings. These names are as follows:

  - `  "Blob"  `
  - `  "BlobKey"  `
  - `  "Boolean"  `
  - `  "Category"  `
  - `  "Date/Time"  `
  - `  "Email"  `
  - `  "Float"  `
  - `  "GeoPt"  `
  - `  "IM"  `
  - `  "Integer"  `
  - `  "Key"  `
  - `  "Link"  `
  - `  "NULL"  `
  - `  "PhoneNumber"  `
  - `  "PostalAddress"  `
  - `  "Rating"  `
  - `  "ShortBlob"  `
  - `  "String"  `
  - `  "Text"  `
  - `  "User"  `

## Statistics limitations

Statistics have the following limitations:

  - The `  __Stat_PropertyType_Kind__  ` property and the `  __Stat_PropertyType_PropertyName_Kind__  ` property return property type metadata for [array](/datastore/docs/concepts/entities#array) value types, and separately record the property type for each value in the array. For example, if an array property stores a list of strings, the property records the property type as `  STRING  ` , while the actual property type is `  ARRAY<STRING>  ` .
  - The `  __Stat_Namespace__  ` entities contain the same information found in `  __Stat_Ns_Total__  ` records. `  __Stat_Namespace__  ` entities are stored in the empty namespace and contain a `  subject_namespace  ` field describing the namespace to which they belong. `  __Stat_Ns_Total__  ` records are stored in the namespace to which they refer, and thus don't contain a `  subject_namespace  ` field. Hence, a query on kind `  __Stat_Namespace__  ` (from the empty string namespace) ordered descending by `  bytes  ` will list the namespaces that consume the largest storage first. Since queries across namespaces are not possible, any query for `  __Stat_Ns_Total__  ` entities will only ever produce at most a single record.

## Statistics entities drop order

Applications with thousands of namespaces, kinds, or property names require a large number of statistics entities. To reduce the overhead of storing and updating the statistics, Firestore in Datastore mode databases progressively drop statistics entities according to the order listed later.

The summary statistics entities `  __Stat_Kind_CompositeIndex__  ` , `  __Stat_PropertyType__  ` , and `  __Stat_Total__  ` are never dropped.

Statistics entities are dropped in groups in the following default order:

1.  per-namespace, per-kind, and per-property statistics:
    
      - `  __Stat_Ns_PropertyName_Kind__  `
      - `  __Stat_Ns_PropertyType_PropertyName_Kind__  `

2.  per-kind and per-property statistics
    
      - `  __Stat_PropertyName_Kind__  `
      - `  __Stat_PropertyType_PropertyName_Kind__  `

3.  per-namespace statistics
    
      - `  __Stat_Namespace__  `
      - `  __Stat_Ns_Kind_CompositeIndex__  `
      - `  __Stat_Ns_PropertyType__  `
      - `  __Stat_Ns_Total__  `

Kind statistics entities have the following drop order:

1.  per-namespace, per-kind statistics
    
      - `  __Stat_Ns_Kind__  `
      - `  __Stat_Ns_Kind_IsRootEntity__  `
      - `  __Stat_Ns_Kind_NotRootEntity__  `
      - `  __Stat_Ns_PropertyType_Kind__  `

2.  per-kind statistics
    
      - `  __Stat_Kind__  `
      - `  __Stat_Kind_IsRootEntity__  `
      - `  __Stat_Kind_NotRootEntity__  `
      - `  __Stat_PropertyType_Kind__  `

## What's next

  - [Locating quota usage information](/datastore/docs/pricing#locating_quota_usage_information_for_your_app)
