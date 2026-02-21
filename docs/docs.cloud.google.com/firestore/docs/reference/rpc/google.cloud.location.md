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
<td><p><code dir="ltr" translate="no">           rpc GetLocation(                         GetLocationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Location            </code> )</p>
<p>Gets information about a location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
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
<td><p><code dir="ltr" translate="no">           rpc ListLocations(                         ListLocationsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListLocationsResponse            </code> )</p>
<p>Lists information about the supported locations for this service. This method can be called in two ways:</p>
<ul>
<li><strong>List all public locations:</strong> Use the path <code dir="ltr" translate="no">            GET /v1/locations           </code> .</li>
<li><strong>List project-visible locations:</strong> Use the path <code dir="ltr" translate="no">            GET /v1/projects/{project_id}/locations           </code> . This may include public locations as well as private or other locations specifically visible to the project.</li>
</ul>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/datastore             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## GetLocationRequest

The request message for `  Locations.GetLocation  ` .

Fields

`  name  `

`  string  `

Resource name for the location.

## ListLocationsRequest

The request message for `  Locations.ListLocations  ` .

Fields

`  name  `

`  string  `

The resource that owns the locations collection, if applicable.

`  filter  `

`  string  `

A filter to narrow down results to a preferred subset. The filtering language accepts strings like `  "displayName=tokyo"  ` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) .

`  page_size  `

`  int32  `

The maximum number of results to return. If not set, the service selects a default.

`  page_token  `

`  string  `

A page token received from the `  next_page_token  ` field in the response. Send that page token to receive the subsequent page.

`  extra_location_types[]  `

`  string  `

Optional. Do not use this field. It is unsupported and is ignored unless explicitly documented otherwise. This is primarily for internal usage.

## ListLocationsResponse

The response message for `  Locations.ListLocations  ` .

Fields

`  locations[]  `

`  Location  `

A list of locations that matches the specified filter in the request.

`  next_page_token  `

`  string  `

The standard List next-page token.

## Location

A resource that represents a Google Cloud location.

Fields

`  name  `

`  string  `

Resource name for the location, which may vary between implementations. For example: `  "projects/example-project/locations/us-east1"  `

`  location_id  `

`  string  `

The canonical id for this location. For example: `  "us-east1"  ` .

`  display_name  `

`  string  `

The friendly name for this location, typically a nearby city name. For example, "Tokyo".

`  labels  `

`  map<string, string>  `

Cross-service attributes for the location. For example

``` text
{"cloud.googleapis.com/region": "us-east1"}
```

`  metadata  `

`  Any  `

Service-specific metadata. For example the available capacity at the given location.
