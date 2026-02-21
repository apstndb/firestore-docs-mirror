# Locations

When you provision a Firestore instance, you must choose a *location* for the instance. To reduce latency and increase availability, store your data close to the users and services that need it.

You can optionally [create multiple databases](/firestore/docs/manage-databases) in your project, each with its own location setting.

Be aware that once you provision a database instance, you cannot change its location setting.

**Important** : The location setting for your *default* Firestore database instance has a [dependency on the "location of default Google Cloud resources"](#default-cloud-location) . This means that when you provision your default Firestore database, its location might have already been set, either during project creation or when setting up another service that shares this location dependency.

Any non-default Firestore database instances in your project do not share this location dependency.

## Types of locations

You can store your Firestore data in a [*multi-region* location](#location-mr) or a [*regional* location](#location-r) .

### Multi-region locations

Select a multi-region location to maximize the availability and durability of your database.

A multi-region location consists of a defined set of [regions](https://cloud.google.com/docs/geography-and-regions#regions_and_zones) where multiple replicas of the database are stored. Each replica is either a read-write replica which contains all of the data in the database or a witness replica which does not maintain a full set of data but participates in replication.

By replicating the data between multiple regions, data can continue to be served even with the loss of an entire region. Within a region, data is replicated across [zones](https://cloud.google.com/docs/geography-and-regions#regions_and_zones) so that data can continue to be served within that region even with the loss of a zone.

Firestore supports the following multi-region locations:

### Standard edition

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
<td><code dir="ltr" translate="no">          eur3         </code></td>
<td>Europe</td>
<td><code dir="ltr" translate="no">          europe-west1         </code> (Belgium), <code dir="ltr" translate="no">          europe-west4         </code> (Netherlands)</td>
<td><code dir="ltr" translate="no">          europe-north1         </code> (Finland)</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">          nam5         </code></td>
<td>United States (Central)</td>
<td><code dir="ltr" translate="no">          us-central1         </code> (Iowa), <code dir="ltr" translate="no">          us-central2         </code> (Oklahoma—private GCP region)</td>
<td><code dir="ltr" translate="no">          us-east1         </code> (South Carolina)</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">          nam7         </code></td>
<td>United States (Central and East)</td>
<td><code dir="ltr" translate="no">          us-central1         </code> (Iowa), <code dir="ltr" translate="no">          us-east4         </code> (Northern Virginia)</td>
<td><code dir="ltr" translate="no">          us-central2         </code> (Oklahoma—private Google Cloud region)</td>
</tr>
</tbody>
</table>

### Enterprise edition

During the Preview, Firestore in Native mode for Enterprise edition is available in the following multi-region locations:

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
<td><code dir="ltr" translate="no">          nam5         </code></td>
<td>United States (Central)</td>
<td><code dir="ltr" translate="no">          us-central1         </code> (Iowa), <code dir="ltr" translate="no">          us-central2         </code> (Oklahoma—private GCP region)</td>
<td><code dir="ltr" translate="no">          us-east1         </code> (South Carolina)</td>
</tr>
</tbody>
</table>

**Note:** If your project already has an App Engine app with a location of either `  us-central  ` or `  europe-west  ` , then your *default* Firestore database will be considered [multi-regional](#location-mr) .

### Regional locations

A regional location is a specific geographic place, such as South Carolina. Data in a regional location is replicated in multiple zones within a [region](https://cloud.google.com/docs/geography-and-regions#regional_resources) .

Select a regional location for lower costs, for lower write latency if your application is sensitive to latency, or for [co-location with other Google Cloud resources](https://cloud.google.com/about/locations/#products-available-by-region) .

Firestore supports the following regional resource locations:

### Standard edition

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

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Iowa

`  northamerica-northeast1  `

Montréal

`  northamerica-northeast2  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Toronto

`  northamerica-south1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Queretaro

`  us-east1  `

South Carolina

`  us-east4  `

Northern Virginia

`  us-east5  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Columbus

`  us-south1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Dallas

**South America**

`  southamerica-west1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Santiago

`  southamerica-east1  `

São Paulo

**Europe**

`  europe-west2  `

London

`  europe-west1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Belgium

`  europe-west4  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Netherlands

`  europe-west8  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Milan

`  europe-southwest1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Madrid

`  europe-west9  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Paris

`  europe-west12  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Turin

`  europe-west10  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Berlin

`  europe-west3  `

Frankfurt

`  europe-north1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Finland

`  europe-north2  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Stockholm

`  europe-central2  `

Warsaw

`  europe-west6  `

Zürich

**Middle East**

`  me-central1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Doha

`  me-central2  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Dammam

`  me-west1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Tel Aviv

**Asia**

`  asia-south1  `

Mumbai

`  asia-south2  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

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

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Melbourne

**Africa**

`  africa-south1  `

This location does not support App Engine. If you plan to use App Engine, you should choose a different location.

Johannesburg

### Enterprise edition

During the Preview, Firestore in Native mode for Enterprise edition is available in the following regional locations:

Region name

Region description

**North America**

`  us-east4  `

Northern Virginia

**South America**

`  southamerica-east1  `

São Paulo

**Europe**

`  europe-west4  `

Netherlands

**Asia**

`  asia-south1  `

Mumbai

`  asia-east1  `

Taiwan

## Location SLA

Your Firestore location type determines the [Service Level Agreement (SLA)](https://cloud.google.com/firestore/sla) uptime percentage:

<table>
<thead>
<tr class="header">
<th>Covered service</th>
<th>Monthly uptime percentage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Firestore Multi-Region</td>
<td>&gt;= 99.999%</td>
</tr>
<tr class="even">
<td>Firestore Regional</td>
<td>&gt;= 99.99%</td>
</tr>
</tbody>
</table>

## Location pricing

Your Firestore location determines the cost of database operations.

For a comprehensive explanation of pricing per region and per region type, see [Understand Firestore billing](/firestore/pricing) .

## View the location of your databases

Use one of the following methods to view the location setting for your databases:

  - Run the [`  gcloud firestore databases list  `](/sdk/gcloud/reference/firestore/databases/list) command.

  - Open the [database list](https://console.cloud.google.com/firestore/databases) in the Google Cloud console. The location for each database is in the location column.

  - In the Firebase console, go to the [Firestore *Data* tab](https://console.firebase.google.com/project/_/firestore/databases/_/data) to view the list of your database instances and their locations.

## Possible location dependencies due to "location for default Google Cloud resources"

The "location for default Google Cloud resources" is the location setting for any project resources associated with Google App Engine, including the following:

  - default Firestore database instance
  - default Cloud Storage for Firebase bucket with the name format of `  *.appspot.com  `
  - Google Cloud Scheduler used specifically with 1st gen scheduled functions

**Note:** None of the other resources in your project share this location dependency, including the following: Realtime Database instances, non-default Firestore instances, non-default Cloud Storage buckets, default Cloud Storage buckets with the name format of `  *.firebasestorage.app  ` , non-scheduled functions, and 2nd gen scheduled functions.

This "location for default Google Cloud resources" is an immutable setting. Also, when you set the location for one of the associated resources, you indirectly set the location for all of them due to their common association with App Engine.

However, with many changes to the Firebase and Google Cloud ecosystem over the years, the associations of resources to App Engine have been changing. Most notably, starting October 30, 2024 , all newly provisioned default Cloud Storage for Firebase buckets have the name format `  *.firebasestorage.app  ` , and they are *not* associated with App Engine.

**Key Point:** Starting October 30, 2024 , provisioning the default Cloud Storage for Firebase bucket does not set the "location for default Google Cloud resources" (like the location for the project's default Firestore instance). Also, provisioning the default Firestore instance no longer sets the location for a new default Cloud Storage for Firebase bucket (with name format of `  *.firebasestorage.app  ` ).

Here are the details of what changed in the possible **location dependencies** :

  - Starting October 30, 2024 , **if the default Firestore instance and the default Cloud Storage for Firebase bucket are *not* yet provisioned:**
    
      - Provisioning the default Firestore instance sets the location for any future App Engine app provisioned in the project. However, it does *not* dictate the location of the future default Cloud Storage bucket.
    
      - Provisioning the default Cloud Storage bucket *no longer* provisions an App Engine app. Thus, the location of the default Cloud Storage bucket does *not* dictate the location of the future default Firestore instance.

  - Starting October 30, 2024 , **if the default Firestore instance has *already* been provisioned, but the default Cloud Storage for Firebase bucket has *not* been provisioned:**
    
      - The existing default Firestore instance does *not* dictate the location of the future default Cloud Storage bucket ( `  *.firebasestorage.app  ` ).

  - Starting October 30, 2024 , **if the default Cloud Storage for Firebase bucket has *already* been provisioned** (specifically, the `  *.appspot.com  ` bucket) **, but the default Firestore instance has *not* been provisioned:**
    
      - Back when the default Cloud Storage bucket ( `  *.appspot.com  ` ) was provisioned, an App Engine app was *also* provisioned, and thus the location of the future default Firestore instance was set at that time. Even if you delete the `  *.appspot.com  ` bucket, you can't delete the App Engine app, so the location setting of the future default Firestore instance is already set.

If you used ***1st gen scheduled* functions** , then their location is set to the location for default Google Cloud resources. This is because Cloud Scheduler and App Engine previously had an association with each other. Also, if you set up 1st gen scheduled functions *before* provisioning other resources that shared this location setting, then you set their location, too.

Note that if you have an App Engine app with a location of either `  us-central  ` or `  europe-west  ` , then your location for default Google Cloud resources is considered [multi-regional](/firestore/docs/locations#location-mr) .

## Next steps

  - To create a Firestore database in specific location, visit one of the [Firestore quickstarts](/firestore/docs/quickstarts) .

<!-- end list -->

  - For more information about building applications to meet your latency, availability, and durability requirements, refer to [Geography and Regions](https://cloud.google.com/docs/geography-and-regions#multi-regional_resources) .
