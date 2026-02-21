# Connect with mongosh

Learn how to create a Firestore with MongoDB compatibility database and connect to it with the `  mongosh  ` tool.

## Before you begin

1.  In the Google Cloud console, go to the project selector page.

2.  Select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  Make sure that you have the following role or roles on the project: Cloud Datastore Owner
    
    #### Check for the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  In the **Principal** column, find all rows that identify you or a group that you're included in. To learn which groups you're included in, contact your administrator.
    
    4.  For all rows that specify or include you, check the **Role** column to see whether the list of roles includes the required roles.
    
    #### Grant the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  Click person\_add **Grant access** .
    
    4.  In the **New principals** field, enter your user identifier. This is typically the email address for a Google Account.
    
    5.  Click **Select a role** , then search for the role.
    
    6.  To grant additional roles, click add **Add another role** and add each additional role.
    
    7.  Click **Save** .

5.  [Install the `  mongosh  ` tool](https://www.mongodb.com/docs/mongodb-shell/install/)

## Create a Firestore with MongoDB compatibility database and retrieve the connection string

In the Google Cloud console, create a new Firestore Enterprise edition database. Firestore with MongoDB compatibility requires Firestore Enterprise edition:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Click **Create a Firestore Database** .

3.  Enter a database ID.

4.  Select Enterprise Edition.

5.  Select a location for your database.

6.  Click **Create Database** .
    
    When the database completes initialization, the console opens the **Firestore Studio** for your database.

7.  In the **Connect to Firestore using an external MongoDB tool** section, copy the connection string.

The connection string depends on the UID of the database (system-generated) and the location of database:

``` text
UID.LOCATION.firestore.goog
```

## Create a user for SCRAM authentication

In the Google Cloud console, create a new database user and assign the user Identity and Access Management permissions.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the database from the list of databases.

3.  In the navigation menu, click **Security** .

4.  Click **Add User** .

5.  Enter a username.

6.  Select an Identity and Access Management role for the user.

7.  Click create. The database creates a user and shows you the user's generated password. **Copy and save this password. You will not be able to retrieve this password later** .

## Connect using `     mongosh    `

Use the connection string, username, and password to connect to your database, run `  mongosh  ` locally with the following configuration options.

``` text
mongosh 'mongodb://USERNAME:PASSWORD@CONNECTION_STRING:443/DATABASE_ID?loadBalanced=true&authMechanism=SCRAM-SHA-256&tls=true&retryWrites=false'
```

Replace the following:

  - USERNAME : the name of the database user you created.
  - PASSWORD : the generated password for the database user you created.
  - CONNECTION\_STRING : the database connection string.
  - DATABASE\_ID : a database ID

Once connected, you can create and read data, for example:

``` text
db.pages.insertOne({ message: "Hello World!"})
db.pages.find({})
exit
```

## What's next

  - [See a list of supported features](/firestore/mongodb-compatibility/docs/supported-data-types-drivers)
  - [Learn about behavior differences in Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/behavior-differences)
  - [Learn about additional authentication methods](/firestore/mongodb-compatibility/docs/connect)
