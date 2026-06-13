---
name: documents/docs.cloud.google.com/firestore/native/docs/knowledge-catalog
uri: https://docs.cloud.google.com/firestore/native/docs/knowledge-catalog
title: View Knowledge Catalog insights
description: View Knowledge Catalog insights for Firestore databases
data_source: docs.cloud.google.com
---

# View Knowledge Catalog insights

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can search for and manage your Firestore resources using Knowledge Catalog, which is a platform for storing, managing, and accessing your metadata. You can use Knowledge Catalog to analyze your Firestore metadata and help with tasks like:

  - Analysis, including dependencies and suitability for a use case
  - Change management
  - Schema evolution

Knowledge Catalog is enabled by default on new and existing Firestore databases, and automatically retrieves the following metadata:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Resource</th>
<th>Type</th>
<th>Fields</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Database</td>
<td>Control plane</td>
<td><ul>
<li>Edition</li>
<li>Mode(s)</li>
<li>Location (including multi-regions)</li>
<li>Project ID</li>
<li>Database name</li>
<li>Created time</li>
</ul></td>
</tr>
<tr class="even">
<td>Database schema</td>
<td>Data plane</td>
<td><ul>
<li>Name</li>
<li>Collection</li>
<li>Field - Data Type(s)</li>
<li>Schema</li>
</ul></td>
</tr>
</tbody>
</table>

## Before you begin

