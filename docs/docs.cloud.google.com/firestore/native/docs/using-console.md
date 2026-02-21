# Use Firestore Studio for Standard edition

You can manage Firestore Standard edition through the following actions in the Google Cloud console:

  - View, query, add, edit, and delete data.
  - Manage indexes.

**Note:** To manage your Security Rules, use the [Firebase console](https://firebase.google.com/docs/firestore/using-console) .

## View data

You can view all your Firestore Standard edition data in the Google Cloud console. From the Firestore Standard edition data viewer, click on a document or collection to open the data nested within that item.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

### Open a specific path

To open a document or collection at a specific path, use the **Edit path** button create :

### Non-existent ancestor documents

A document can exist even if one or more its ancestors don't exist. For example, the document at path `  /mycoll/mydoc/mysubcoll/mysubdoc  ` can exist even if the ancestor document `  /mycoll/mydoc  ` does not. The Firestore Standard edition data viewer displays non-existent ancestor documents as follows:

  - In a collection's list of documents, the document IDs of non-existent ancestor documents are *italicized* .
  - In a non-existent ancestor document's information panel, the data viewer points out that the document does not exist.

**Warning:** Even though non-existent ancestor documents appear in the console, they do not appear in queries and snapshots. You must create the document to include it in query results.

### Filter data

You can filter documents in a collection based on field value and the `  ==  ` , `  !-  ` , `  >  ` , `  >=  ` , `  <  ` , `  <=  ` , `  in  ` , `  not-in  ` , `  array-contains  ` , `  array-contains-any  ` conditions. For example, you can display only documents where the value of field `  firstname  ` equals `  Sam  ` . To apply a collection filter:

1.  Click the filter button filter\_list next to a collection ID:

2.  From the **Add filters** menu, select a document field, a filter condition, and a sort order.

3.  Click **Apply** .

To remove a collection filter, open the same menu and click **Clear filter** .

## Query data

You can query for documents in the ***Query Builder*** tab of the Firestore Studio page.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

4.  Click the **Query Builder** tab.

5.  Select a [query scope](/firestore/docs/concepts/index-overview#query_scopes) .
    
    Select ***Collection*** to query a single collection. In the text field, enter a path to a collection.
    
    Select ***Collection group*** to query all collections with the same ID. In the ***Collection group*** field, enter a collection group ID.
    
    The table will automatically display documents from the specified collection or collection group.

6.  Click ***Add to query*** to filter the returned set of documents. By default, the Query Builder adds a `  WHERE  ` clause. You can modify this clause using the dropdowns and text fields or change to one of the other available clauses. To continue building more complex queries, click ***Add to query*** .
    
    To remove a query clause, click it's remove button delete . To remove all query clauses, click ***Clear*** .
    
    **Note:** Queries must meet Firestore Standard edition requirements and limitations for queries. Otherwise, the query fails and the page returns an error that describes why the query failed.

7.  Click ***Run*** to retrieve results from your database.

**Tip:** Queries that you run are stored in your browser history. During the session, you can move forward and back within the browser to access recent queries. You can bookmark queries that you want to access often or to share with others.

### Query requirements and limitations

As you use the Query Builder, keep in mind the following requirements and limitations for queries.

  - All queries must be supported by one more indexes. If the database cannot find an index to support the query, it will return an error that contains a link to build the required index.

  - `  ORDER BY  ` clauses must match the fields in the `  WHERE  ` clauses and come in the same order. By default, results are ordered by document ID. If you filter by any other field with anything other than an equality ( `  ==  ` ), add an `  ORDER BY  ` clause for that field.

  - Range ( `  <  ` , `  <=  ` , `  >  ` , `  >=  ` ) and not equals ( `  !=  ` , `  not-in  ` ) query clauses must all filter on the same field.

For additional limitations, see [Query limitations](/firestore/docs/query-data/queries#query_limitations) .

## Manage data

In Firestore Standard edition, you store data in documents and organize your documents into collections. Before you start adding data, learn more about the [Firestore Standard edition data model](./data-model) .

You can add, edit, and delete documents and collections from the Firebase console. To manage your data from the GCP console, go to the **Firestore Studio** page:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Firestore Studio** .

**Note:** Read, write, and delete operations performed in the console count towards your Firestore Standard edition usage.

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

**Note:** In some cases, deleting a large number of documents might cause the data viewer to load slowly or to return a timeout error. This applies to delete operations performed through the data viewer and elsewhere.

To delete a collection:

1.  Select the collection you want to delete.
2.  Click the menu icon at the top of the documents column, then click **Delete collection** .

To delete a document:

1.  Select the document you want to delete.
2.  Click the menu icon at the top of the document details column. Select **Delete document** or **Delete document fields** .

Deleting a document deletes all of the nested data in that document, including any subcollections.

Deleting a document's fields does not delete its subcollections. Although empty, the document still exists and can appear in query results.

To delete a specific field in a document:

1.  Select the document to view its fields.
2.  Click the delete icon beside the field you want to delete.

## Manage Firestore Security Rules

You can view your [Firestore Security Rules](/firestore/docs/security/get-started) from the Google Cloud console. To edit or delete your ruleset, enable Firebase, and [use the Firebase CLI or Firebase console](/firestore/docs/security/get-started#deploying_rules) .

### Enabling Firebase

To edit your Firestore Security Rules, you must enable Firebase for your Google Cloud project. If Firebase is not enabled, you can enable Firebase from the ***Security Rules*** page:

The Firestore Security Rules feature is closely integrated with Firebase Auth and the Firebase SDKs (Web, Android, Apple platforms). For more on Firebase and Firestore, see [getting started with Firebase](/firestore/docs/client/get-firebase) .

### View Security Rules

To view your Firestore Security Rules from the Google Cloud console, go to the ***Security Rules*** page:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Security Rules** .

### Edit Security Rules

To edit or delete your Firestore Security Rules, [use the Firebase CLI or Firebase console](/firestore/docs/security/get-started#deploying_rules) . In the Firebase console, go to the [**Rules** tab](https://console.firebase.google.com/project/_/firestore/rules) in the **Firestore in Native Mode** section. Learn more about [setting up and customizing rules](./security/get-started) .

## Manage indexes

To create new indexes for your queries and manage existing indexes from the Firebase console, go to the [**Indexes** tab](https://console.firebase.google.com/project/_/firestore/indexes) in the **Firestore in Native Mode** section. Learn more about [managing indexes](./query-data/indexing) .
