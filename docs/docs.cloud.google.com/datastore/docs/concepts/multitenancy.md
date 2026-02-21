You can support *multitenancy* in your application by providing separate data partitions for multiple client organizations, known as tenants. This allows you to customize *data values* for each tenant, while keeping the same *data schema* for all tenants. This makes provisioning new tenants more efficient because you don't have to change data structure when you add a tenant.

## Benefits of multitenancy

Firestore in Datastore mode allows a multitenant application to use separated silos of data for each tenant while still using:

  - a single project
  - a single logical structure for the kinds
  - a single set of index definitions, because the kinds are the same logically for each tenant

Datastore mode enables multitenancy by providing *namespaces* .

## Multitenancy and partitioned data

Datastore mode uses *partitions* to silo data for each tenant. The combination of a project ID and a namespace ID forms a *partition ID* , which identifies each partition. An entity belongs to a single partition, and queries are scoped to a single partition.

**Note:** Namespaces are not a security mechanism in Datastore mode. A user with access to one partition in a project has access to all partitions in the project. Namespaces provide a way to organize your entities within a project.

## Specifying a namespace for an entity

You specify the namespace when you create the entity: after you create the entity, you cannot change the namespace. If you don't explicitly specify a namespace for an entity, it is automatically assigned to the *default namespace* , which has no string identifier.

## Using namespaces with parent entities

An entity and all of its ancestors belong to one and only one namespace. This means that when you create an entity with another entity designated as parent, the child entity is in the same namespace as its parent: you cannot specify some other namespace.

## Sample use case

A key benefit of multitenancy is having the same application serve multiple client organizations. To achieve this benefit, for a given kind, your application should behave the same regardless of the namespace. For example, from the application’s perspective, an entity of kind `  Task  ` in one namespace should logically be the same as an entity of kind `  Task  ` in all other namespaces. Your application could then use a single set of index definitions to support `  Task  ` queries, regardless of which namespaces contain `  Task  ` entities.

For example, consider a Task List application that silos data on a per user basis. The application could define namespaces based on user name, resulting in the following partitions:

``` text
Partition ID: project:"my_project_id"/namespace:"Joe"
Partition ID: project:"my_project_id"/namespace:"Alice"
Partition ID: project:"my_project_id"/namespace:"Charlie"
```

The application could define a logical structure of a `  Task  ` kind as follows, to use for all namespaces:

``` text
kind: Task
properties:
 - "done", Boolean
 - "created", DateTime
 - "description", String, excluded from index
```

When a user creates an entity of kind `  Task  ` , the entity is stored in the user’s own partition, resulting in siloed data. The application processes `  Task  ` entities consistently across namespaces because only one schema is used for the `  Task  ` kind. An application with siloed data and consistent behaviour would be multitenant.

If the logical structure of a `  Task  ` kind differs by namespace, the application would not be multitenant because it processes `  Task  ` entities differently across namespaces. For example, consider `  Task  ` kinds that have different schema based on namespace:

  - `  Task  ` entities in the Joe namespace *exclude* the `  description  ` property from the index
  - `  Task  ` entities in the Alice namespace *include* the `  description  ` property from the index

The application could query on the `  description  ` property for Alice’s `  Task  ` entities, but it could not query on the `  description  ` property for Joe’s `  Task  ` entities, so the application would not be multitenant.

## Viewing namespaces in the console

To see statistics for the namespaces used in your project, visit the [Datastore Dashboard](https://console.cloud.google.com/datastore/stats) page in the Google Cloud console. To programmatically determine which namespaces are used in your project, see [Namespace queries](/datastore/docs/concepts/metadataqueries#namespace_queries) .

If you need to group data *within* a tenant, you can categorize your data by [kinds](/datastore/docs/concepts/entities#kinds_and_identifiers) , and you can also organize highly related data with [entity groups](/datastore/docs/concepts/entities#entity_groups) .

## What's next

  - Learn about [entities](/datastore/docs/concepts/entities) .
  - Learn about [queries](/datastore/docs/concepts/queries) .
