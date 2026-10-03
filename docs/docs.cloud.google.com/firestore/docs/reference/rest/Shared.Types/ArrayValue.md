---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue
title: ArrayValue
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

An array value.

**JSON representation**

```
{
  "values": [
    {
      object (Value)
    }
  ]
}
```

| Fields     |                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `object ( `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value)` )` Values in the array. |

## Value

A message that can hold any of the supported value types.

**JSON representation**

```
{

  // Union field value_type can be only one of the following:
  "nullValue": null,
  "booleanValue": boolean,
  "integerValue": string,
  "doubleValue": number,
  "timestampValue": string,
  "stringValue": string,
  "bytesValue": string,
  "referenceValue": string,
  "geoPointValue": {
    object (LatLng)
  },
  "arrayValue": {
    object (ArrayValue)
  },
  "mapValue": {
    object (MapValue)
  },
  "fieldReferenceValue": string,
  "variableReferenceValue": string,
  "functionValue": {
    object (Function)
  },
  "pipelineValue": {
    object (Pipeline)
  }
  // End of list of possible types for union field value_type.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Union field <code>value_type</code> . Must have a value set. <code>value_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>nullValue</code></td>
<td><p><code>null</code></p>
<p>A null value.</p></td>
</tr>
<tr class="odd">
<td><code>booleanValue</code></td>
<td><p><code>boolean</code></p>
<p>A boolean value.</p></td>
</tr>
<tr class="even">
<td><code>integerValue</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>An integer value.</p></td>
</tr>
<tr class="odd">
<td><code>doubleValue</code></td>
<td><p><code>number</code></p>
<p>A double value.</p></td>
</tr>
<tr class="even">
<td><code>timestampValue</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>A timestamp value.</p>
<p>Precise only to microseconds. When stored, any additional precision is rounded down.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>stringValue</code></td>
<td><p><code>string</code></p>
<p>A string value.</p>
<p>The string, represented as UTF-8, must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes of the UTF-8 representation are considered by queries.</p></td>
</tr>
<tr class="even">
<td><code>bytesValue</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p>A bytes value.</p>
<p>Must not exceed 1 MiB - 89 bytes. Only the first 1,500 bytes are considered by queries.</p>
<p>A base64-encoded string.</p></td>
</tr>
<tr class="odd">
<td><code>referenceValue</code></td>
<td><p><code>string</code></p>
<p>A reference to a document. For example: <code>projects/{projectId}/databases/{databaseId}/documents/{document_path}</code> .</p></td>
</tr>
<tr class="even">
<td><code>geoPointValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/LatLng"><code>LatLng</code></a><code> )</code></p>
<p>A geo point value representing a point on the surface of Earth.</p></td>
</tr>
<tr class="odd">
<td><code>arrayValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue"><code>ArrayValue</code></a><code> )</code></p>
<p>An array value.</p>
<p>Cannot directly contain another array value, though can contain a map which contains another array.</p></td>
</tr>
<tr class="even">
<td><code>mapValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#MapValue"><code>MapValue</code></a><code> )</code></p>
<p>A map value.</p></td>
</tr>
<tr class="odd">
<td><code>fieldReferenceValue</code></td>
<td><p><code>string</code></p>
<p>Value which references a field.</p>
<p>This is considered relative (vs absolute) since it only refers to a field and not a field within a particular document.</p>
<p><strong>Requires:</strong></p>
<ul>
<li><p>Must follow [field reference][FieldReference.field_path] limitations.</p></li>
<li><p>Not allowed to be used when writing documents.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code>variableReferenceValue</code></td>
<td><p><code>string</code></p>
<p>Pointer to a variable defined elsewhere in a pipeline.</p>
<p>Unlike <code>fieldReferenceValue</code> which references a field within a document, this refers to a variable, defined in a separate namespace than the fields of a document.</p></td>
</tr>
<tr class="odd">
<td><code>functionValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Function"><code>Function</code></a><code> )</code></p>
<p>A value that represents an unevaluated expression.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>Not allowed to be used when writing documents.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>pipelineValue</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Pipeline"><code>Pipeline</code></a><code> )</code></p>
<p>A value that represents an unevaluated pipeline.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>Not allowed to be used when writing documents.</li>
</ul></td>
</tr>
</tbody>
</table>

## MapValue

A map value.

**JSON representation**

```
{
  "fields": {
    string: {
      object (Value)
    },
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: object ( `[`Value`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value)` ))` The map's fields. The map keys represent field names. Field names matching the regular expression `__.*__` are reserved. Reserved field names are forbidden except in certain documented contexts. The map keys, represented as UTF-8, must not exceed 1,500 bytes and cannot be empty. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

## Function

Represents an unevaluated scalar expression.

For example, the expression `like(user_name, "%alice%")` is represented as:

```
name: "like"
args { fieldReference: "user_name" }
args { stringValue: "%alice%" }
```

**JSON representation**

```
{
  "name": string,
  "args": [
    {
      object (Value)
    }
  ],
  "options": {
    string: {
      object (Value)
    },
    ...
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the function to evaluate.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>must be in snake case (lower case with underscore separator).</li>
</ul></td>
</tr>
<tr class="even">
<td><code>args[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value"><code>Value</code></a><code> )</code></p>
<p>Optional. Ordered list of arguments the given function expects.</p></td>
</tr>
<tr class="odd">
<td><code>options</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value"><code>Value</code></a><code> ))</code></p>
<p>Optional. Optional named arguments that certain functions may support.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>

## Pipeline

A Firestore query represented as an ordered list of operations / stages.

**JSON representation**

```
{
  "stages": [
    {
      object (Stage)
    }
  ]
}
```

| Fields     |                                                                                                                                                                   |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stages[]` | `object ( `[`Stage`](https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Stage)` )` Required. Ordered list of stages to evaluate. |

## Stage

A single operation within a pipeline.

A stage is made up of a unique name, and a list of arguments. The exact number of arguments & types is dependent on the stage type.

To give an example, the stage `filter(state = "MD")` would be encoded as:

```
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

**JSON representation**

```
{
  "name": string,
  "args": [
    {
      object (Value)
    }
  ],
  "options": {
    string: {
      object (Value)
    },
    ...
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the stage to evaluate.</p>
<p><strong>Requires:</strong></p>
<ul>
<li>must be in snake case (lower case with underscore separator).</li>
</ul></td>
</tr>
<tr class="even">
<td><code>args[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value"><code>Value</code></a><code> )</code></p>
<p>Optional. Ordered list of arguments the given stage expects.</p></td>
</tr>
<tr class="odd">
<td><code>options</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/ArrayValue#Value"><code>Value</code></a><code> ))</code></p>
<p>Optional. Optional named arguments that certain functions may support.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>
