# Firestore overview

Firestore is a flexible, scalable database for mobile, web, and server development from Firebase and Google Cloud. Firestore keeps your data in sync across client apps through realtime listeners and offers offline support for mobile and web so you can build responsive apps that work regardless of network latency or Internet connectivity. Firestore in Native Mode also offers seamless integration with other Firebase and Google Cloud products, including Cloud Run functions.

## Key capabilities

<table>
<tbody>
<tr class="odd">
<td>Flexibility</td>
<td>The Firestore in Native Mode data model supports flexible, hierarchical data structures. Store your data in documents, organized into collections. Documents can contain complex nested objects in addition to subcollections.</td>
</tr>
<tr class="even">
<td>Expressive querying</td>
<td>In Firestore in Native Mode, you can use queries to retrieve individual, specific documents or to retrieve all the documents in a collection that match your query parameters. Your queries can include multiple, chained filters and combine filtering and sorting. They're also indexed by default, so query performance is proportional to the size of your result set, not your dataset.</td>
</tr>
<tr class="odd">
<td>Designed to scale</td>
<td>Firestore in Native Mode brings you automatic multi-region data replication, strongly-consistent queries, atomic batch operations, and transaction support.</td>
</tr>
<tr class="even">
<td>Realtime updates</td>
<td>Firestore in Native Mode uses data synchronization to update data on any connected device. However, it's also designed to make simple, one-time fetch queries efficiently.</td>
</tr>
<tr class="odd">
<td>Offline support</td>
<td>Firestore in Native Mode caches data that your app is actively using, so the app can write, read, listen to, and query data even if the device is offline. When the device comes back online, Firestore in Native Mode synchronizes any local changes back to Firestore in Native Mode.</td>
</tr>
</tbody>
</table>

## How does it work?

Firestore in Native Mode is a cloud-hosted, NoSQL database available in Node.js, Java, Python, Unity, C++ and Go client libraries, in addition to REST and RPC APIs. Apple, Android, and web apps can also access the database directly using the client libraries.

Following Firestore in Native Mode's NoSQL data model, you store data in documents that contain fields mapping to values. These documents are stored in collections, which are containers for your documents that you can use to organize your data and build queries. Documents support many different [data types](/firestore/docs/concepts/data-types) , from simple strings and numbers, to complex, nested objects. You can also create subcollections within documents and build hierarchical data structures that scale as your database grows. The Firestore in Native Mode [data model](/firestore/docs/data-model) supports whatever data structure works best for your app.

Additionally, querying in Firestore in Native Mode is expressive, efficient, and flexible. Create shallow queries to retrieve data at the document level without needing to retrieve the entire collection, or any nested subcollections. Add sorting, filtering, and limits to your queries or cursors to paginate your results. To keep data in your apps current, without retrieving your entire database each time an update happens, add realtime listeners. Adding realtime listeners to your app notifies you with a data snapshot whenever the data your client apps are listening to changes, retrieving only the new changes.

Protect access to your data in [Firestore in Native Mode with Identity and Access Management (IAM) for server-side](/firestore/docs/security/iam) languages. For Android, Apple platforms, and JavaScript protect your data with [Firebase Authentication and Firestore Security Rules](/firestore/docs/security/get-started) .

## What's next

  - [Get started](/firestore/docs/create-database-server-client-library) with Firestore in Native Mode — set up your database, then add data and start reading it.
  - Learn more about the Firestore in Native Mode [data model](/firestore/docs/data-model) .
  - [Create and manage databases](/firestore/docs/manage-databases) .
