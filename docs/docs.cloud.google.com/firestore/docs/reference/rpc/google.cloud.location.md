## Index

  - `  Locations  ` (interface)
  - `  GetLocationRequest  ` (message)
  - `  ListLocationsRequest  ` (message)
  - `  ListLocationsResponse  ` (message)
  - `  Location  ` (message)

## Locations

An abstract interface that provides location-related information for a service. Service-specific metadata is provided through the `  Location.metadata  ` field.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetLocation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetLocation(              GetLocationRequest            </code> ) returns ( <code dir="ltr" translate="no">             Location            </code> )</p>
<p>Gets information about a location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/datastore</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListLocations</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListLocations(              ListLocationsRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListLocationsResponse            </code> )</p>
<p>Lists information about the supported locations for this service.</p>
<p>This method lists locations based on the resource scope provided in the <code dir="ltr" translate="no">            ListLocationsRequest.name           </code> field:</p>
<ul>
<li><strong>Global locations</strong> : If <code dir="ltr" translate="no">name</code> is empty, the method lists the public locations available to all projects.</li>
<li><strong>Project-specific locations</strong> : If <code dir="ltr" translate="no">name</code> follows the format <code dir="ltr" translate="no">projects/{project}</code> , the method lists locations visible to that specific project. This includes public, private, or other project-specific locations enabled for the project.</li>
</ul>
<p>For gRPC and client library implementations, the resource name is passed as the <code dir="ltr" translate="no">name</code> field. For direct service calls, the resource name is incorporated into the request path based on the specific service implementation and version.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/datastore</code></li>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## GetLocationRequest

The request message for `  Locations.GetLocation  ` .

Fields

`name`

`string`

Resource name for the location.

## ListLocationsRequest

The request message for `  Locations.ListLocations  ` .

Fields

`name`

`string`

The resource that owns the locations collection, if applicable.

`filter`

`string`

A filter to narrow down results to a preferred subset. The filtering language accepts strings like `"displayName=tokyo"` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) .

`page_size`

`int32`

The maximum number of results to return. If not set, the service selects a default.

`page_token`

`string`

A page token received from the `next_page_token` field in the response. Send that page token to receive the subsequent page.

`extra_location_types[]`

`string`

Optional. Do not use this field unless explicitly documented otherwise. This is primarily for internal usage.

## ListLocationsResponse

The response message for `  Locations.ListLocations  ` .

Fields

`locations[]`

`  Location  `

A list of locations that matches the specified filter in the request.

`next_page_token`

`string`

The standard List next-page token.

## Location

A resource that represents a Google Cloud location.

Fields

`name`

`string`

Resource name for the location, which may vary between implementations. For example: `"projects/example-project/locations/us-east1"`

`location_id`

`string`

The canonical id for this location. For example: `"us-east1"` .

`display_name`

`string`

The friendly name for this location, typically a nearby city name. For example, "Tokyo".

`labels`

`map<string, string>`

Cross-service attributes for the location. For example

    {"cloud.googleapis.com/region": "us-east1"}

`metadata`

`  Any  `

Service-specific metadata. For example the available capacity at the given location.
