[VPC Service Controls](https://cloud.google.com/vpc-service-controls/) lets organizations define a perimeter around Google Cloud resources to mitigate data exfiltration risks. With VPC Service Controls, you create perimeters that protect the resources and data of services that you explicitly specify.

## Bundled Firestore services

The following APIs are bundled together in VPC Service Controls:

  - `  firestore.googleapis.com  `
  - `  datastore.googleapis.com  `
  - `  firestorekeyvisualizer.googleapis.com  `

When you restrict the `  firestore.googleapis.com  ` service in a perimeter, the perimeter also restricts the `  datastore.googleapis.com  ` and `  firestorekeyvisualizer.googleapis.com  ` services.

### Restrict the datastore.googleapis.com service

The `  datastore.googleapis.com  ` service is bundled under the `  firestore.googleapis.com  ` service. To restrict the `  datastore.googleapis.com  ` service, you must restrict the `  firestore.googleapis.com  ` service as follows:

  - When creating a service perimeter using the Google Cloud console, add Firestore as the restricted service.

  - When creating a service perimeter using the Google Cloud CLI, use `  firestore.googleapis.com  ` instead of `  datastore.googleapis.com  ` .
    
    ``` text
    --perimeter-restricted-services=firestore.googleapis.com
    ```

### App Engine legacy bundled services for Datastore

[App Engine legacy bundled services for Datastore](https://cloud.google.com/appengine/docs/standard/python/bundled-services-overview) don't support service perimeters. Protecting the Datastore service with a service perimeter blocks traffic from App Engine legacy bundled services. Legacy bundled services include:

  - [Java 8 Datastore with App Engine APIs](https://cloud.google.com/appengine/docs/standard/java/datastore)
  - [Python 2 NDB client library for Datastore](https://cloud.google.com/appengine/docs/standard/python/ndb/creating-entities)
  - [Go 1.11 Datastore with App Engine APIs](https://cloud.google.com/appengine/docs/standard/go111/datastore)

## Egress protection on import and export operations

Firestore in Datastore mode supports VPC Service Controls but requires additional configuration to get full egress protection on import and export operations. You must use the Firestore service agent to authorize import and export operations instead of the default App Engine service account. Use the following instructions to view and configure the authorization account for import and export operations.

### Firestore service agent

Firestore uses a Firestore service agent to authorize import and export operations instead of using the App Engine service account. The service agent and service account use the following naming conventions:

  - Firestore service agent  
    `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  `

Firestore previously used the App Engine default service account instead of the Firestore service agent. If your database still uses the App Engine service account to import or export data, we recommend that you follow the instructions in this section to migrate to using the Firestore service agent.

  - App Engine service account  
    `  PROJECT_ID @appspot.gserviceaccount.com  `

The Firestore service agent is preferable because it is specific to Firestore. The App Engine service account is shared by more than one service.

**Note:** If you use VPC Service Controls, you must use the Firestore service agent to fully protect import and export operations. VPC Service Controls is not compatible with the App Engine service account.

### View authorization account

You can view which account your import and export operations use to authorize requests from the **Import/Export** page in the Google Cloud console. You can also view if your database already uses the Firestore service agent.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  View the authorization account next to the **Import/Export jobs run as** label.

If your project does not use the Firestore service agent, you can migrate to the Firestore service agent using either of these techniques:

  - [Migrate a project by checking and updating Cloud Storage bucket permissions (recommended)](#migrate-by-project) .
  - [Add an organization-wide policy constraint](#migrate-by-org-policy) that affects all projects within the organization.

The first of these techniques is preferable because it localizes the scope of effect to a single Datastore mode project. The second technique is not preferred because it doesn't migrate existing Cloud Storage bucket permissions. It does, however, offer security compliance at the organization level.

### Migrate by checking and updating Cloud Storage bucket permissions

The migration process has two steps:

1.  Update Cloud Storage bucket permissions. See the following section for details.
2.  Confirm migration to the Firestore service agent.

#### Service agent bucket permissions

For any export or import operations that use a Cloud Storage bucket in *another* project, you must grant the Firestore service agent permissions for that bucket. For example, operations that move data to another project need to access a bucket in that other project. Otherwise, these operations fail after migrating to the Firestore service agent.

Import and export workflows that stay within the same project do not require changes to permissions. The Firestore service agent can access buckets in the same project by default.

Update the permissions for Cloud Storage buckets from other projects to give access to the `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  ` service agent. Grant the service agent the `  Firestore Service Agent  ` role.

The `  Firestore Service Agent  ` role grants read and write permissions for a Cloud Storage bucket. If you need to grant only read or only write permissions, use a [custom role](https://cloud.google.com/iam/docs/creating-custom-roles) .

The migration process described in the following section helps you identify Cloud Storage buckets that might require permission updates.

#### Migrate a project to the Firestore Service Agent

Complete the following steps to migrate from the App Engine service account to the Firestore service agent. Once completed, the migration can't be undone.

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  If your project has not yet migrated to the Firestore service agent, you see a banner describing the migration and a **Check Bucket Status** button. The next step helps you identify and fix potential permission errors.
    
    Click **Check Bucket Status** .
    
    A menu appears with the option to complete your migration and a list of Cloud Storage buckets. It may take a few minutes for the list to finish loading.
    
    This list includes buckets which were recently used in import and export operations, but do not currently give read and write permissions to the Datastore mode service agent.

5.  Take note of the principal name of your project's Datastore mode service agent. The service agent name appears under the **Service agent to give access to** label.

6.  For any bucket in the list that you will use for future import or export operations, complete the following steps:
    
    1.  In this bucket's table row, click **Fix** . This opens that bucket's permissions page in a new tab.
    
    2.  Click **Add** .
    
    3.  In the **New principals** field, enter the name of your Firestore service agent.
    
    4.  In the **Select a role** field, select **Service Agents \> Firestore Service Agent** .
    
    5.  Click **Save** .
    
    6.  Return to the tab with the Datastore mode Import/Export page.
    
    7.  Repeat these steps for other buckets in the list. Make sure to view all the pages of the list.

7.  Click **Migrate to Firestore Service Agent** . If you still have buckets with failed permission checks, you need to confirm your migration by clicking **Migrate** .
    
    An alert informs you when your migration completes. Migration can't be undone.

#### View migration status

To verify your project's migration status:

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Import/Export** .

4.  Look for the principal next to the **Import/Export jobs run as** label.
    
    If the principal is `  service- PROJECT_NUMBER @gcp-sa-firestore.iam.gserviceaccount.com  ` , then your project has already migrated to the Firestore service agent. The migration can't be undone.
    
    If the project has not been migrated, a banner appears at the top of the page with a **Check Bucket Status** button. See [Migrate to the Firestore service agent](#migrate_to_the_firestore_service_agent) to complete the migration.

### Add an organization-wide policy constraint

  - Set the following constraint in your organization's policy:
    
    **Require Firestore Service Agent for import/export** ( `  firestore.requireP4SAforImportExport  ` ).
    
    This constraint requires import and export operations to use the Firestore service agent to authorize requests. To set this constraint, see [Creating and managing organization policies](/resource-manager/docs/organization-policy/creating-managing-policies#creating_and_editing_policies) .

Applying this organizational policy constraint does not automatically grant the appropriate Cloud Storage bucket permissions for the Firestore service agent.

If the constraint creates permission errors for any import or export workflows, you can disable it to go back to using default service account. After you [check and update Cloud Storage bucket permissions](#migrate-by-project) , you can enable the constraint again.
