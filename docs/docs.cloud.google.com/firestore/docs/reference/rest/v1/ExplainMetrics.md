Explain metrics for the query.

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
  &quot;planSummary&quot;: {
    object (PlanSummary)
  },
  &quot;executionStats&quot;: {
    object (ExecutionStats)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  planSummary  `

`  object ( PlanSummary  ` )

Planning phase information for the query.

`  executionStats  `

`  object ( ExecutionStats  ` )

Aggregated stats from the execution of the query. Only present when `  ExplainOptions.analyze  ` is set to true.

## PlanSummary

Planning phase information for the query.

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
  &quot;indexesUsed&quot;: [
    {
      object
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  indexesUsed[]  `

`  object ( Struct  ` format)

The indexes selected for the query. For example: \[ {"queryScope": "Collection", "properties": "(foo ASC, **name** ASC)"}, {"queryScope": "Collection", "properties": "(bar ASC, **name** ASC)"} \]

## ExecutionStats

Execution statistics for the query.

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
  &quot;resultsReturned&quot;: string,
  &quot;executionDuration&quot;: string,
  &quot;readOperations&quot;: string,
  &quot;debugStats&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resultsReturned  `

`  string ( int64 format)  `

Total number of results returned, including documents, projections, aggregation results, keys.

`  executionDuration  `

`  string ( Duration  ` format)

Total time to execute the query in the backend.

A duration in seconds with up to nine fractional digits, ending with ' `  s  ` '. Example: `  "3.5s"  ` .

`  readOperations  `

`  string ( int64 format)  `

Total billable read operations.

`  debugStats  `

`  object ( Struct  ` format)

Debugging statistics from the execution of the query. Note that the debugging stats are subject to change as Firestore evolves. It could include: { "indexes\_entries\_scanned": "1000", "documents\_scanned": "20", "billing\_details" : { "documents\_billable": "20", "index\_entries\_billable": "1000", "min\_query\_cost": "0" } }
