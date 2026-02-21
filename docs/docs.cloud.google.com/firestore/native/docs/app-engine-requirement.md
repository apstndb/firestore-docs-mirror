# App Engine Requirement

Previously, all Firestore databases were linked to an App Engine app. When linked, your database requires an active App Engine app in the same project. Without the active App Engine app, read and write access to the database is disabled.

Firestore databases are now provisioned unlinked from App Engine by default.

If your database is linked to an App Engine, you can unlink your database.

## Active App Engine

An active App Engine app means that an app exists in the same project and that this app is not disabled. It does not require that app to have any usage. The linked app and database must exist in the same region.

If you disable your App Engine app, you also disable access to the Firestore database linked to that app.

### View App Engine link status

You can check the App Engine unlink state using the REST API:

``` text
curl  --header "Authorization: Bearer $(gcloud auth print-access-token)" \
--header "Content-type: application/json" \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases/(default)"
```

In the response, look at the value of `  appEngineIntegrationMode  ` . If the value is `  DISABLED  ` , your database is not linked to an App Engine app.

### Unlink your database from App Engine

If you disable a linked App Engine app, you also disable read and write access to your database. If this happens, the **Firestore Data** page in Google Cloud console presents the option to unlink your database from the App Engine app. Click **Unlink Database** to begin the process.

You can also unlink your database using the REST API:

``` text
curl -X PATCH \
--header "Authorization: Bearer $(gcloud auth print-access-token)" \
--header "Content-type: application/json" \
--data '{"app_engine_integration_mode": "DISABLED"}' \
"https://firestore.googleapis.com/v1/projects/PROJECT_ID/databases/(default)?updateMask=appEngineIntegrationMode"
```

When you unlink your database, you can disable App Engine without affecting access to your database. Unlinking is a permanent operation. It may take up to five minutes for the unlinking operation to take effect.

## Migrating Terraform App Engine Resources

If you previously managed Firestore databases via the `  google_app_engine_application  ` Terraform resource, you can use the `  google_firestore_database  ` Terraform resource instead.

For general instructions on managing Firestore databases via Terraform, see [Automating database creation](https://cloud.google.com/firestore/docs/solutions/automate-database-create#create_a_database_with_terraform) .

### Create a google\_firestore\_database resource

In your Terraform configuration file, create a new `  google_firestore_database  ` resource:

#### firestore.tf

``` text
resource "google_firestore_database" "database" {
  project     = "project"
  name        = "(default)"
  location_id = "location"
  
  type = "database_type" // either "FIRESTORE_NATIVE" or "DATASTORE_MODE"
  
  app_engine_integration_mode = "DISABLED"

  // Optional, but recommended for safety
  delete_protection_state = "DELETE_PROTECTION_ENABLED"
}
```

See [Firestore locations](https://cloud.google.com/firestore/docs/locations) for the list of available locations. Choose the location corresponding to that of your existing database.

### Import the existing Firestore database

First, ensure that the [Firestore API](#enabling_the_api_via_terraform) is enabled.

Next, import the existing Firestore database into your Terraform state:

``` text
terraform import google_firestore_database.database "(default)"
```

Next, run:

``` text
terraform plan
```

Inspect the output to ensure the import completed successfully. If the output shows any fields changing, ensure these changes are intended. If the output includes a line similar to:

``` text
google_firestore_database.database must be replaced
```

then inspect your Terraform configuration file to see if there were any mistakes, particularly in the project , location , or name fields, and then run `  terraform plan  ` again. Any fields that are requiring Terraform to replace your database will be marked with `  # forces replacement  ` in the plan output.

**Warning:** Do not run `  terraform apply  ` if you see any database resources requiring replacement. Doing so may cause the loss of your Firestore data.

Once you are satisfied with the Terraform plan output, run:

``` text
terraform apply
```

### Removing the google\_app\_engine\_application resource

If you have an existing `  google_app_engine_application  ` resource in your Terraform configuration file, remove it from that file now.

Afterwards, once again run:

``` text
terraform plan
```

You should see output similar to the following:

``` text
Terraform will perform the following actions:

  # google_app_engine_application.app will be destroyed
  # (because google_app_engine_application.app is not in configuration)
```

Once you are satisfied with the plan output, run

``` text
terraform apply
```

Terraform does not currently support deletion of App Engine resources; although Terraform will show the resource as being destroyed, it will not actually delete the App Engine application. However, the App Engine application will no longer be managed by Terraform.

## Firestore API Requirement

Previously, all Firestore databases were linked to an App Engine app. Firestore databases are now provisioned unlinked from App Engine by default. Additionally, all databases, both existing and newly created, now have the following requirements:

  - To manage your database from the Google Cloud console and the gcloud CLI, the Firestore API must be enabled in the project. This is required for both Firestore in Native mode and Firestore in Datastore mode databases.

  - When executed from the Google Cloud console or the gcloud CLI, the administrative operations below will require the following IAM permissions:
    
      - Create database: `  datastore.databases.create  `
      - View database metadata: `  datastore.databases.getMetadata  `
      - Edit database metadata: `  datastore.databases.update  `

[Predefined roles](/firestore/docs/security/iam#predefined_roles) such as *Datastore User* and *Datastore Viewer* include the required permissions. If you created any custom IAM roles, you may need to update them to include the permissions above.

If you previously defined a custom role for Datastore, it might lack the `  datastore.databases.getMetadata  ` permission. Ensure continued access by updating your custom roles with `  datastore.databases.getMetadata  ` or by using a [predefined role](/firestore/docs/security/iam#predefined_roles) .

### Enabling the API via Terraform

If you wish, you can also enable the Firestore API via Terraform:

``` text
resource "google_project_service" "firestore" {
  project = "project"
  service = "firestore.googleapis.com"
}
```

If you have a `  google_firestore_database  ` resource, you can add a dependency on the `  google_project_service  ` resource to ensure that the API is enabled before Terraform attempts to create the database:

``` text
resource "google_firestore_database" "database" {
  // ...
  depends_on = [google_project_service.firestore]
}
```
