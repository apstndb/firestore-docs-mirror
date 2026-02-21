This page describes how to use the Google Cloud console and the Google Cloud CLI to configure time-to-live (TTL) policies. Before you read this page, you should understand the [Datastore mode data model](/datastore/docs/concepts/entities) .

## Time-to-live overview

Use TTL policies to automatically remove stale data from your databases. A TTL policy designates a given property as the expiration time for entities in a given kind. With TTL, you can decrease storage costs by cleaning out obsolete data. Data is typically deleted within 24 hours after its expiration date.

### Pricing

TTL delete operations count towards your entity delete costs. For pricing of delete operations, see [Firestore in Datastore mode pricing](../pricing) .

### Limits and constraints

  - You can mark only one property per kind as a TTL property.
  - You can have a maximum of 500 TTL policies.

### TTL deletion

Note the following key behaviors of TTL-driven deletion:

  - Deletion through TTL is not an instantaneous process. Expired entities continue to appear in queries and lookup requests until the TTL process actually deletes them. TTL trades deletion timeliness for the benefit of reduced total cost of ownership for deletions. Data is typically deleted within 24 hours after its expiration date.

  - Deleting an entity through TTL does not delete that entity's descendant entities.

  - Applying a TTL policy on an existing kind results in a bulk deletion of all data that's expired according to the new TTL policy. Note that this bulk deletion is also not instantaneous and depends on how much data exists for that kind.

  - If an entity has an expiration time in the past and you add a new ttl policy to the kind, the entity will be deleted within 24 hours of the ttl policy finishing setup and becoming active.

  - TTL does not necessarily delete entities in the same order as their expiration timestamps.

  - Deletions are not done transactionally. Entities with the same expiration time are not necessarily deleted at the same time. If you require this behavior, perform the deletions using a client library.

  - Datastore mode will always honor the latest TTL field to determine the expiration. For example, if an expired but not-yet-deleted entity has its TTL field updated to a later date, the entity will not be expired and the new date will be used.

  - Datastore mode will only expire a document when the TTL field is set to a `  Timestamp  ` type. Leaving the field absent or set to a value like `  null  ` allows expirations to be disabled on a per-document basis.

  - TTL is designed to minimize impact on other database activities. Deletions driven by TTL are treated with a lower priority. Other strategies are also in place to smooth out traffic spikes from TTL-driven deletes.

### TTL properties and indexes

A TTL property can be indexed or un-indexed. However, because a TTL property is a timestamp, indexing the property can affect performance at higher traffic rates. Indexing a timestamp property is against best practices and can create [hotspots](/datastore/docs/best-practices#high_readwrite_rates_to_a_narrow_key_range) . Hotspots are high read, write, and delete rates to a narrow key range.

By default, Datastore creates a built-in index for all properties. You can [exclude a property from indexes](/datastore/docs/concepts/indexes#unindexed_properties) to disable indexes on a TTL property.

## Permissions

The principal configuring a TTL policy requires the following permission in the project:

  - Viewing TTL policies requires the `  datastore.indexes.list  ` and `  datastore.indexes.get  ` permissions.
  - Modifying TTL policies requires the `  datastore.indexes.update  ` permission.
  - Checking the status of TTL operations requires `  datastore.operations.list  ` and `  datastore.operations.get  ` .

For roles that assign these permissions, see [Datastore Identity and Access Management roles](/datastore/docs/access/iam#iam_roles) .

## Before you begin

Before you use the gcloud CLI to manage TTL policies, use the [`  gcloud components update  `](/sdk/gcloud/reference/components/update) command to update components to the latest available version:

``` text
gcloud components update
```

## Create a TTL policy

When you create a TTL policy, you designate an entity property as the expiration time for entities in a kind. The TTL policy applies to the specified kind in all namespaces.

TTL uses a specified property to identify entities that are eligible for deletion. This TTL property must be of type `  Date and time  ` . You can select a property that already exists or you can designate a property that you plan to add later.

Consider the following before you set the TTL property value:

  - The TTL property value can be a time in the future, now, or in the past. If the value is a time in the past, the entity is immediately eligible for deletion. For example, you might create a TTL policy with the property `  expireAt  ` , which you then add to existing entities.

  - Using any other data type or not setting the TTL property value will disable the TTL for the individual entity.

Follow the steps below to create a TTL policy:

### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

4.  Click **Create Policy** .

5.  Enter a kind name and a timestamp property name.

6.  Click **Create** .

The console returns to the **Time-to-live** page. If the operation successfully starts, the page adds an entry to the TTL policies table. On failure, the page displays an error message.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls update  `](/sdk/gcloud/reference/firestore/fields/ttls/update) command to configure a TTL policy. Add the `  --async  ` flag to prevent the gcloud CLI from waiting for the operation to complete.
    
    ``` text
    gcloud firestore fields ttls update ttl_field --collection-group=collection_group_name --enable-ttl
    ```

Even on an empty database, it can take ten minutes or more to enable a TTL policy. After you start an operation, closing the terminal does not cancel the operation.

## View TTL policies

Follow the steps below to view TTL policies and their statuses.

### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

The Google Cloud console lists TTL policies for your database and includes each policy's status.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls list  `](/sdk/gcloud/reference/firestore/fields/ttls/list) command to view a TTL policy. The following command lists all TTL policies.
    
    ``` text
    gcloud firestore fields ttls list
    ```
    
    To list TTL policies under a specific kind, use the following:
    
    ``` text
    gcloud firestore fields ttls list  --collection-group=collection_group_name
    ```

### View operation details

You can use the gcloud CLI to view more details about a TTL policy that is in the `  CREATING  ` state.

Use the [`  operations list  `](/sdk/gcloud/reference/firestore/operations/list) command to see all running and recently completed operations:

``` text
gcloud firestore operations list
```

The response includes an estimate of the operation's progress.

## Disable a TTL policy

Follow the steps below to disable a TTL policy.

### Google Cloud console

1.  In the Google Cloud console, go to the **Databases** page.

2.  Select the required database from the list of databases.

3.  In the navigation menu, click **Time-to-live** .

4.  In the TTL policy table, find the row for the TTL policy. Within this table row, click the **Delete** (trashcan) button.

5.  Confirm by clicking **Delete** .

The Google Cloud console returns to the **Time-to-live** page. On success, Datastore removes the TTL policy from the table.

### gcloud

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Use the [`  firestore fields ttls update  `](/sdk/gcloud/reference/firestore/fields/ttls/update) command to configure a TTL policy. Add the `  --async  ` flag to prevent the gcloud CLI from waiting for the operation to complete.
    
    ``` text
    gcloud firestore fields ttls update ttl_field --collection-group=collection_group_name --disable-ttl
    ```

## Monitor TTL deletions

You can use Cloud Monitoring to view metrics about TTL-driven deletions. Datastore provides the following metrics for TTL:

<table>
<tbody>
<tr class="odd">
<td>datastore.googleapis.com/entity/ttl_deletion_count</td>
<td>TTL deletion count</td>
<td><p>Total count of entities deleted by TTL policies.</p></td>
</tr>
<tr class="even">
<td>datastore.googleapis.com/entity/ttl_expiration_to_deletion_delays</td>
<td>TTL expiration to deletion delays</td>
<td><p>Time elapsed between when an entity expired under a TTL policy and when it was actually deleted.</p></td>
</tr>
</tbody>
</table>

To set up a dashboard with Datastore metrics, see [manage custom dashboard](/monitoring/charts/dashboards) and [add dashboard widgets](/monitoring/charts) .