To use Knowledge Catalog insights with Firestore, you must first have a Firestore database. For more information, see [Create and manage databases](https://docs.cloud.google.com/firestore/native/docs/manage-databases) .

### Required roles for accessing search results

To search for and view Firestore metadata in Knowledge Catalog, principals must have permissions to view Firestore resources, including the `dataplex.projects.search` permission.

To grant principals - such as users, groups, or service accounts - these permissions, assign them the **Cloud Datastore Viewer** ( [`roles/datastore.viewer`](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore) ) IAM role on the project that contains the Firestore resources.

Knowledge Catalog operation

Firestore resource

Roles or permissions required

Search for Firestore resources

Database

`datastore.databases.getMetadata`

Database schema

`datastore.schemas.get`

For more information about granting roles, see [Manage access](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) . For more information about Firestore IAM roles, see [Firestore roles and permissions](https://docs.cloud.google.com/iam/docs/roles-permissions/firestore) .

### Required roles for searching entries

To search for entries, you need at least one of the following [IAM roles](https://docs.cloud.google.com/dataplex/docs/iam-roles#predefined-roles) on the project that is used for search:

  - Dataplex Catalog Admin ( [`roles/dataplex.catalogAdmin`](https://docs.cloud.google.com/dataplex/docs/iam-roles#dataplex.catalogAdmin) )
  - Dataplex Catalog Editor ( [`roles/dataplex.catalogEditor`](https://docs.cloud.google.com/dataplex/docs/iam-roles#dataplex.catalogEditor) )
  - Dataplex Catalog Viewer ( [`roles/dataplex.catalogViewer`](https://docs.cloud.google.com/dataplex/docs/iam-roles#dataplex.catalogViewer) )

Permissions on search results are checked independently of the selected project. For more information, see [Search for data assets with Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-assets#required-roles) .

## Types of metadata discovery

Knowledge Catalog metadata discovery is an automated process that scans connected data sources - like Firestore - to identify data assets (like collections and databases) and extract their technical metadata like schemas, descriptions, and locations into the Knowledge Catalog catalog. This process runs periodically to keep the catalog synchronized with source systems.

> **Important:** Database and collection group IDs must follow the following naming convention in order to appear in Knowledge Catalog: Must contain only letters, numbers, or characters in `""'-._~%%!$&'()*+,;=@/'` , and cannot be in UUID format or empty. IDs cannot start with a slash ( `/` ) or contain two slashes in a row ( `//` ).

### Keyword and natural language search

Knowledge Catalog supports keyword and natural language searches.

  - Keyword search lets you find resources using specific keywords, filters, and a defined syntax. For example, you might enter `system=Firestore AND type=Database` to view all Firestore databases.
  - Natural language search (Preview) uses AI to understand semantic queries. It lets you find resources using everyday language, eliminating the need for complex syntax. For example, you can enter queries like `List all Firestore databases related to sales` .

For more information, see [Search syntax for Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-syntax) .

### Example: Discover a Firestore collection group schema

To understand the metadata discovery process, consider a Firestore database named `user-firestore-database` . In this database, you have a collection group schema named `user-schema` .

After discovery is complete, you can search for these assets - `user-firestore-database` and `user-schema` - in the Knowledge Catalog page of the Google Cloud console or by using the Knowledge Catalog API. You can then view details about the assets and enrich them with additional business or operational metadata.

## Enrich metadata using aspects

*Aspect types* are reusable resources that you can use as templates for aspects. Aspect types help you avoid duplication of work and incomplete aspects. You can use Knowledge Catalog to create the aspect types that you need.

After you create custom aspect types, you can attach aspects to your Firestore resources. Attaching aspects to your resources lets you do the following:

  - Add business metadata to the assets
  - Search for assets by business metadata and other custom metadata

To learn more about creating aspect types and attaching aspects to Firestore, see [Manage aspects and enrich metadata](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata) .

## Search for Firestore assets

Use the Knowledge Catalog search page in the Google Cloud console to search for Firestore assets.

1.  Go to the Knowledge Catalog **Search** page.

2.  In the **Filters** panel, click **Systems** , and then select **Firestore** .

3.  Optional. In **Type aliases** , you can filter the search results to a specific type of Firestore asset by the selecting one or more of the following type alias:
    
      - Database
      - Database schema
      - Other

### Use queries to perform keyword search

You can use the search field in Knowledge Catalog to perform keyword search queries. For example, you might enter `system=Firestore AND type=Database` to view all Firestore databases.

For more information, see [Search syntax for Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-syntax) .

To view all Firestore assets, enter `system=Firestore` . You can enter specific keywords. For example, to view all Firestore databases:

    system=Firestore AND type=Database

You can also use parentheses and the logical operators `AND` and `OR` for complex expressions. To learn more about the expressions that you can use in the search field, see [Search syntax for Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-syntax) .

You can directly enter search queries for specific Firestore assets into the search field. The format of the query string is as follows:

    type="projects/dataplex-types/locations/global/entryTypes/QUERY_STRING"

Replace the following:

  - `  QUERY_STRING  ` : use the following list to identify a query string based on the type of Firestore asset that you want to query:
    
      - `firestore-database`
      - `firestore-schema`

An example query might look like the following:

    type="projects/1234567890/locations/global/entryTypes/firestore-schema"

## Search by aspect type

Knowledge Catalog includes a few built-in aspect types that you can use to perform searches.

To search by aspect type, follow these steps:

1.  In the **Aspects** panel, click the **Add more aspect types** menu.
2.  Enter `Firestore` , then select one or more of the following aspect types to limit the search results to that type.
      - Firestore Database
      - Firestore Schema
3.  Click **OK** .
4.  In the results table, click the name of the asset to view the metadata for that asset.
5.  Optional: Enhance or view your assets. You can do any of the following:
      - To add a rich text description of the asset, in **Overview** , click **Add** .
      - To attach an aspect to the asset, in **Aspects** , click **Add** .
      - To view member databases for an instance, click the **Entry List** tab, and then click **Show all children entries in search** .
      - In **Entry details** , view the full details of the asset. Click the entry name to drill down to additional entries.

### Natural Language search in Firestore

Natural language search (Preview) uses AI to understand semantic queries. It lets you find resources using everyday language, eliminating the need for complex syntax. For example, you can enter queries like `List all Firestore collections related to sales` .

For more information, see [Search syntax for Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-syntax) .

### Syntax search in Firestore

Keyword search lets you find resources using specific keywords, filters, and a defined syntax. For example, you might enter `system=Firestore AND type=Database` to view all Firestore databases.

For more information, see [Search syntax for Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/search-syntax) .

### Example workflow: Drill down from database to schema

To drill down from a database to a schema, follow these steps:

1.  Go to the Knowledge Catalog **Search** page.

2.  In the **Filters panel** , select **Systems** and then **Firestore** . Alternatively, enter `system=Firestore` in the search field.

3.  Select a database.

4.  On the **Firestore details** page, click the **Entry list** tab, and then click **Show all children entries in search** .
    
    > **Note:** If there is no **Entry list** tab, then return to the **Search** page and choose a different database.

5.  On the **Firestore database details** page, click the **Entry list** tab, and then click **Show all children entries in search** . Knowledge Catalog displays the collection groups in the database.

6.  Select a collection group name, and then on the **Collection group details** page, click **Schema** to view the schema.

7.  Optional: To add an aspect type to a database, click the **Add aspect** button.

## Pricing

There is no charge for storing Firestore technical metadata in Knowledge Catalog. Standard Knowledge Catalog pricing applies for API calls and additional business metadata enrichment. For more information, see the [Knowledge Catalog pricing page](https://docs.cloud.google.com/dataplex/pricing) .

## Limitations

  - Query results are truncated after 10,000 collection groups have been ingested.
  - During batch ingestion, it can take up to 48 hours for updates to your database to be reflected in Knowledge Catalog.
  - During live ingestion, it can take up to 5 minutes for updates to your database to be reflected in Knowledge Catalog.
  - Collection groups aren't updated during live ingestion.
  - Collection group schemas are updated during live ingestion, however, this update covers only the first 100 top-level primitive fields in alphabetical order. The remaining schema information is updated 24 to 48 hours following live ingestion.
  - The extraction process may take several minutes.

## What's next

  - [About data catalog management in Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/catalog-overview)
  - [Knowledge Catalog Identity and Access Management roles](https://docs.cloud.google.com/dataplex/docs/iam-roles)
