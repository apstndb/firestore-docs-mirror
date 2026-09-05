---
name: documents/docs.cloud.google.com/firestore/native/docs/using-console
uri: https://docs.cloud.google.com/firestore/native/docs/using-console
title: Use Firestore Studio for Standard edition
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

# Use Firestore Studio for Standard edition

You can manage Firestore Standard edition through the following actions in the Google Cloud console:

  - View, query, add, edit, and delete data.
  - Manage indexes.
  - Manage security rules.

## View data

You can view all your Firestore Standard edition data in the Google Cloud console. From the Firestore Standard edition data viewer, click a document or collection to open the data nested within that item.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

### Open a specific path

To open a document or collection at a specific path, use the **Edit path** button create :

![Firestore Panel view in the console, with the Edit path button highlighted.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-edit-path.png)

### Configure panel settings

You can configure preferences for the data viewer in Firestore Studio. These preferences only affect your console view and don't change database metadata.

To configure panel settings:

1.  In the data viewer toolbar, click **Panel settings** settings .

2.  In the **Project panel settings** panel, configure the following options:
    
      - **Show non-existent parents** : Toggle whether to show non-existent parent documents in the documents list. This setting is enabled by default.
      - **Realtime updates enabled** : Toggle whether to receive live updates when documents change. This setting is enabled by default. Disabling real-time updates can help lower costs by reducing read operations.

3.  Click **Save** .

> **Note:** Panel settings apply to all databases in your project. Filtering data in the data viewer is supported only when real-time updates are enabled.

### Non-existent parent documents

A document can exist even if one or more of its parents don't exist. For example, the document at path `/mycoll/mydoc/mysubcoll/mysubdoc` can exist even if the parent document `/mycoll/mydoc` doesn't.

By default, the Firestore Standard edition data viewer displays non-existent parent documents as follows:

  - In a collection's list of documents, the document IDs of non-existent parent documents are *italicized* .
  - In a non-existent parent document's information panel, the data viewer points out that the document doesn't exist.

![Firestore data viewer in the console, showing a hierarchy of documents with a missing document highlighted and a warning message.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-non-existent-ancestor-document.png)

