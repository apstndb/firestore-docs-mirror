This page describes how to edit an entity using the [Google Cloud console](https://console.cloud.google.com/) .

To learn how to modify an entity programmatically, see [Updating an entity](https://docs.cloud.google.com/datastore/docs/concepts/entities#updating_an_entity) .

## Before you begin

This page assumes you have already created an entity that is stored in Firestore in Datastore mode. You can create an entity through the Datastore API as described in [Getting Started with the Datastore API](https://docs.cloud.google.com/datastore/docs/datastore-api-tutorial) , or through the entity editor in the [Google Cloud console](https://console.cloud.google.com/) as described in the [Quickstart](https://docs.cloud.google.com/datastore/docs/store-query-data) .

## Select an entity to edit

1.  In the Google Cloud console, go to the **Databases** page.
    
    [Go to Databases](https://console.cloud.google.com/datastore/databases)

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Datastore Studio** .

4.  Find the entity you want to edit by specifying the namespace, kind, and/or filters for property values. To learn how, see [Run a query](https://docs.cloud.google.com/datastore/docs/store-query-data#run_a_query) .

5.  Click on the **Name/ID** of an entity. Your screen should look similar to the following:
    
    ![The entity overview page showing information about an entity.](https://docs.cloud.google.com/static/datastore/images/edit_entity.png)

### Edit a property

1.  Open the **Edit Entity** page for an entity. Under **Properties** , click **Edit** edit for the property you want to edit.
    
    **Tip:** You can filter the properties table. Click **Filter properties** at the top of the table.

2.  In the **Edit property** pane, modify the property's **Name** , **Type** , or **Value** . You can also modify whether the property is indexed. To learn about the impact of including or excluding a property from indexes, see [Excluded properties](https://docs.cloud.google.com/datastore/docs/concepts/indexes#unindexed_properties) .
    
    ![Click the edit button to edit a property.](https://docs.cloud.google.com/static/datastore/images/edit_property.png)

3.  Click **Done** . The **Edit property** pane closes and the properties table now shows your changes. Changes are not committed to the database until you click **Save** . The properties table highlights uncommitted changes with a blue dot next to the property name.

4.  Make additional changes to other properties. When you complete your edits, click **Save** to commit your changes to the database.
    
    The console commits your changes and takes you back to the **Datastore Studio** page.

### Add a property

1.  Open the **Edit Entity** page for an entity. Click **Add property** .

2.  In the **Add a property** pane, specify a name for the property.

3.  Select a type for the property's data type.

4.  Specify a value for the property.

5.  Specify whether the property is indexed. To learn about the impact of including or excluding a property from indexes, see [Excluded properties](https://docs.cloud.google.com/datastore/docs/concepts/indexes#unindexed_properties) .
    
    ![The add-a-property pane.](https://docs.cloud.google.com/static/datastore/images/add_property.png)

6.  Click **Add** . The **Add a property** pane closes and the properties table now shows your changes. Changes are not committed to the database until you click **Save** . The properties table highlights uncommitted changes with a blue dot next to the property name.

7.  Make additional changes to other properties. When you complete your edits, click **Save** to commit your changes to the database.
    
    The console commits your changes and takes you back to the **Datastore Studio** page.

### Delete a property

1.  Open the **Edit Entity** page for an entity. Under **Properties** , click **Delete** delete for the property you want to delete.
    
    ![The delete button within the property table.](https://docs.cloud.google.com/static/datastore/images/delete_property.png)

2.  The properties table now shows your changes. Changes are not committed to the database until you click **Save** . The properties table highlights uncommitted property deletions with crossed out names and property values.
    
    You can undo an uncommitted deletion by clicking **Restore** in the property's table row.

3.  Make additional changes to other properties. When you complete your edits, click **Save** to commit your changes to the database.

## Complex properties

The entity editor supports properties with complex types such as `Array` and `Embedded entity` .

### Array properties

When you add or modify the value of an `Array` property, provide a value in JSON format.

![An example of valid JSON for an array property.](https://docs.cloud.google.com/static/datastore/images/array_property.png)

If you enter invalid JSON for the **Value** field you will receive an error message. You will not be able to add the property if the JSON is invalid.

### Embedded entity properties

When you add or modify the value of an `Embedded entity` property, provide a value in JSON format.

![An example of valid JSON for an embedded entity property](https://docs.cloud.google.com/static/datastore/images/embedded_entity_property.png)

If you enter invalid JSON for the **Value** field you will receive an error message. You will not be able to add the property if the JSON is invalid.

## What's next

  - Learn about [best practices for entities](https://docs.cloud.google.com/datastore/docs/best-practices#entities) .
