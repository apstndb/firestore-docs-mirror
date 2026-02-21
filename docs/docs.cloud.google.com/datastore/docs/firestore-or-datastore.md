When you create a Firestore database, you must choose between two modes: Native mode or Datastore mode. This page explains the difference between the two modes.

## Choose a database mode

When you create a new Firestore database, you must select a database mode. You can have both Native mode and Datastore mode databases in the same project, but each database will be of a single type.

We recommend the following when choosing a database mode:

  - **Use Firestore in Native mode for all new applications (server, mobile, and web).**
    
    Firestore in Native mode uses a document-based data model that aligns with industry standards. In addition to a strongly consistent and scalable database, Firestore in Native mode provides real-time data syncing and backend-as-as-service features.

  - **Use Firestore in Datastore mode if your app depends on the Datastore API.**
    
    Datastore Mode is fully supported and is recommended for applications with a dependency on the Datastore API. Native mode and Datastore mode share an underlying storage layer with the same availability, consistency, and scaling capabilities.

## Firestore in Native mode

Firestore is the next major version of Datastore and a re-branding of the product. Taking the best of Datastore and the [Firebase Realtime Database](https://firebase.google.com/docs/database/rtdb-vs-firestore) , Firestore is a NoSQL document database built for automatic scaling, high performance, and ease of application development.

Firestore introduces the following features:

  - A strongly consistent storage layer
  - A collection and document data model
  - Real-time updates
  - Mobile and Web client libraries

Firestore is backwards compatible with Datastore, but the new data model, real-time updates, and mobile and web client library features are not. To access all Firestore features, you must use Firestore in Native mode.

## Firestore in Datastore mode

Firestore in Datastore mode uses Datastore system behavior but accesses Firestore's storage layer, removing the following Datastore limitations:

  - All Datastore queries are now strongly consistent, unless you explicitly request [eventual consistency](/datastore/docs/reference/data/rpc/google.datastore.v1#google.datastore.v1.ReadOptions) .
  - Queries in transactions are no longer required to be ancestor queries.
  - Transactions are no longer limited to 25 entity groups.
  - Writes to an entity group are no longer limited to 1 per second.

Datastore mode disables Firestore features that are not compatible with Datastore:

  - The project will accept Datastore API requests and deny Firestore API requests.
  - The project will use Datastore indexes instead of Firestore indexes.
  - You can use Datastore client libraries with this project but not Firestore client libraries.
  - Firestore real-time capabilities will not be available.
  - In the Google Cloud console, the database will use the Datastore viewer.

## Pricing and locations

Native mode and Datastore mode databases use the same pricing structure and are available in the same locations. Pricing and locations are described in detail in the following pages:

#### Firestore in Native mode

  - [Firestore pricing](/firestore/pricing)
  - [Firestore locations](/firestore/docs/locations)

#### Firestore in Datastore mode

  - [Firestore in Datastore mode pricing](/datastore/pricing)
  - [Firestore in Datastore mode locations](/datastore/docs/locations)

### Feature comparison

The following table compares the system behavior of the database modes:

Firestore in  
Native mode

Firestore in  
Datastore mode

**Data model**

Document database organized into documents and collections.

Entities organized into kinds and entity groups.

**Storage Layer**

A strongly consistent storage layer.

A strongly consistent storage layer.

**Queries and transactions**

  - Strongly consistent queries across the entire database
  - Transactions can access any number of collections and documents

<!-- end list -->

  - Removes the previous consistency limitations of Datastore
  - Strongly consistent queries across the entire database
  - Transactions can access any number of entity groups

**[Datastore v1 API](/datastore/docs/reference/data/rest) support**

No, requests are denied

Yes

**[Firestore v1 API](/firestore/docs/reference/rest) support**

Yes

No, requests are denied

**Real-time updates**

[Supports the ability to *listen* to a document or a set of documents for real-time updates.](/firestore/docs/query-data/listen)

While listening to a document or set of documents, your clients are notified of any data changes and sent the newest set of data.

Not supported

**Offline data persistence**

[The mobile and web client libraries support offline data persistence.](/firestore/docs/manage-data/enable-offline)

Not supported

**Client libraries**

Firestore client libraries:

  - Java
  - Python
  - PHP
  - Go
  - Ruby
  - C\#
  - Node.js
  - Android
  - iOS+
  - Web
  - C++
  - Unity

Datastore client libraries:

  - Java
  - Python
  - PHP
  - Go
  - Ruby
  - C\#
  - Node.js
  - C++

**Security**

  - Identity and Access Management (IAM) manages database access
  - Firestore Security Rules support serverless authentication and authorization for the mobile and web client libraries

IAM manages database access

**SLA**

[Firestore SLA](/firestore/sla)

[Firestore SLA](/firestore/sla)

**Locations**

Both modes support the same locations. For a detailed list of locations, see the following pages:

  - [Firestore in Native mode locations](/firestore/docs/locations)
  - [Firestore in Datastore mode locations](/datastore/docs/locations)

**Pricing**

Both modes use the same pricing structure for entity and document operations.

Firestore in Datastore mode does not charge for [small operations](/datastore/pricing#small_operations) .

Both modes use the same pricing structure for stored data and network bandwidth.

For more details about pricing, see the following pages:

  - [Firestore in Native mode pricing](/firestore/pricing)
  - [Firestore in Datastore mode pricing](/datastore/pricing)

**Console**

Firebase Console and Google Cloud console Firestore Viewer

Google Cloud console Datastore Viewer

**Namespaces**

Not supported

Namespaces supported

**App Engine client library integration**

Not supported in the App Engine standard environment Python 2.7 and PHP 5.5 runtimes

Supported in the [App Engine standard environment](/appengine/docs/standard) , all other runtimes

Supported in the [App Engine flexible environment](/appengine/docs/flexible) , all runtimes

Supported in all runtimes

## Create a new database

You can create a new Firestore database in either Native mode or Datastore mode. This choice does not depend on the modes of any existing databases in your project.

See [Create and manage databases](/datastore/docs/manage-databases) for more info.

## Change between Native mode and Datastore mode

If your database is empty, you can change between Native mode and Datastore mode.

**Warning:** Mode changes are only allowed if the database is empty of all entities and documents. A mode change takes a few minutes to take effect during which time the database will reject writes.

Change database to **Native mode** :

### gcloud

Use the [gcloud firestore databases update](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command to change your database to Native mode.

``` text
gcloud firestore databases update --type=firestore-native --database='DATABASE_ID'
```

Replace DATABASE\_ID with the ID of your database.

### rest

``` text
curl --request PATCH \
--header "Authorization: Bearer "$(gcloud auth print-access-token) \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{"type":"FIRESTORE_NATIVE"}' \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases/DATABASE_ID?updateMask=type"
```

Replace the following:

  - PROJECT\_ID : the project ID
  - DATABASE\_ID : the database ID

Change database to **Datastore mode** :

### gcloud

Use the [gcloud firestore databases update](https://cloud.google.com/sdk/gcloud/reference/firestore/databases/update) command to change your database to Datastore mode.

``` text
 gcloud firestore databases update --type=datastore-mode --database='DATABASE_ID'
```

Replace DATABASE\_ID with the ID of your database.

### rest

``` text
curl --request PATCH \
--header "Authorization: Bearer "$(gcloud auth print-access-token) \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{"type":"DATASTORE_MODE"}' \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases/DATABASE_ID?updateMask=type"
```

Replace the following:

  - PROJECT\_ID : the project ID
  - DATABASE\_ID : the database ID
