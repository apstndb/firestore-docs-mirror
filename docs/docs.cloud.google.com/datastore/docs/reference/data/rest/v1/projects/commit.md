  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
      - [JSON representation](#body.request_body.SCHEMA_REPRESENTATION)
  - [Response body](#body.response_body)
      - [JSON representation](#body.CommitResponse.SCHEMA_REPRESENTATION)
  - [Authorization scopes](#body.aspect)
  - [Mode](#Mode)
  - [Mutation](#Mutation)
      - [JSON representation](#Mutation.SCHEMA_REPRESENTATION)
  - [ConflictResolutionStrategy](#ConflictResolutionStrategy)
  - [PropertyTransform](#PropertyTransform)
      - [JSON representation](#PropertyTransform.SCHEMA_REPRESENTATION)
  - [ServerValue](#ServerValue)
  - [MutationResult](#MutationResult)
      - [JSON representation](#MutationResult.SCHEMA_REPRESENTATION)
  - [Try it\!](#try-it)

Commits a transaction, optionally creating, deleting or modifying some entities.

### HTTP request

`  POST https://datastore.googleapis.com/v1/projects/{projectId}:commit  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  projectId  `

`  string  `

Required. The ID of the project against which to make the request.

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
  &quot;databaseId&quot;: string,
  &quot;mode&quot;: enum (Mode),
  &quot;mutations&quot;: [
    {
      object (Mutation)
    }
  ],

  // Union field transaction_selector can be only one of the following:
  &quot;transaction&quot;: string,
  &quot;singleUseTransaction&quot;: {
    object (TransactionOptions)
  }
  // End of list of possible types for union field transaction_selector.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  databaseId  `

`  string  `

The ID of the database against which to make the request.

'(default)' is not allowed; please use empty string '' to refer the default database.

`  mode  `

`  enum ( Mode  ` )

The type of commit to perform. Defaults to `  TRANSACTIONAL  ` .

`  mutations[]  `

`  object ( Mutation  ` )

The mutations to perform.

When mode is `  TRANSACTIONAL  ` , mutations affecting a single entity are applied in order. The following sequences of mutations affecting a single entity are not permitted in a single `  projects.commit  ` request:

  - `  insert  ` followed by `  insert  `
  - `  update  ` followed by `  insert  `
  - `  upsert  ` followed by `  insert  `
  - `  delete  ` followed by `  update  `

When mode is `  NON_TRANSACTIONAL  ` , no two mutations may affect a single entity.

Union field `  transaction_selector  ` . Must be set when mode is `  TRANSACTIONAL  ` . `  transaction_selector  ` can be only one of the following:

`  transaction  `

`  string ( bytes format)  `

The identifier of the transaction associated with the commit. A transaction identifier is returned by a call to `  Datastore.BeginTransaction  ` .

A base64-encoded string.

`  singleUseTransaction  `

`  object ( TransactionOptions  ` )

Options for beginning a new transaction for this request. The transaction is committed when the request completes. If specified, `  TransactionOptions.mode  ` must be `  TransactionOptions.ReadWrite  ` .

### Response body

The response for `  Datastore.Commit  ` .

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
  &quot;mutationResults&quot;: [
    {
      object (MutationResult)
    }
  ],
  &quot;indexUpdates&quot;: integer,
  &quot;commitTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  mutationResults[]  `

`  object ( MutationResult  ` )

The result of performing the mutations. The i-th mutation result corresponds to the i-th mutation in the request.

`  indexUpdates  `

`  integer  `

The number of index entries updated during the commit, or zero if none were updated.

`  commitTime  `

`  string ( Timestamp  ` format)

The transaction commit timestamp. Not set for non-transactional commits.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `  https://www.googleapis.com/auth/datastore  `
  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .

## Mode

The modes available for commits.

Enums

`  MODE_UNSPECIFIED  `

Unspecified. This value must not be used.

`  TRANSACTIONAL  `

Transactional: The mutations are either all applied, or none are applied. Learn about transactions [here](https://cloud.google.com/datastore/docs/concepts/transactions) .

`  NON_TRANSACTIONAL  `

Non-transactional: The mutations may not apply as all or none.

## Mutation

A mutation to apply to an entity.

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
  &quot;conflictResolutionStrategy&quot;: enum (ConflictResolutionStrategy),
  &quot;propertyMask&quot;: {
    object (PropertyMask)
  },
  &quot;propertyTransforms&quot;: [
    {
      object (PropertyTransform)
    }
  ],

  // Union field operation can be only one of the following:
  &quot;insert&quot;: {
    object (Entity)
  },
  &quot;update&quot;: {
    object (Entity)
  },
  &quot;upsert&quot;: {
    object (Entity)
  },
  &quot;delete&quot;: {
    object (Key)
  }
  // End of list of possible types for union field operation.

  // Union field conflict_detection_strategy can be only one of the following:
  &quot;baseVersion&quot;: string,
  &quot;updateTime&quot;: string
  // End of list of possible types for union field conflict_detection_strategy.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  conflictResolutionStrategy  `

`  enum ( ConflictResolutionStrategy  ` )

The strategy to use when a conflict is detected. Defaults to `  SERVER_VALUE  ` . If this is set, then `  conflict_detection_strategy  ` must also be set.

`  propertyMask  `

`  object ( PropertyMask  ` )

The properties to write in this mutation. None of the properties in the mask may have a reserved name, except for `  __key__  ` . This field is ignored for `  delete  ` .

If the entity already exists, only properties referenced in the mask are updated, others are left untouched. Properties referenced in the mask but not in the entity are deleted.

`  propertyTransforms[]  `

`  object ( PropertyTransform  ` )

Optional. The transforms to perform on the entity.

This field can be set only when the operation is `  insert  ` , `  update  ` , or `  upsert  ` . If present, the transforms are be applied to the entity regardless of the property mask, in order, after the operation.

Union field `  operation  ` . The mutation operation.

For `  insert  ` , `  update  ` , and `  upsert  ` : - The entity's key must not be reserved/read-only. - No property in the entity may have a reserved name, not even a property in an entity in a value. - No value in the entity may have meaning 18, not even a value in an entity in another value. `  operation  ` can be only one of the following:

`  insert  `

`  object ( Entity  ` )

The entity to insert. The entity must not already exist. The entity key's final path element may be incomplete.

`  update  `

`  object ( Entity  ` )

The entity to update. The entity must already exist. Must have a complete key path.

`  upsert  `

`  object ( Entity  ` )

The entity to upsert. The entity may or may not already exist. The entity key's final path element may be incomplete.

`  delete  `

`  object ( Key  ` )

The key of the entity to delete. The entity may or may not already exist. Must have a complete key path and must not be reserved/read-only.

Union field `  conflict_detection_strategy  ` . When set, the server will detect whether or not this mutation conflicts with the current version of the entity on the server. Conflicting mutations are not applied, and are marked as such in MutationResult. `  conflict_detection_strategy  ` can be only one of the following:

`  baseVersion  `

`  string ( int64 format)  `

The version of the entity that this mutation is being applied to. If this does not match the current version on the server, the mutation conflicts.

`  updateTime  `

`  string ( Timestamp  ` format)

The update time of the entity that this mutation is being applied to. If this does not match the current update time on the server, the mutation conflicts.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

## ConflictResolutionStrategy

The possible ways to resolve a conflict detected in a mutation.

Enums

`  STRATEGY_UNSPECIFIED  `

Unspecified. Defaults to `  SERVER_VALUE  ` .

`  SERVER_VALUE  `

The server entity is kept.

`  FAIL  `

The whole commit request fails.

## PropertyTransform

A transformation of an entity property.

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
  &quot;property&quot;: string,

  // Union field transform_type can be only one of the following:
  &quot;setToServerValue&quot;: enum (ServerValue),
  &quot;increment&quot;: {
    object (Value)
  },
  &quot;maximum&quot;: {
    object (Value)
  },
  &quot;minimum&quot;: {
    object (Value)
  },
  &quot;appendMissingElements&quot;: {
    object (ArrayValue)
  },
  &quot;removeAllFromArray&quot;: {
    object (ArrayValue)
  }
  // End of list of possible types for union field transform_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  property  `

`  string  `

Optional. The name of the property.

Property paths (a list of property names separated by dots ( `  .  ` )) may be used to refer to properties inside entity values. For example `  foo.bar  ` means the property `  bar  ` inside the entity property `  foo  ` .

If a property name contains a dot `  .  ` or a backlslash `  \  ` , then that name must be escaped.

Union field `  transform_type  ` . The transformation to apply to the property. `  transform_type  ` can be only one of the following:

`  setToServerValue  `

`  enum ( ServerValue  ` )

Sets the property to the given server value.

`  increment  `

`  object ( Value  ` )

Adds the given value to the property's current value.

This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the given value. If either of the given value or the current property value are doubles, both values will be interpreted as doubles. Double arithmetic and representation of double values follows IEEE 754 semantics. If there is positive/negative integer overflow, the property is resolved to the largest magnitude positive/negative integer.

`  maximum  `

`  object ( Value  ` )

Sets the property to the maximum of its current value and the given value.

This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the given value. If a maximum operation is applied where the property and the input value are of mixed types (that is - one is an integer and one is a double) the property takes on the type of the larger operand. If the operands are equivalent (e.g. 3 and 3.0), the property does not change. 0, 0.0, and -0.0 are all zero. The maximum of a zero stored value and zero input value is always the stored value. The maximum of any numeric value x and NaN is NaN.

`  minimum  `

`  object ( Value  ` )

Sets the property to the minimum of its current value and the given value.

This must be an integer or a double value. If the property is not an integer or double, or if the property does not yet exist, the transformation will set the property to the input value. If a minimum operation is applied where the property and the input value are of mixed types (that is - one is an integer and one is a double) the property takes on the type of the smaller operand. If the operands are equivalent (e.g. 3 and 3.0), the property does not change. 0, 0.0, and -0.0 are all zero. The minimum of a zero stored value and zero input value is always the stored value. The minimum of any numeric value x and NaN is NaN.

`  appendMissingElements  `

`  object ( ArrayValue  ` )

Appends the given elements in order if they are not already present in the current property value. If the property is not an array, or if the property does not yet exist, it is first set to the empty array.

Equivalent numbers of different types (e.g. 3L and 3.0) are considered equal when checking if a value is missing. NaN is equal to NaN, and the null value is equal to the null value. If the input contains multiple equivalent values, only the first will be considered.

The corresponding transform result will be the null value.

`  removeAllFromArray  `

`  object ( ArrayValue  ` )

