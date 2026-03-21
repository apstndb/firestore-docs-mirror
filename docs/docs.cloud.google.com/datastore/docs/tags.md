This guide describes how to create and manage tags on Datastore mode databases.

## About tags

A tag is a key-value pair that can attach to a resource within Google Cloud. You can use tags to conditionally allow or deny policies based on whether a resource has a specific tag. For example, you can conditionally grant Identity and Access Management (IAM) roles based on whether a resource has a specific tag. For more information about tags, see [Tags overview](/resource-manager/docs/tags/tags-overview) .

Tags are attached to resources by creating a tag binding resource that links the value to the Google Cloud resource.

## Required permissions

To get the permissions that you need to manage tags, ask your administrator to grant you the following IAM roles:

  - [Tag Viewer](/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer) ( `  roles/resourcemanager.tagViewer  ` ) on the resources the tags are attached to
  - View and manage tags at the organization level: [Organization Viewer](/iam/docs/roles-permissions/resourcemanager#resourcemanager.organizationViewer) ( `  roles/resourcemanager.organizationViewer  ` ) on the organization
  - Create, update, and delete tag definitions: [Tag Administrator](/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagAdmin) ( `  roles/resourcemanager.tagAdmin  ` ) on the resource you're creating, updating, or deleting tags for
  - Attach and remove tags from resources: [Tag User](/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser) ( `  roles/resourcemanager.tagUser  ` ) on the tag value and the resources that you are attaching or removing the tag value to

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

To attach tags to Datastore databases, you need the [Datastore Owner](/datastore/docs/access/iam#iam_roles) role ( `  roles/datastore.owner  ` ).

## Create tag keys and values

Before you can attach a tag, you need to create a tag and configure its value. To create tag keys and tag values, see [Creating a tag](/resource-manager/docs/tags/tags-creating-and-managing#creating_tag) and [Adding a tag value](/resource-manager/docs/tags/tags-creating-and-managing#adding_tag_values) .

## Add tags during resource creation

You can add tags at the time of creating databases. Adding tags during resource creation, lets you instantly provide essential metadata for your resources and also helps with better organization, cost tracking, and automated policy application.

### gcloud

``` text
  gcloud firestore databases create \
      --location=LOCATION \
      --database=DATABASE \
      --tags=[KEY=VALUE,...]
```

Replace the following:

  - `  LOCATION  ` : the location to operate on.
  - `  DATABASE  ` : the ID to use for the database.
  - `  KEY  ` = `  VALUE  ` : list of tags KEY=VALUE pairs to bind. Each item must be expressed as `  <tag-key-namespaced-name>=<tag-value-short-name>  ` or `  <tag-key-name>=<tag-value-name>  ` .

Specify multiple tags by separating the tags with a comma, for example, `  TAGKEY1=TAGVALUE1,TAGKEY2=TAGVALUE2  `

### API

Send a `  POST  ` request to the following URL:

``` text
      
https://firestore.googleapis.com/v1/projects/PROJECT/databases?databaseId=DATABASE
```

Provide the following JSON in the request body:

``` text
      
"type": "FIRESTORE_NATIVE",
"locationId": LOCATION,
"tags": {KEY:VALUE}
```

Replace the following:

  - `  PROJECT  ` : the project to operate on.
  - `  DATABASE  ` : the ID to use for the database.
  - `  LOCATION  ` : the location to operate on.
  - `  KEY  ` : `  VALUE  ` : list of tags KEY=VALUE pairs to bind. Each item must be expressed as `  <tag-key-namespaced-name>:<tag-value-short-name>  ` or `  <tag-key-name>:<tag-value-name>  ` .

## Add tags to existing resources

To add a tag to existing databases, follow these steps:

### gcloud

To attach a tag to a database, you must create a tag binding resource by using the `  gcloud resource-manager tags bindings create  ` command:

``` text
      gcloud resource-manager tags bindings create \
          --tag-value=TAGVALUE_NAME \
          --parent=RESOURCE_ID \
          --location=LOCATION
      
```

Replace the following:

  - `  TAGVALUE_NAME  ` : the permanent ID or namespaced name of the tag value that is attached—for example, `  tagValues/567890123456  ` .
  - `  RESOURCE_ID  ` is the full ID of the resource, including the API domain name to identify the type of resource ( `  //firestore.googleapis.com/  ` ). For example, to attach a tag to a database in `  projects/firestore-test-project  ` , the full ID is: `  //firestore.googleapis.com/projects/firestore-test-project/databases/\(default\)  ` .
  - `  LOCATION  ` : the location of your resource. If you're attaching a tag to a global resource, such as a folder or a project, omit this flag. If you're attaching a tag to a regional or a zonal resource, you must specify the location—for example, `  us-central1  ` (region) or `  us-central1-a  ` (zone).

## List tags attached to resources

You can view a list of tag bindings directly attached to or inherited by the database.

### gcloud

To get a list of tag bindings attached to a resource, use the `  gcloud resource-manager tags bindings list  ` command:

``` text
      gcloud resource-manager tags bindings list \
          --parent=RESOURCE_ID \
          --location=LOCATION
      
```

Replace the following:

  - `  RESOURCE_ID  ` is the full ID of the resource, including the API domain name to identify the type of resource ( `  //firestore.googleapis.com/  ` ). For example, to attach a tag to a database in `  projects/firestore-test-project  ` , the full ID is: `  //firestore.googleapis.com/projects/firestore-test-project/databases/\(default\)  ` .
  - `  LOCATION  ` : the location of your resource. If you're viewing a tag attached to a global resource, such as a folder or a project, omit this flag. If you're viewing a tag attached to a regional or a zonal resource, you must specify the location—for example, `  us-central1  ` (region) or `  us-central1-a  ` (zone).

You should get a response similar to the following:

``` text
name: tagBindings/%2F%2Fcloudresourcemanager.googleapis.com%2Fprojects%2F7890123456/tagValues/567890123456
          tagValue: tagValues/567890123456
          resource: //firestore.googleapis.com/projects/firestore-test-project/databases/(default)
      
```

## Detach tags from resources

You can detach tags that have been directly attached to a database. Inherited tags can be overridden by attaching a tag with the same key and a different value, but they can't be detached.

### gcloud

To delete a tag binding, use the `  gcloud resource-manager tags bindings delete  ` command:

``` text
      gcloud resource-manager tags bindings delete \
          --tag-value=TAGVALUE_NAME \
          --parent=RESOURCE_ID \
          --location=LOCATION
      
```

Replace the following:

  - `  TAGVALUE_NAME  ` : the permanent ID or namespaced name of the tag value that is attached—for example, `  tagValues/567890123456  ` .
  - `  RESOURCE_ID  ` is the full ID of the resource, including the API domain name to identify the type of resource ( `  //firestore.googleapis.com/  ` ). For example, to attach a tag to a database in `  projects/firestore-test-project  ` , the full ID is: `  //firestore.googleapis.com/projects/firestore-test-project/databases/\(default\)  ` .
  - `  LOCATION  ` : the location of your resource. If you're attaching a tag to a global resource, such as a folder or a project, omit this flag. If you're attaching a tag to a regional or a zonal resource, you must specify the location—for example, `  us-central1  ` (region) or `  us-central1-a  ` (zone).

## Delete tag keys and values

When removing a tag key or value definition, ensure that the tag is detached from the database. You must delete existing tag attachments, called tag bindings, before deleting the tag definition itself. To delete tag keys and tag values, see [Deleting tags](/resource-manager/docs/tags/tags-creating-and-managing#deleting) .

## Identity and Access Management conditions and tags

You can use tags and IAM conditions to conditionally grant role bindings to users in your hierarchy. Changing or deleting the tag attached to a resource can remove user access to that resource if an IAM policy with conditional role bindings has been applied. For more information, see [Identity and Access Management conditions and tags](/resource-manager/docs/tags/tags-creating-and-managing#iam_conditions_and_tags) .

## What's next

  - See the other [services that support tags](/resource-manager/docs/tags/tags-supported-services) .
  - See [Tags and access control](/iam/docs/tags-access-control) to learn how to use tags with IAM.
