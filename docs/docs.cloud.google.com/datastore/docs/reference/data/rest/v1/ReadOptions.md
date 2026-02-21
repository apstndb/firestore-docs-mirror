  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [ReadConsistency](#ReadConsistency)

The options shared by read requests.

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

  // Union field consistency_type can be only one of the following:
  &quot;readConsistency&quot;: enum (ReadConsistency),
  &quot;transaction&quot;: string,
  &quot;newTransaction&quot;: {
    object (TransactionOptions)
  },
  &quot;readTime&quot;: string
  // End of list of possible types for union field consistency_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  consistency_type  ` . For Cloud Firestore in Datastore mode, if you don't specify read\_consistency then all lookups and queries default to `  read_consistency  ` = `  STRONG  ` . Note that, in Cloud Datastore, global queries defaulted to `  read_consistency  ` = `  EVENTUAL  ` .

Explicitly setting `  read_consistency  ` = `  EVENTUAL  ` will result in eventually consistent lookups and queries. `  consistency_type  ` can be only one of the following:

`  readConsistency  `

`  enum ( ReadConsistency  ` )

The non-transactional read consistency to use.

`  transaction  `

`  string ( bytes format)  `

The identifier of the transaction in which to read. A transaction identifier is returned by a call to `  Datastore.BeginTransaction  ` .

A base64-encoded string.

`  newTransaction  `

`  object ( TransactionOptions  ` )

Options for beginning a new transaction for this request.

The new transaction identifier will be returned in the corresponding response as either `  LookupResponse.transaction  ` or `  RunQueryResponse.transaction  ` .

`  readTime  `

`  string ( Timestamp  ` format)

Reads entities as they were at the given time. This value is only supported for Cloud Firestore in Datastore mode.

This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

## ReadConsistency

The possible values for read consistencies.

Enums

`  READ_CONSISTENCY_UNSPECIFIED  `

Unspecified. This value must not be used.

`  STRONG  `

Strong consistency.

`  EVENTUAL  `

Eventual consistency.