Removes all of the given elements from the array in the property. If the property is not an array, or if the property does not yet exist, it is set to the empty array.

Equivalent numbers of different types (e.g. 3L and 3.0) are considered equal when deciding whether an element should be removed. NaN is equal to NaN, and the null value is equal to the null value. This will remove all equivalent values if there are duplicates.

The corresponding transform result will be the null value.

## ServerValue

A value that is calculated by the server.

Enums

`  SERVER_VALUE_UNSPECIFIED  `

Unspecified. This value must not be used.

`  REQUEST_TIME  `

The time at which the server processed the request, with millisecond precision. If used on multiple properties (same or different entities) in a transaction, all the properties will get the same server timestamp.

## MutationResult

The result of applying a mutation.

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
  &quot;key&quot;: {
    object (Key)
  },
  &quot;version&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;conflictDetected&quot;: boolean,
  &quot;transformResults&quot;: [
    {
      object (Value)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  key  `

`  object ( Key  ` )

The automatically allocated key. Set only when the mutation allocated a key.

`  version  `

`  string ( int64 format)  `

The version of the entity on the server after processing the mutation. If the mutation doesn't change anything on the server, then the version will be the version of the current entity or, if no entity is present, a version that is strictly greater than the version of any previous entity and less than the version of any possible future entity.

`  createTime  `

`  string ( Timestamp  ` format)

The create time of the entity. This field will not be set after a 'delete'.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

The update time of the entity on the server after processing the mutation. If the mutation doesn't change anything on the server, then the timestamp will be the update timestamp of the current entity. This field will not be set after a 'delete'.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  conflictDetected  `

`  boolean  `

Whether a conflict was detected for this mutation. Always false when a conflict detection strategy field is not set in the mutation.

`  transformResults[]  `

`  object ( Value  ` )

The results of applying each `  PropertyTransform  ` , in the same order of the request.
