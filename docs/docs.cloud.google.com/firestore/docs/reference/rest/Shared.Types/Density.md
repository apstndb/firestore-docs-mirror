---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Density
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/Density
title: Density
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

The density configuration for the index.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>DENSITY_UNSPECIFIED</code></td>
<td>Unspecified. It will use database default setting. This value is input only.</td>
</tr>
<tr class="even">
<td><code>SPARSE_ALL</code></td>
<td><p>An index entry will only exist if ALL fields are present in the document.</p>
<p>This is both the default and only allowed value for Standard Edition databases (for both Cloud Firestore <code>ANY_API</code> and Cloud Datastore <code>DATASTORE_MODE_API</code> ).</p>
<p>Take for example the following document:</p>
<pre data-fenced=""><code>{
  &quot;__name__&quot;: &quot;...&quot;,
  &quot;a&quot;: 1,
  &quot;b&quot;: 2,
  &quot;c&quot;: 3
}</code></pre>
<p>an index on <code>(a ASC, b ASC, c ASC, __name__ ASC)</code> will generate an index entry for this document since <code>a</code> , 'b', <code>c</code> , and <code>__name__</code> are all present but an index of <code>(a ASC, d ASC, __name__ ASC)</code> will not generate an index entry for this document since <code>d</code> is missing.</p>
<p>This means that such indexes can only be used to serve a query when the query has either implicit or explicit requirements that all fields from the index are present.</p></td>
</tr>
<tr class="odd">
<td><code>SPARSE_ANY</code></td>
<td><p>An index entry will exist if ANY field are present in the document.</p>
<p>This is used as the definition of a sparse index for Enterprise Edition databases.</p>
<p>Take for example the following document:</p>
<pre data-fenced=""><code>{
  &quot;__name__&quot;: &quot;...&quot;,
  &quot;a&quot;: 1,
  &quot;b&quot;: 2,
  &quot;c&quot;: 3
}</code></pre>
<p>an index on <code>(a ASC, d ASC)</code> will generate an index entry for this document since <code>a</code> is present, and will fill in an <code>unset</code> value for <code>d</code> . An index on <code>(d ASC, e ASC)</code> will not generate any index entry as neither <code>d</code> nor <code>e</code> are present.</p>
<p>An index that contains <code>__name__</code> will generate an index entry for all documents since Firestore guarantees that all documents have a <code>__name__</code> field.</p></td>
</tr>
<tr class="even">
<td><code>DENSE</code></td>
<td><p>An index entry will exist regardless of if the fields are present or not.</p>
<p>This is the default density for an Enterprise Edition database.</p>
<p>The index will store <code>unset</code> values for fields that are not present in the document.</p></td>
</tr>
</tbody>
</table>
