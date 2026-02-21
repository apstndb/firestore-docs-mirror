# Supported data types

This page describes the data types that Firestore supports.

## Data types

The following table lists the data types supported by Firestore. It also describes the sort order used when comparing values of the same type:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Data type</th>
<th>Sort order</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Array</td>
<td>By element values</td>
<td><p>An array cannot contain another array value as one of its elements.</p>
<p>Within an array, elements maintain the position assigned to them. When sorting two or more arrays, arrays are ordered based on their element values.</p>
<p>When comparing two arrays, the first elements of each array are compared. If the first elements are equal, then the second elements are compared and so on until a difference is found. If an array runs out of elements to compare but is equal up to that point, then the shorter array is ordered before the longer array.</p>
<p>For example, <code dir="ltr" translate="no">        [1, 2, 3] &lt; [1, 2, 3, 1] &lt; [2]       </code> . The array <code dir="ltr" translate="no">        [2]       </code> has the greatest first element value. The array <code dir="ltr" translate="no">        [1, 2, 3]       </code> has elements equal to the first three elements of <code dir="ltr" translate="no">        [1, 2, 3, 1]       </code> but is shorter in length.</p></td>
</tr>
<tr class="even">
<td>Boolean</td>
<td><code dir="ltr" translate="no">       false      </code> &lt; <code dir="ltr" translate="no">       true      </code></td>
<td>—</td>
</tr>
<tr class="odd">
<td>Bytes</td>
<td>Byte order</td>
<td>Up to 1,048,487 bytes (1 MiB - 89 bytes). Only the first 1,500 bytes are considered by queries.</td>
</tr>
<tr class="even">
<td>Date and time</td>
<td>Chronological</td>
<td>When stored in Firestore, precise only to microseconds; any additional precision is rounded down.</td>
</tr>
<tr class="odd">
<td>Floating-point number</td>
<td>Numeric</td>
<td>64-bit double precision according to <a href="https://en.wikipedia.org/wiki/IEEE_754">IEEE 754</a> , including (normalized) <code dir="ltr" translate="no">       NaN      </code> &amp; <code dir="ltr" translate="no">       +/-Infinity      </code> .</td>
</tr>
<tr class="even">
<td>Geographical point</td>
<td>By latitude, then longitude</td>
<td>At this time we do not recommend using this data type due to querying limitations. It is generally better to store latitude and longitude as separate numeric fields. If your app needs simple distance-based geoqueries, see <a href="../solutions/geoqueries">Geo queries</a></td>
</tr>
<tr class="odd">
<td>Integer</td>
<td>Numeric</td>
<td>64-bit, signed</td>
</tr>
<tr class="even">
<td>Map</td>
<td>By keys, then by value</td>
<td><p>Represents an object embedded within a document. When indexed, you can query on subfields. If you exclude this value from indexing, then all subfields are also excluded from indexing.</p>
<p>Key ordering is always sorted. For example, if you write <code dir="ltr" translate="no">        {c: "foo", a: "bar", b: "qux"}       </code> the map is sorted by key and saved as <code dir="ltr" translate="no">        {a: "bar", b: "qux", c: "foo"}       </code> .</p>
<p>Map fields are sorted by key and compared by key-value pairs, first comparing the keys and then the values. If the first key-value pairs are equal, the next key-value pairs are compared, and so on. If two maps have all of the same key-value pairs, then map length is considered. For example, the following maps are in ascending order:</p>
<p><code dir="ltr" translate="no">        {a: "aaa", b: "baz"}       </code><br />
<code dir="ltr" translate="no">        {a: "foo", b: "bar"}       </code><br />
<code dir="ltr" translate="no">        {a: "foo", b: "bar", c: "qux"}       </code><br />
<code dir="ltr" translate="no">        {a: "foo", b: "baz"}       </code><br />
<code dir="ltr" translate="no">        {b: "aaa", c: "baz"}       </code><br />
<code dir="ltr" translate="no">        {c: "aaa"}       </code><br />
</p></td>
</tr>
<tr class="odd">
<td>Null</td>
<td>None</td>
<td>—</td>
</tr>
<tr class="even">
<td>Reference</td>
<td>By path elements (collection, document ID, collection, document ID...)</td>
<td>For example, <code dir="ltr" translate="no">       projects/[PROJECT_ID]/databases/[DATABASE_ID]/documents/[DOCUMENT_PATH]      </code> .</td>
</tr>
<tr class="odd">
<td>Text string</td>
<td>UTF-8 encoded byte order</td>
<td>Up to 1,048,487 bytes (1 MiB - 89 bytes). Only the first 1,500 bytes of the UTF-8 representation are considered by queries.</td>
</tr>
<tr class="even">
<td>Vector</td>
<td>By dimension and then by individual element values</td>
<td>The max supported embedding dimension is 2048. To store vectors with larger dimensions, use <a href="https://en.wikipedia.org/wiki/Dimensionality_reduction">dimensionality reduction</a> .</td>
</tr>
</tbody>
</table>

## Value type ordering

When a query involves a field with values of mixed types, Firestore uses a deterministic ordering based on the internal representations. The following list shows the order:

1.  Null values
2.  Boolean values
3.  Integer and floating-point values, sorted in numerical order
4.  Date values
5.  Text string values
6.  Byte values
7.  Firestore references
8.  Geographical point values
9.  Array values
10. Vector embeddings
11. Map values

## Numeric ordering

Firestore sorts all numeric values ( `  Integer  ` & `  Floating point  ` ) interleaved with each other. Floating point comparison follows the total ordering of [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) with the notable exception being that Firestore normalizes all `  NaN  ` values, and considers it less than `  -Infinity  ` .
