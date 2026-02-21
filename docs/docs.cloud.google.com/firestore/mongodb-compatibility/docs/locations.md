# Firestore with MongoDB compatibility locations

When you provision a Firestore database, you must choose a *location* for it. To reduce latency and increase availability, store your data close to the users and services that need it.

You can optionally [create multiple databases](/firestore/mongodb-compatibility/docs/create-databases) in your project, each with its own location setting.

Be aware that once you provision a database, you cannot change its location setting.

## Types of locations

You can store your Firestore with MongoDB compatibility data in a [*multi-region* location](#location-mr) or a [*regional* location](#location-r) .

### Multi-region locations

Select a multi-region location to maximize the availability and durability of your database.

A multi-region location consists of a defined set of [regions](https://cloud.google.com/docs/geography-and-regions#regions_and_zones) where multiple replicas of the database are stored. Each replica is either a read-write replica which contains all of the data in the database or a witness replica which does not maintain a full set of data but participates in replication.

By replicating the data between multiple regions, data can continue to be served even with the loss of an entire region. Within a region, data is replicated across [zones](https://cloud.google.com/docs/geography-and-regions#regions_and_zones) so that data can continue to be served within that region even with the loss of a zone.

Firestore with MongoDB compatibility supports the following multi-region locations:

<table>
<thead>
<tr class="header">
<th>Multi-region name</th>
<th>Multi-region description</th>
<th>Read-Write regions</th>
<th>Witness region</th>
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

### Regional locations

A regional location is a specific geographic place, such as South Carolina. Data in a regional location is replicated in multiple zones within a [region](https://cloud.google.com/docs/geography-and-regions#regional_resources) . All regional locations are separated from other regional locations by at least 100 miles.

Select a regional location for lower costs, for lower write latency if your application is sensitive to latency, or for [co-location with other Google Cloud resources](https://cloud.google.com/about/locations/#products-available-by-region) .

Firestore with MongoDB compatibility supports the following regional resource locations:

Region name

Region description

**North America**

`  us-west1  `

Oregon

`  us-west2  `

Los Angeles

`  us-west3  `

Salt Lake City

`  us-west4  `

Las Vegas

`  us-central1  `

Iowa

`  northamerica-northeast1  `

Montréal

`  northamerica-northeast2  `

Toronto

`  northamerica-south1  `

Queretaro

`  us-east1  `

South Carolina

`  us-east4  `

Northern Virginia

`  us-east5  `

Columbus

`  us-south1  `

Dallas

**South America**

`  southamerica-west1  `

Santiago

`  southamerica-east1  `

São Paulo

**Europe**

`  europe-west2  `

London

`  europe-west1  `

Belgium

`  europe-west4  `

Netherlands

`  europe-west8  `

Milan

`  europe-southwest1  `

Madrid

`  europe-west9  `

Paris

`  europe-west12  `

Turin

`  europe-west10  `

Berlin

`  europe-west3  `

Frankfurt

`  europe-north1  `

Finland

`  europe-north2  `

Stockholm

`  europe-central2  `

Warsaw

`  europe-west6  `

Zürich

**Middle East**

`  me-central1  `

Doha

`  me-central2  `

Dammam

`  me-west1  `

Tel Aviv

**Asia**

`  asia-south1  `

Mumbai

`  asia-south2  `

Delhi

`  asia-southeast1  `

Singapore

`  asia-southeast2  `

Jakarta

`  asia-east2  `

Hong Kong

`  asia-east1  `

Taiwan

`  asia-northeast1  `

Tokyo

`  asia-northeast2  `

Osaka

`  asia-northeast3  `

Seoul

**Australia**

`  australia-southeast1  `

Sydney

`  australia-southeast2  `

Melbourne

**Africa**

`  africa-south1  `

Johannesburg

## Location SLA

Your Firestore with MongoDB compatibility location type determines the [Service Level Agreement (SLA)](/firestore/sla) uptime percentage at General Availability (GA):

<table>
<thead>
<tr class="header">
<th>Covered service</th>
<th>Monthly uptime percentage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Firestore with MongoDB compatibility Multi-Region</td>
<td>&gt;= 99.999%</td>
</tr>
<tr class="even">
<td>Firestore with MongoDB compatibility Regional</td>
<td>&gt;= 99.99%</td>
</tr>
</tbody>
</table>

## Location pricing

Your Firestore with MongoDB compatibility location determines the cost of database operations.

For a comprehensive explanation of pricing per region and per region type, see [Understand Firestore with MongoDB compatibility billing](https://cloud.google.com/firestore/enterprise/pricing) .

## View the location of your databases

Use one of the following methods to view the location setting for your databases:

  - Run the [`  gcloud firestore databases list  `](https://cloud.google.com//sdk/gcloud/reference/firestore/databases/list) command.

  - Open the [database list](https://console.cloud.google.com/firestore/databases) in the Google Cloud console. The location for each database is in the location column.

## Next steps

  - To create a Firestore with MongoDB compatibility database in a specific location, see [Create and manage databases](/firestore/mongodb-compatibility/docs/create-databases)

  - For more information about building applications to meet your latency, availability, and durability requirements, refer to [Geography and Regions](https://cloud.google.com/docs/geography-and-regions#multi-regional_resources) .
