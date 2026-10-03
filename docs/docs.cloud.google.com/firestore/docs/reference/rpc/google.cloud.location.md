---
name: documents/docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location
uri: https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location
title: Package google.cloud.location
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

## Index

- [`Locations`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Locations) (interface)
- [`GetLocationRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.GetLocationRequest) (message)
- [`ListLocationsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.ListLocationsRequest) (message)
- [`ListLocationsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.ListLocationsResponse) (message)
- [`Location`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Location) (message)

## Locations

An abstract interface that provides location-related information for a service. Service-specific metadata is provided through the [`Location.metadata`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Location.FIELDS.google.protobuf.Any.google.cloud.location.Location.metadata) field.

**GetLocation**

`rpc GetLocation( `[`GetLocationRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.GetLocationRequest)` ) returns ( `[`Location`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Location)` )`

Gets information about a location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListLocations**

`rpc ListLocations( `[`ListLocationsRequest`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.ListLocationsRequest)` ) returns ( `[`ListLocationsResponse`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.ListLocationsResponse)` )`

Lists information about the supported locations for this service.

This method lists locations based on the resource scope provided in the [`ListLocationsRequest.name`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.ListLocationsRequest.FIELDS.string.google.cloud.location.ListLocationsRequest.name) field:

- **Global locations** : If `name` is empty, the method lists the public locations available to all projects.
- **Project-specific locations** : If `name` follows the format `projects/{project}` , the method lists locations visible to that specific project. This includes public, private, or other project-specific locations enabled for the project.

For gRPC and client library implementations, the resource name is passed as the `name` field. For direct service calls, the resource name is incorporated into the request path based on the specific service implementation and version.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/datastore`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## GetLocationRequest

The request message for [`Locations.GetLocation`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Locations.GetLocation) .

| Fields |                                          |
|--------|------------------------------------------|
| `name` | `string` Resource name for the location. |

## ListLocationsRequest

The request message for [`Locations.ListLocations`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Locations.ListLocations) .

| Fields                   |                                                                                                                                                                                                                 |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                   | `string` The resource that owns the locations collection, if applicable.                                                                                                                                        |
| `filter`                 | `string` A filter to narrow down results to a preferred subset. The filtering language accepts strings like `"displayName=tokyo"` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) . |
| `page_size`              | `int32` The maximum number of results to return. If not set, the service selects a default.                                                                                                                     |
| `page_token`             | `string` A page token received from the `next_page_token` field in the response. Send that page token to receive the subsequent page.                                                                           |
| `extra_location_types[]` | `string` Optional. Do not use this field unless explicitly documented otherwise. This is primarily for internal usage.                                                                                          |

## ListLocationsResponse

The response message for [`Locations.ListLocations`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Locations.ListLocations) .

| Fields            |                                                                                                                                                                                                     |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `locations[]`     | [`Location`](https://docs.cloud.google.com/firestore/docs/reference/rpc/google.cloud.location#google.cloud.location.Location) A list of locations that matches the specified filter in the request. |
| `next_page_token` | `string` The standard List next-page token.                                                                                                                                                         |

## Location

A resource that represents a Google Cloud location.

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
<td><code>location_id</code></td>
<td><p><code>string</code></p>
<p>The canonical id for this location. For example: <code>"us-east1"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>display_name</code></td>
<td><p><code>string</code></p>
<p>The friendly name for this location, typically a nearby city name. For example, "Tokyo".</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Cross-service attributes for the location. For example</p>
<pre data-fenced=""><code>{&quot;cloud.googleapis.com/region&quot;: &quot;us-east1&quot;}</code></pre></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#any"><code>Any</code></a></p>
<p>Service-specific metadata. For example the available capacity at the given location.</p></td>
</tr>
</tbody>
</table>
