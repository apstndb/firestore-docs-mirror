An array value.

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
  &quot;values&quot;: [
    {
      object (Value)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  values[]  `

`  object ( Value  ` )

Values in the array.

## Value

A message that can hold any of the supported value types.

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

  // Union field value_type can be only one of the following:
  &quot;nullValue&quot;: null,
  &quot;booleanValue&quot;: boolean,
  &quot;integerValue&quot;: string,
  &quot;doubleValue&quot;: number,
  &quot;timestampValue&quot;: string,
  &quot;stringValue&quot;: string,
  &quot;bytesValue&quot;: string,
  &quot;referenceValue&quot;: string,
  &quot;geoPointValue&quot;: {
    object (LatLng)
  },
  &quot;arrayValue&quot;: {
    object (ArrayValue)
  },
  &quot;mapValue&quot;: {
    object (MapValue)
  },
  &quot;fieldReferenceValue&quot;: string,
  &quot;functionValue&quot;: {
    object (Function)
  },
  &quot;pipelineValue&quot;: {
    object (Pipeline)
  }
  // End of list of possible types for union field value_type.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  value_type  ` . Must have a value set. `  value_type  ` can be only one of the following:

`  nullValue  `

`  null  `

A null value.

`  booleanValue  `

`  boolean  `

A boolean value.

`  integerValue  `

`  string ( int64 format)  `

An integer value.

`  doubleValue  `

`  number  `

A double value.

`  timestampValue  `

`  string ( Timestamp  ` format)

A timestamp value.

Precise only to microseconds. When stored, any additional precision is rounded down.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  stringValue  `

`  string  `

A string value.

The string, represented as UTF-8, must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes of the UTF-8 representation are considered by queries.

`  bytesValue  `

`  string ( bytes format)  `

A bytes value.

Must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes are considered by queries.

A base64-encoded string.

`  referenceValue  `

`  string  `

A reference to a document. For example: `  projects/{projectId}/databases/{databaseId}/documents/{document_path}  ` .

`  geoPointValue  `

`  object ( LatLng  ` )

A geo point value representing a point on the surface of Earth.

`  arrayValue  `

`  object ( ArrayValue  ` )

An array value.

Cannot directly contain another array value, though can contain a map which contains another array.

`  mapValue  `

`  object ( MapValue  ` )

A map value.

`  fieldReferenceValue  `

`  string  `

Value which references a field.

This is considered relative (vs absolute) since it only refers to a field and not a field within a particular document.

**Requires:**

  - Must follow \[field reference\]\[FieldReference.field\_path\] limitations.

  - Not allowed to be used when writing documents.

`  functionValue  `

`  object ( Function  ` )

A value that represents an unevaluated expression.

**Requires:**

  - Not allowed to be used when writing documents.

`  pipelineValue  `

`  object ( Pipeline  ` )

A value that represents an unevaluated pipeline.

**Requires:**

  - Not allowed to be used when writing documents.

## MapValue

A map value.

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
  &quot;fields&quot;: {
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

`  fields  `

`  map (key: string, value: object ( Value  ` ))

The map's fields.

The map keys represent field names. Field names matching the regular expression `  __.*__  ` are reserved. Reserved field names are forbidden except in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## Function

Represents an unevaluated scalar expression.

For example, the expression `  like(user_name, "%alice%")  ` is represented as:

``` text
name: "like"
args { fieldReference: "user_name" }
args { stringValue: "%alice%" }
```

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
  &quot;name&quot;: string,
  &quot;args&quot;: [
    {
      object (Value)
    }
  ],
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

`  name  `

`  string  `

Required. The name of the function to evaluate.

**Requires:**

  - must be in snake case (lower case with underscore separator).

`  args[]  `

`  object ( Value  ` )

Optional. Ordered list of arguments the given function expects.

`  options  `

`  map (key: string, value: object ( Value  ` ))

Optional. Optional named arguments that certain functions may support.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## Pipeline

A Firestore query represented as an ordered list of operations / stages.

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
  &quot;stages&quot;: [
    {
      object (Stage)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  stages[]  `

`  object ( Stage  ` )

Required. Ordered list of stages to evaluate.

## Stage

A single operation within a pipeline.

A stage is made up of a unique name, and a list of arguments. The exact number of arguments & types is dependent on the stage type.

To give an example, the stage `  filter(state = "MD")  ` would be encoded as:

``` text
name: "filter"
args {
  functionValue {
    name: "eq"
    args { fieldReferenceValue: "state" }
    args { stringValue: "MD" }
  }
}
```

See public documentation for the full list.

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
  &quot;name&quot;: string,
  &quot;args&quot;: [
    {
      object (Value)
    }
  ],
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

`  name  `

`  string  `

Required. The name of the stage to evaluate.

**Requires:**

  - must be in snake case (lower case with underscore separator).

`  args[]  `

`  object ( Value  ` )

Optional. Ordered list of arguments the given stage expects.

`  options  `

`  map (key: string, value: object ( Value  ` ))

Optional. Optional named arguments that certain functions may support.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .
