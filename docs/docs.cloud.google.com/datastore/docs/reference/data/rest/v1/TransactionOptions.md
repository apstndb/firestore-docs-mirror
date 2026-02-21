  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [ReadWrite](#ReadWrite)
      - [JSON representation](#ReadWrite.SCHEMA_REPRESENTATION)
  - [ReadOnly](#ReadOnly)
      - [JSON representation](#ReadOnly.SCHEMA_REPRESENTATION)

Options for beginning a new transaction.

Transactions can be created explicitly with calls to `  Datastore.BeginTransaction  ` or implicitly by setting `  ReadOptions.new_transaction  ` in read requests.

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

  // Union field mode can be only one of the following:
  &quot;readWrite&quot;: {
    object (ReadWrite)
  },
  &quot;readOnly&quot;: {
    object (ReadOnly)
  }
  // End of list of possible types for union field mode.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  mode  ` . The `  mode  ` of the transaction, indicating whether write operations are supported. `  mode  ` can be only one of the following:

`  readWrite  `

`  object ( ReadWrite  ` )

The transaction should allow both reads and writes.

`  readOnly  `

`  object ( ReadOnly  ` )

The transaction should only allow reads.

## ReadWrite

Options specific to read / write transactions.

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
  &quot;previousTransaction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  previousTransaction  `

`  string ( bytes format)  `

The transaction identifier of the transaction being retried.

A base64-encoded string.

## ReadOnly

Options specific to read-only transactions.

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
  &quot;readTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  readTime  `

`  string ( Timestamp  ` format)

Reads entities at the given time.

This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .
