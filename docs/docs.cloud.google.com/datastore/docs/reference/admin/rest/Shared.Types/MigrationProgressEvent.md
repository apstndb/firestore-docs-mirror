  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [PrepareStepDetails](#PrepareStepDetails)
      - [JSON representation](#PrepareStepDetails.SCHEMA_REPRESENTATION)
  - [RedirectWritesStepDetails](#RedirectWritesStepDetails)
      - [JSON representation](#RedirectWritesStepDetails.SCHEMA_REPRESENTATION)

An event signifying the start of a new step in a [migration from Cloud Datastore to Cloud Firestore in Datastore mode](https://cloud.google.com/datastore/docs/upgrade-to-firestore) .

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
  &quot;step&quot;: enum (MigrationStep),

  // Union field step_details can be only one of the following:
  &quot;prepareStepDetails&quot;: {
    object (PrepareStepDetails)
  },
  &quot;redirectWritesStepDetails&quot;: {
    object (RedirectWritesStepDetails)
  }
  // End of list of possible types for union field step_details.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  step  `

`  enum ( MigrationStep  ` )

The step that is starting.

An event with step set to `  START  ` indicates that the migration has been reverted back to the initial pre-migration state.

Union field `  step_details  ` . Details about this step. `  step_details  ` can be only one of the following:

`  prepareStepDetails  `

`  object ( PrepareStepDetails  ` )

Details for the `  PREPARE  ` step.

`  redirectWritesStepDetails  `

`  object ( RedirectWritesStepDetails  ` )

Details for the `  REDIRECT_WRITES  ` step.

## PrepareStepDetails

Details for the `  PREPARE  ` step.

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
  &quot;concurrencyMode&quot;: enum (ConcurrencyMode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  concurrencyMode  `

`  enum ( ConcurrencyMode  ` )

The concurrency mode this database will use when it reaches the `  REDIRECT_WRITES  ` step.

## RedirectWritesStepDetails

Details for the `  REDIRECT_WRITES  ` step.

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
  &quot;concurrencyMode&quot;: enum (ConcurrencyMode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  concurrencyMode  `

`  enum ( ConcurrencyMode  ` )

The concurrency mode for this database.
