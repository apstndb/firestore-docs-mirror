  - [JSON representation](#SCHEMA_REPRESENTATION)

Identifies a subset of entities in a project. This is specified as combinations of kinds and namespaces (either or both of which may be all, as described in the following examples). Example usage:

Entire project: kinds=\[\], namespaceIds=\[\]

Kinds Foo and Bar in all namespaces: kinds=\['Foo', 'Bar'\], namespaceIds=\[\]

Kinds Foo and Bar only in the default namespace: kinds=\['Foo', 'Bar'\], namespaceIds=\[''\]

Kinds Foo and Bar in both the default and Baz namespaces: kinds=\['Foo', 'Bar'\], namespaceIds=\['', 'Baz'\]

The entire Baz namespace: kinds=\[\], namespaceIds=\['Baz'\]

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kinds&quot;: [
    string
  ],
  &quot;namespaceIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kinds[]  `

`  string  `

If empty, then this represents all kinds.

`  namespaceIds[]  `

`  string  `

An empty list represents all namespaces. This is the preferred usage for projects that don't use namespaces.

An empty string element represents the default namespace. This should be used if the project has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique.
