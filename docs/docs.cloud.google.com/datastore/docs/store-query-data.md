# Store and query data in Firestore in Datastore mode

This page shows you how to store and query data in Firestore in Datastore mode using the Google Cloud console.

## Before you begin

  - Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

  - In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

  - In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

  - If you are **not** the project owner, your account requires the following permissions to complete this quickstart:
    
      - Your account requires the [**Datastore Owner** role](/iam/docs/understanding-roles#cloud_datastore_roles) which contains the `  datastore.databases.create  ` permission needed to create a Datastore mode instance.
      - Datastore mode requires an active App Engine application. If the project doesn't have an application, this quickstart creates one for you. In that case, you require the `  appengine.applications.create  ` permission. The project owner can assign this permission with an [IAM custom role](/iam/docs/creating-custom-roles) .

## Create a database

1.  To create a new database instance, open the Datastore section in the Google Cloud console:  

2.  Select a database mode.
    
    When you create a new Firestore database, you have the option to use Firestore in either Native Mode or Datastore mode. You can't use both modes in the same project.
    
    Select from one of the database options:
    
      - **Firestore in Native Mode**
        
        Recommended for mobile and web apps. To get started with Firestore, continue in the [Firestore Quickstart](/firestore/docs/quickstart) .
    
      - **Firestore in Datastore Mode**
        
        Recommended for app architectures with backend servers.
    
    For more guidance on selecting a database mode and for a feature-by-feature comparison, see [choosing between Native Mode and Datastore Mode](/datastore/docs/firestore-or-datastore) .

3.  Select a database location. Datastore mode supports multi-region and regional locations.
    
    A multi-region location maximizes availability and durability. Regional locations offer lower write latency. To learn more about location types, see [Datastore mode locations](/datastore/docs/locations) . The location applies to both Datastore mode databases and App Engine apps for your Google Cloud project.
    
    **Warning:** Once you create your database, you cannot change the location.
    
    Click **Create database** . After your database finishes initializing, the Google Cloud console directs you to the Datastore Entities page.

## Store data

1.  Go to the Datastore Entities page in the Google Cloud console.
    
    This page lets you store, query, update, and delete data.

2.  Click **Create entity** .

3.  On the **Create an entity** page, use `  [default]  ` for **Namespace** .

4.  Type `  Task  ` in the **Kind** field. Leave **Key identifier** set to the default value of `  Numeric ID (auto-generated)  ` .

5.  Under **Properties** , use the **Add property** button to add these properties:
    
    <table>
    <thead>
    <tr class="header">
    <th>Name</th>
    <th>Type</th>
    <th>Value</th>
    <th>Indexed</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>description</td>
    <td>String</td>
    <td>Learn about Datastore.</td>
    <td></td>
    </tr>
    <tr class="even">
    <td>created</td>
    <td>Date and time</td>
    <td>(today's date)</td>
    <td>✓</td>
    </tr>
    <tr class="odd">
    <td>done</td>
    <td>Boolean</td>
    <td>False</td>
    <td>✓</td>
    </tr>
    </tbody>
    </table>
    
    Your creation page should now look like this:

6.  Click **Create** . The console displays the `  Task  ` entity that you just created.

You just stored data in your database\!

## Run a query

Datastore mode databases support querying data by kind or by Google Query Language (GQL). The instructions below walk you through using both to query your database.

### Run kind queries

1.  Click **Query by kind** .
2.  Select `  Task  ` as the kind.

The query results show the `  Task  ` entity that you created.

Next, add a query clause to restrict the results to entities that meet specific criteria:

1.  Click **Add query clause** .
2.  In the dropdown lists, select `  WHERE  ` , `  done  ` , `  ==  ` , **boolean** , and **false** .
3.  Click **Run** . The results show the `  Task  ` entity that you created since its `  done  ` value is `  false  ` .
4.  Now change the query clause to `  WHERE  ` , `  done  ` , `  ==  ` , **boolean** , and **true** . Click **Run** . The results do not include the `  Task  ` entity that you created, because its `  done  ` value is not `  true  ` .

### Run GQL queries

1.  Click **Query by GQL** .
2.  Enter `  SELECT * FROM Task  ` as the query. Note that `  Task  ` is case sensitive.
3.  Click **Run query** .

The query results show the `  Task  ` entity that you created.

**Tip**

The GQL query editor supports autocompletion for kinds: When you need to type a kind name, press Ctrl+Space to see a list of the available kinds. Up to 300 alphabetically sorted kinds can appear in the list. For better matches of kinds, type one or more characters.

Add a query filter to restrict the results to entities that meet specific criteria:

1.  Run a query such as `  SELECT * FROM Task WHERE done=false  ` . Note that `  Task  ` and `  done  ` are case sensitive. The results show the `  Task  ` entity that you created, since its `  done  ` value is `  false  ` .
2.  Now run a query such as `  SELECT * FROM Task WHERE done=true  ` . The results do not include the `  Task  ` entity that you created, because its `  done  ` value is not `  true  ` .

## Clean up

1.  Click **Query by kind** and ensure `  Task  ` is the selected kind.
2.  Click **Clear** to remove any query clauses.
3.  Select the `  Task  ` entity that you created.
4.  Click **Delete** , and then confirm you want to delete the `  Task  ` entity. Depending on the size of the browser window, **Delete** might be under the more\_vert **More actions** menu. Once deleted, the entity is permanently removed from your database.

That's it, you completed this quickstart\!

## What's next

  - Learn more about [Datastore Queries](/datastore/docs/concepts/queries) .
  - Learn more about [Datastore mode](/datastore/docs) databases.