To hide non-existent parent documents from the collection documents list, disable **Show non-existent parents** in the [panel settings](https://docs.cloud.google.com/firestore/native/docs/using-console#configure-panel-settings) .

> **Warning:** Even though non-existent parent documents appear in the console, they don't appear in queries and snapshots. You must create the document to include it in query results.

### Filter data

You can filter documents in a collection based on field value and the `==` , `!-` , `>` , `>=` , `<` , `<=` , `in` , `not-in` , `array-contains` , `array-contains-any` conditions. For example, you can display only documents where the value of field `firstname` equals `Sam` .

> **Note:** Filtering data in the data viewer is supported only when **Realtime updates enabled** is selected in [panel settings](https://docs.cloud.google.com/firestore/native/docs/using-console#configure-panel-settings) .

To apply a collection filter:

1.  Click the filter button filter\_list next to a collection ID:
    
    ![Firestore Panel view in the console, with the Filter button highlighted.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-filter-documents.png)

2.  From the **Add filters** menu, select a document field, a filter condition, and a sort order.
    
    ![Firestore Add filters panel, showing options to filter by field, add conditions, change sort order, and preview query code.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-apply-filter.png)

3.  Click **Apply** .

To remove a collection filter, open the same menu and click **Clear filter** .

## Query data

You can query for documents in the ***Query Builder*** tab of the Firestore Studio page.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

4.  Click the **Query Builder** tab.

5.  Select a [query scope](https://docs.cloud.google.com/firestore/docs/concepts/index-overview#query_scopes) .
    
    Select ***Collection*** to query a single collection. In the text field, enter a path to a collection.
    
    Select ***Collection group*** to query all collections with the same ID. In the ***Collection group*** field, enter a collection group ID.
    
    The table will automatically display documents from the specified collection or collection group.

6.  Click ***Add to query*** to filter the returned set of documents. By default, the Query Builder adds a `WHERE` clause. You can modify this clause using the dropdowns and text fields or change to one of the other available clauses. To continue building more complex queries, click ***Add to query*** .
    
    To remove a query clause, click it's remove button delete . To remove all query clauses, click ***Clear*** .
    
    > **Note:** Queries must meet Firestore Standard edition requirements and limitations for queries. Otherwise, the query fails and the page returns an error that describes why the query failed.

7.  Click ***Run*** to retrieve results from your database.
    
    ![Query builder displaying results of a query.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-query-builder.png)

> **Tip:** Queries that you run are stored in your browser history. During the session, you can move forward and back within the browser to access recent queries. You can bookmark queries that you want to access often or to share with others.

### Query requirements and limitations

As you use the Query Builder, keep in mind the following requirements and limitations for queries.

  - All queries must be supported by one more indexes. If the database cannot find an index to support the query, it will return an error that contains a link to build the required index.
    
    ![Query builder with an error message to build the required index for the query.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-query-builder-index-error.png)

  - `ORDER BY` clauses must match the fields in the `WHERE` clauses and come in the same order. By default, results are ordered by document ID. If you filter by any other field with anything other than an equality ( `==` ), add an `ORDER BY` clause for that field.
    
    ![Query builder with a query clause and an order by clause on the same field.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-query-builder-order-by.png)

  - Range ( `<` , `<=` , `>` , `>=` ) and not equals ( `!=` , `not-in` ) query clauses must all filter on the same field.

For additional limitations, see [Query limitations](https://docs.cloud.google.com/firestore/docs/query-data/queries#query_limitations) .

## Manage data

In Firestore Standard edition, you store data in documents and organize your documents into collections. Before you start adding data, learn more about the [Firestore Standard edition data model](https://docs.cloud.google.com/firestore/native/docs/data-model) .

You can add, edit, and delete documents and collections from the Firebase console. To manage your data from the GCP console, go to the **Firestore Studio** page:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

> **Note:** Read, write, and delete operations performed in the console count towards your Firestore Standard edition usage.

### Add data

1.  Click **Start Collection** .
2.  Enter a collection ID. Enter a document ID. Firestore Standard edition will generate document ID, but you can overwrite for a specific document ID. Add fields for the data in your document.
3.  Click **Save** . Your new collection and document appear in the data viewer.
4.  To add more documents to the collection, click **Add Document** .

### Edit data

1.  Click on a collection to view its documents, then click on a document to view its fields and subcollections.
2.  Click on a field to edit its value. To add fields or subcollections to the selected document, click **Add Field** or **Start Collection** .

### Delete data

You can delete documents or collections from the data viewer.

> **Note:** In some cases, deleting a large number of documents might cause the data viewer to load slowly or to return a timeout error. This applies to delete operations performed through the data viewer and elsewhere.

To delete a collection:

1.  Select the collection you want to delete.
2.  Click the menu icon at the top of the documents column, then click **Delete collection** .

![Click Delete collection from the menu in the documents column](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-delete-collection.png)

To delete a document:

1.  Select the document you want to delete.
2.  Click the menu icon at the top of the document details column. Select **Delete document** or **Delete document fields** .

Deleting a document deletes all of the nested data in that document, including any subcollections.

Deleting a document's fields does not delete its subcollections. Although empty, the document still exists and can appear in query results.

![Click Delete document or Delete document fields from the context menu in the document details column](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-delete-document.png)

To delete a specific field in a document:

1.  Select the document to view its fields.
2.  Click the delete icon beside the field you want to delete.

![Click the delete icon to remove a field from a document](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-delete-field.png)

## Manage Firestore Security Rules

You can manage and deploy [Firestore Security Rules](https://docs.cloud.google.com/firestore/native/docs/security/get-started) directly in the Google Cloud console. The rules editor is available for Firestore in Native mode in both the Standard and Enterprise editions.

### Use the Google Cloud console

> **Note:** The Google Cloud console doesn't support deployment of Firestore Security Rules to the `(default)` database. To manage rules for the `(default)` database, use the [Firebase console](https://docs.cloud.google.com/firestore/native/docs/security/get-started#use-the-firebase-console) or the [Firebase CLI](https://docs.cloud.google.com/firestore/native/docs/security/get-started#use_the_cli) .

#### Required permissions

To manage and deploy security rules in the Google Cloud console, you need the following IAM permissions:

  - `firebaserules.releases.create`
  - `firebaserules.releases.delete`
  - `firebaserules.releases.update`
  - `firebaserules.rulesets.create`
  - `firebaserules.rulesets.delete`
  - `firebaserules.rulesets.list`
  - `firebaserules.rulesets.test` (required to use the rules simulator)

To deploy rules in the Google Cloud console:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click the ID of the database you want to manage.

3.  In the navigation menu, click **Security** .

4.  Click the **Firestore Rules** tab.

5.  In the rules editor, view your rules. To edit, click **New ruleset** or **Clone ruleset** , and then modify your rules.

6.  Click **Publish** to deploy your changes.

You can also view previous rulesets in the timeline and clone or restore them.

### Test rules with the rules simulator

You can test draft security rules against simulated requests before deploying them.

To test rules in the Google Cloud console:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click the ID of the database you want to test.

3.  In the navigation menu, click **Security** .

4.  Click the **Firestore Rules** tab, and then click the **Simulator** tab.

5.  Select the **Simulation type** ( **get** , **create** , **update** , or **delete** ).

6.  Enter the target document **Location** .

7.  (Optional) Configure mock document data or authentication parameters.

8.  Click **Run** to view evaluation results and line highlights in the rules editor.

### Enabling Firebase

To edit your `(default)` database's Firestore Security Rules using the Firebase console or Firebase CLI, you must enable Firebase for your Google Cloud project. If Firebase is not enabled, you can enable Firebase from the ***Security*** page in the Google Cloud console:

![If Firebase is not enabled in your project, the Enable Firebase SDK button appears.](https://docs.cloud.google.com/firestore/native/docs/images/firestore-console-rules-enable-firebase.png)

The Firestore Security Rules feature is closely integrated with Firebase Auth and the Firebase SDKs (Web, Android, Apple platforms). For more on Firebase and Firestore, see [getting started with Firebase](https://docs.cloud.google.com/firestore/docs/client/get-firebase) .

## Manage indexes

To create new indexes for your queries and manage existing indexes from the Firebase console, go to the **Databases & Storage** \> **Firestore** \> [**Indexes** tab](https://console.firebase.google.com/project/_/firestore/indexes) . Learn more about [managing indexes](https://docs.cloud.google.com/firestore/native/docs/query-data/indexing) .
