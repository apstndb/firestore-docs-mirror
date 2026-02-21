This page describes how to view and manage the entities, indexes, and statistics for the data your application stores in your database.

## Viewing Datastore statistics

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Datastore Studio** to view data for the entities in your application, as well as statistics for the built-in and composite indexes.

The dashboard should look like:

For more information about the statistics on this page, see [Viewing Statistics in the Console](/datastore/docs/console/datastore-statistics) .

## Viewing indexes

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Indexes** to view a table of your application's indexes.

For each index, you should see its status, such as whether it is ready to serve your application. You should also see the amount of storage space used by the index and the number of entries in each index.

## Viewing entities

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Datastore Studio** to view the entities that your application stored in your database.

You should see:

You can also create, update, delete, and query entities on this page. Learn how in the [Quickstart](/datastore/docs/store-query-data) .

**Note:** While individual entities are removed almost immediately, a namespace container may remain visible for several days to a week after the final entity within it is removed.

## What's next?

  - Get details about [Statistics in the Console](/datastore/docs/console/datastore-statistics) .
