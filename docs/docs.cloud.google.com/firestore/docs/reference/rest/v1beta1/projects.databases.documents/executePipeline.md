Executes a pipeline query.

### HTTP request

`  POST https://firestore.googleapis.com/v1beta1/{database=projects/*/databases/*}/documents:executePipeline  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  database  `

`  string  `

Required. Database identifier, in the form `  projects/{project}/databases/{database}  ` .

### Request body

The request body contains data with the following structure:

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

  // Union field pipeline_type can be only one of the following:
  &quot;structuredPipeline&quot;: {
    object (StructuredPipeline)
  }
  // End of list of possible types for union field pipeline_type.

  // Union field consistency_selector can be only one of the following:
  &quot;transaction&quot;: string,
  &quot;newTransaction&quot;: {
    object (TransactionOptions)
  },
  &quot;readTime&quot;: string
  // End of list of possible types for union field consistency_selector.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  pipeline_type  ` .

`  pipeline_type  ` can be only one of the following:

`  structuredPipeline  `

`  object ( StructuredPipeline  ` )

A pipelined operation.

Union field `  consistency_selector  ` . Optional consistency arguments, defaults to strong consistency. `  consistency_selector  ` can be only one of the following:

`  transaction  `

`  string ( bytes format)  `

Run the query within an already active transaction.

The value here is the opaque transaction ID to execute the query in.

A base64-encoded string.

`  newTransaction  `

`  object ( TransactionOptions  ` )

Execute the pipeline in a new transaction.

The identifier of the newly created transaction will be returned in the first response on the stream. This defaults to a read-only transaction.

`  readTime  `

`  string ( Timestamp  ` format)

Execute the pipeline in a snapshot transaction at the given time.

This must be a microsecond precision timestamp within the past one hour, or if Point-in-Time Recovery is enabled, can additionally be a whole minute timestamp within the past 7 days.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Response body

The response for \[Firestore.Execute\]\[\].

If successful, the response body contains data with the following structure:

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
  &quot;transaction&quot;: string,
  &quot;results&quot;: [
    {
      object (Document)
    }
  ],
  &quot;executionTime&quot;: string,
  &quot;explainStats&quot;: {
    object (ExplainStats)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transaction  `

`  string ( bytes format)  `

Newly created transaction identifier.

This field is only specified as part of the first response from the server, alongside the `  results  ` field when the original request specified \[ExecuteRequest.new\_transaction\]\[\].

A base64-encoded string.

`  results[]  `

`  object ( Document  ` )

An ordered batch of results returned executing a pipeline.

The batch size is variable, and can even be zero for when only a partial progress message is returned.

The fields present in the returned documents are only those that were explicitly requested in the pipeline, this includes those like `  __name__  ` and `  __update_time__  ` . This is explicitly a divergence from `  Firestore.RunQuery  ` / `  Firestore.GetDocument  ` RPCs which always return such fields even when they are not specified in the `  mask  ` .

`  executionTime  `

`  string ( Timestamp  ` format)

The time at which the results are valid.

This is a (not strictly) monotonically increasing value across multiple responses in the same stream. The API guarantees that all previously returned results are still valid at the latest `  executionTime  ` . This allows the API consumer to treat the query if it ran at the latest `  executionTime  ` returned.

If the query returns no results, a response with `  executionTime  ` and no `  results  ` will be sent, and this represents the time at which the operation was run.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  explainStats  `

`  object ( ExplainStats  ` )

Query explain stats.

This is present on the **last** response if the request configured explain to run in 'analyze' or 'explain' mode in the pipeline options. If the query does not return any results, a response with `  explainStats  ` and no `  results  ` will still be sent.

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

## StructuredPipeline

A Firestore query represented as an ordered list of operations / stages.

This is considered the top-level function which plans and executes a query. It is logically equivalent to `  query(stages, options)  ` , but prevents the client from having to build a function wrapper.

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
  &quot;pipeline&quot;: {
    object (Pipeline)
  },
  &quot;options&quot;: {
    string: {
      object (Value)
    },
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  pipeline  `

`  object ( Pipeline  ` )

Required. The pipeline query to execute.

`  options  `

`  map (key: string, value: object ( Value  ` ))

Optional. Optional query-level arguments.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## ExplainStats

Pipeline explain stats.

Depending on the explain options in the original request, this can contain the optimized plan and / or execution stats.

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
  &quot;data&quot;: {
    &quot;@type&quot;: string,
    field1: ...,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  data  `

`  object  `

The format depends on the `  output_format  ` options in the request.

Currently there are two supported options: `  TEXT  ` and `  JSON  ` . Both supply a `  google.protobuf.StringValue  ` .

An object containing fields of an arbitrary type. An additional field `  "@type"  ` contains a URI identifying the type. Example: `  { "id": 1234, "@type": "types.example.com/standard/id" }  ` .
