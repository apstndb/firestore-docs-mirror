Before you use Firestore in Datastore mode, you must choose a *location* where the project's data is stored. To reduce latency and increase availability, store your data close to the users and services that need it.

**Warning:** Once you select a location for your project, you cannot change it. [Your project's location setting applies to more than one product.](#selecting_a_location)

## Types of locations

You can store your Datastore mode data in either a *multi-region* location or a *regional* location.

Data in a multi-region location operates in a [multi-zone and multi-region replicated configuration](/docs/geography-and-regions#multi-regional_resources) . Select a multi-region location if you want to maximize the availability and durability of your database. Multi-region locations can withstand the loss of an entire region and maintain availability without data loss. In the [Datastore Service Level Agreement](/datastore/sla) , multi-region locations define a higher monthly uptime percentage than regional locations.

Data in a regional location operates in a [multi-zone replicated configuration](/docs/geography-and-regions#regional_resources) . Select a regional location if your application is more sensitive to write latency or if you want [co-location with other Google Cloud resources](/about/locations#products-available-by-region) that your application may use.

### Multi-region locations

A multi-region location consists of a defined set of [regions](/docs/geography-and-regions#regions_and_zones) where multiple replicas of the database are stored. Each replica is either a read-write replica which contains all of the data in the database or a witness replica which does not maintain a full set of data but participates in replication.

By replicating the data between multiple regions, data can continue to be served even with the loss of an entire region. Within a region, data is replicated across [zones](/docs/geography-and-regions#regions_and_zones) so that data can continue to be served within that region even with the loss of a zone.

The following multi-region locations are available:

<table>
<thead>
<tr class="header">
<th>Multi-Region Name</th>
<th>Multi-Region Description</th>
<th>Read-Write Regions</th>
<th>Witness Region</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       eur3      </code></td>
<td>Europe</td>
<td><code dir="ltr" translate="no">       europe-west1      </code> (Belgium), <code dir="ltr" translate="no">       europe-west4      </code> (Netherlands)</td>
<td><code dir="ltr" translate="no">       europe-north1      </code> (Finland)</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       nam5      </code></td>
<td>United States (Central)</td>
<td><code dir="ltr" translate="no">       us-central1      </code> (Iowa), <code dir="ltr" translate="no">       us-central2      </code> (Oklahoma—private Google Cloud region)</td>
<td><code dir="ltr" translate="no">       us-east1      </code> (South Carolina)</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       nam7      </code></td>
<td>United States (Central and East)</td>
<td><code dir="ltr" translate="no">       us-central1      </code> (Iowa), <code dir="ltr" translate="no">       us-east4      </code> (Northern Virginia)</td>
<td><code dir="ltr" translate="no">       us-central2      </code> (Oklahoma—private Google Cloud region)</td>
</tr>
</tbody>
</table>

**Note:** For Legacy Cloud Datastore databases not yet upgraded to Firestore in Datastore mode, see [Multi-region locations (Legacy Cloud Datastore)](/datastore/docs/pre-migration/multi-r) .

### Regional location

A regional location is a specific geographic place, such as South Carolina. The following regional locations are available:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Region Name</th>
<th>Region Description</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>North America</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       us-west1      </code></td>
<td>Oregon</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       us-west2      </code></td>
<td>Los Angeles</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       us-west3      </code></td>
<td>Salt Lake City</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       us-west4      </code></td>
<td>Las Vegas</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        us-central1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Iowa</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       northamerica-northeast1      </code></td>
<td>Montréal</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        northamerica-northeast2       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Toronto</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        northamerica-south1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Queretaro</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       us-east1      </code></td>
<td>South Carolina</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       us-east4      </code></td>
<td>Northern Virginia</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        us-east5       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Columbus</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        us-south1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Dallas</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td><strong>South America</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        southamerica-west1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Santiago</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       southamerica-east1      </code></td>
<td>São Paulo</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td><strong>Europe</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       europe-west2      </code></td>
<td>London</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       europe-west1      </code></td>
<td>Belgium</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-west4       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Netherlands</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       europe-west3      </code></td>
<td>Frankfurt</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-west8       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Milan</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-southwest1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Madrid</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-west9       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Paris</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-west12       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Turin</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-west10       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Berlin</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       europe-north1      </code></td>
<td>Finland</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        europe-north2       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Stockholm</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       europe-central2      </code></td>
<td>Warsaw</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       europe-west6      </code></td>
<td>Zürich</td>
<td><a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
</tr>
<tr class="odd">
<td><strong>Middle East</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        me-central1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Doha</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        me-central2       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Dammam</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><p><code dir="ltr" translate="no">        me-west1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Tel Aviv</td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Asia</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       asia-south1      </code></td>
<td>Mumbai</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        asia-south2       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Delhi</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       asia-southeast1      </code></td>
<td>Singapore</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       asia-southeast2      </code></td>
<td>Jakarta</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       asia-east2      </code></td>
<td>Hong Kong</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       asia-east1      </code></td>
<td>Taiwan</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       asia-northeast1      </code></td>
<td>Tokyo</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><code dir="ltr" translate="no">       asia-northeast2      </code></td>
<td>Osaka</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       asia-northeast3      </code></td>
<td>Seoul</td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Australia</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><code dir="ltr" translate="no">       australia-southeast1      </code></td>
<td>Sydney</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        australia-southeast2       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Melbourne</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Africa</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td><p><code dir="ltr" translate="no">        africa-south1       </code></p>
<p>This location does not support App Engine. If you plan to use App Engine, you should choose a different location.</p></td>
<td>Johannesburg</td>
<td></td>
</tr>
</tbody>
</table>

## Selecting a location

The location setting for your Google Cloud project applies to both Firestore in Datastore mode and App Engine. When you select a location in either product, you set the location for your entire Google Cloud project.

**Important:** After you select the location of your project, you cannot change it.

If you have not yet selected a location for your project, you will be asked to select the location when you complete any of the following tasks:

  - Creating a new App Engine application.
  - [Creating your first Datastore mode entity using the Google Cloud console](/datastore/docs/store-query-data) .

### Viewing the location of your project

Use one of the following methods to find out which location you selected for your project:

  - Run the `  gcloud app describe  ` command.

  - If you have at least one version of an App Engine app deployed, open the [App Engine Dashboard](https://console.cloud.google.com/appengine) in the Google Cloud console. The location information in the upper right-hand corner of the dashboard applies to both App Engine and Firestore in Datastore mode.

## Next steps

  - For more information about building applications to meet your latency, availability and durability requirements, see [Geography and Regions](/docs/geography-and-regions#multi-regional_resources) .
  - For a map of locations, see [Cloud Data Center Locations](/about/datacenters) .
