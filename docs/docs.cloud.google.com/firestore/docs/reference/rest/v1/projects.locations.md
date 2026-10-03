---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations
title: 'REST Resource: projects.locations'
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Resource: Location

A resource that represents a Google Cloud location.

**JSON representation**

```
{
  "name": string,
  "locationId": string,
  "displayName": string,
  "labels": {
    string: string,
    ...
  },
  "metadata": {
    "@type": string,
    field1: ...,
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
<p>Resource name for the location, which may vary between implementations. For example: <code>"projects/example-project/locations/us-east1"</code></p></td>
</tr>
<tr class="even">
<td><code>locationId</code></td>
<td><p><code>string</code></p>
<p>The canonical id for this location. For example: <code>"us-east1"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>The friendly name for this location, typically a nearby city name. For example, "Tokyo".</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Cross-service attributes for the location. For example</p>
<pre data-fenced=""><code>{&quot;cloud.googleapis.com/region&quot;: &quot;us-east1&quot;}</code></pre>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><code>object</code></p>
<p>Service-specific metadata. For example the available capacity at the given location.</p>
<p>An object containing fields of an arbitrary type. An additional field <code>"@type"</code> contains a URI identifying the type. Example: <code>{ "id": 1234, "@type": "types.example.com/standard/id" }</code> .</p></td>
</tr>
</tbody>
</table>

| Methods                                                                                          |                                                                   |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| [`get`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/get)   | Gets information about a location.                                |
| [`list`](https://docs.cloud.google.com/firestore/docs/reference/rest/v1/projects.locations/list) | Lists information about the supported locations for this service. |
