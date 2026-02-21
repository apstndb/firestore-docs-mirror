Every Firestore in Datastore mode [query](/datastore/docs/concepts/queries) computes its results using one or more *indexes* which contain entity keys in a sequence specified by the index's properties and, optionally, the entity's ancestors. The indexes are updated to reflect any changes the application makes to its entities, so that the correct results of all queries are available with no further computation needed.

There are two types of indexes:

  - *Built-in indexes*  
    By default, a Datastore mode database automatically predefines an index for each property of each entity kind. These single property indexes are suitable for simple types of queries.
  - *Composite indexes*  
    Composite indexes index multiple property values per indexed entity. Composite indexes support complex queries and are defined in an [index configuration file](/datastore/docs/tools/indexconfig) ( `  index.yaml  ` ).

The types of indexes are discussed in more detail later.

**Note:** The index-based query mechanism supports a wide range of queries and is suitable for most applications. However, it does not support some kinds of query common in other database technologies: in particular, joins and aggregate queries aren't supported within the Datastore mode query engine. See [Restrictions on queries](/datastore/docs/concepts/queries#restrictions_on_queries) for limitations on Datastore mode queries.

## Index definition and structure

An index is defined on a list of properties of a given [entity kind](/datastore/docs/concepts/entities#kinds_and_identifiers) , with a corresponding order (ascending or descending) for each property. For use with [ancestor queries](/datastore/docs/concepts/queries#ancestor_queries) , the index may also optionally include an entity's ancestors.

An index contains entries for every property named in the index's definition. Each entry of the index represents an entity that is a potential result for queries based on the index. An entity is included in the index only if it has an indexed value set for every property used in the index; if the index definition refers to a property for which the entity has no value, that entity won't appear in the index and hence will never be returned as a result for any query based on the index.

**Note:** Datastore mode databases distinguish between an entity that does not possess a property and one that possesses the property with a null value ( `  None  ` ). If you explicitly assign a null value to an entity's property, that entity may be included in the results of a query referring to that property.

The composite index is sorted first by ancestor and then by property values, in the order specified in the index definition. Based on this understanding, you can create the [perfect index](/datastore/docs/concepts/optimize-indexes#finding_the_perfect_index) that enables efficient querying.

## Index configuration

Firestore in Datastore mode provides *built-in* , or automatic, indexes for queries of the following forms:

  - Kindless queries using only ancestor and key filters
  - Queries using only ancestor and equality filters
  - Queries using only inequality filters (which are [limited to a single property](/datastore/docs/concepts/queries#inequality_filters_are_limited_to_at_most_one_property) )
  - Queries using only ancestor filters, equality filters on properties, and inequality filters on keys
  - Queries with no filters and only one sort order on a property, either ascending or descending

As an example, by default, Datastore mode databases automatically predefine two single property indexes for each property of each entity kind, one in ascending order and one in descending order. If you don't want your database to maintain an index for a property, [exclude the property from your indexes](#unindexed_properties) . Note that excluding a property removes it from any composite indexes.

Built-in indexes are sufficient to perform many simple queries, such as equality-only queries and simple inequality queries.

Built-in indexes don't appear in the [Indexes page](https://console.cloud.google.com/project/_/datastore/indexes) of the Google Cloud console.

For more complex queries, an application must define *composite* , or manual, indexes. Composite indexes are required for queries of the following form:

  - Queries with ancestor and inequality filters
  - Queries with one or more inequality filters on a property and one or more equality filters on other properties
  - Queries with a sort order on keys in descending order
  - Queries with multiple sort orders
  - Queries with one or more filters and one or more sort orders

Composite indexes are defined in the application's [index configuration file](/datastore/docs/tools/indexconfig) ( `  index.yaml  ` ). (Built-in indexes are not contained in the index configuration file.)

Composite indexes are composed of multiple properties and require that each individual property must not be [excluded from your indexes](#unindexed_properties) .

Composite indexes are viewable in the [Indexes page](https://console.cloud.google.com/project/_/datastore/indexes) of the Google Cloud console. You cannot use the Google Cloud console to create or update composite indexes.

If the application tries to perform a query that cannot be executed with the available indexes (either built-in or specified in the index configuration file), the query will fail.

The Datastore mode API automatically suggests indexes that are appropriate for most applications. Depending on your application's use of your Datastore mode database and the size and shape of your data, manual adjustments to your indexes may be warranted. For example, writing entities with multiple property values may result in an [exploding index](#index_limits) with high [storage costs](/datastore/docs/concepts/storage-size) and increased write latency.

The [Datastore emulator](/datastore/docs/tools/datastore-emulator) can help make it easier to manage your index configuration file. Instead of failing to execute a query that requires an index and does not have one, the Datastore emulator can generate an index configuration that would allow the query to succeed. If your local testing of an application exercises every possible query the application will issue, using every combination of filter and sort order, the generated entries will represent a complete set of indexes. If your testing does not exercise every possible query form, you can review and adjust the index configuration file before updating indexes.

You can learn more about `  index.yaml  ` at [Index Configuration](/datastore/docs/tools/indexconfig) .

## Deploying or deleting indexes

When you are done modifying your index configuration file, run the [`  gcloud datastore indexes create  `](/sdk/gcloud/reference/datastore/indexes/create) command to place the indexes into service. Learn more at [updating your indexes](/datastore/docs/tools/indexconfig#Datastore_Updating_indexes) .

**Note:** If you use the `  appcfg.py  ` or `  appcfg.sh  ` commands to deploy an application to App Engine, the index configuration file is automatically deployed. If you use the [`  gcloud app deploy  `](/sdk/gcloud/reference/app/deploy) command to deploy your application, the index configuration file is not automatically deployed. You must either specifically list `  index.yaml  ` as an argument to `  gcloud app deploy  ` or run `  gcloud datastore indexes create  ` to deploy the index configuration file.

If you previously deployed indexes that are no longer needed, you can [delete the unused indexes](/datastore/docs/tools/indexconfig#Datastore_Deleting_unused_indexes) .

## Storage costs and write latency

Indexes contribute to your storage costs. [Index entry size](/datastore/docs/concepts/storage-size#index_entry_size) describes how built-in and composite indexes contribute to your database's storage size. You can use [Firestore in Datastore mode statistics](/datastore/docs/concepts/stats) to see more information about index entries and index storage size.

Indexes also contribute to write latency. When updating a property value, the database also updates every related index. The more indexes the database needs to update, the longer the operation takes.

You can reduce storage costs and improve write performance by [deleting unused indexes](/datastore/docs/tools/indexconfig#Datastore_Deleting_unused_indexes) and [excluding properties from indexing](/datastore/docs/concepts/indexes#unindexed_properties) . This also prevents operations from failing due to [index limits](#index_limits) .

## Indexes and properties

Here are a few special considerations to keep in mind about indexes and how they relate to the properties of your entities:

### Properties with mixed value types

When two entities have properties of the same name but different value types, an index of the property sorts the entities first by [value type](/datastore/docs/concepts/entities#value_type_ordering) and then by a secondary ordering appropriate to each type. For example, if two entities each have a property named `  age  ` , one with an integer value and one with a string value, the entity with the integer value always precedes the one with the string value when sorted by the `  age  ` property, regardless of the property values themselves.

This is especially worth noting in the case of integers and floating-point numbers, which are treated as separate types by Datastore mode. Because all integers are sorted before all floats, a property with the integer value `  38  ` is sorted before one with the floating-point value `  37.5  ` .

### Excluded properties

If you know you will never have to filter or sort on a particular property, you can tell your Datastore mode database not to maintain index entries for that property by excluding it from indexes. This lowers the cost of running your application by reducing the [storage size](/datastore/docs/concepts/storage-size) needed for index entries. This can also improve write latency. An entity with an excluded property behaves as if the property were not set: queries with a filter or sort order on the excluded property will never match that entity.

**Note:** If a property appears in a composite index, then excluding the property will disable it in the composite index. For example, suppose that an entity has properties **priority** and **done** and that you want to create an index able to satisfy queries like `  WHERE priority = 4 AND done = FALSE  ` . Also suppose that you don't care about the queries `  WHERE priority = 4  ` and `  WHERE done = FALSE  ` . If you exclude **priority** from indexes and create an index for **priority** and **done** , Datastore mode won't create index entries for the **priority** and **done** index and so the `  WHERE priority = 4 AND done = FALSE  ` query won't work. For your database to create entries for the **priority** and **done** indexes, both **priority** and **done** must be indexed.

The `  description  ` property in the following example is excluded from indexes:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["category"] = "Personal",
    ["created"] = new DateTime(1999, 01, 01, 0, 0, 0, DateTimeKind.Utc),
    ["done"] = false,
    ["priority"] = 4,
    ["percent_complete"] = 10.0,
    ["description"] = new Value()
    {
        StringValue = "Learn Cloud Datastore",
        ExcludeFromIndexes = true
    },
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
type Task struct {
 Category        string
 Done            bool
 Priority        int
 Description     string `datastore:",noindex"`
 PercentComplete float64
 Created         time.Time
}
task := &Task{
 Category:        "Personal",
 Done:            false,
 Priority:        4,
 Description:     "Learn Cloud Datastore",
 PercentComplete: 10.0,
 Created:         time.Now(),
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task =
    Entity.newBuilder(taskKey)
        .set("category", "Personal")
        .set("created", Timestamp.now())
        .set("done", false)
        .set("priority", 4)
        .set("percent_complete", 10.0)
        .set(
            "description",
            StringValue.newBuilder("Learn Cloud Datastore").setExcludeFromIndexes(true).build())
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = [
  {
    name: 'category',
    value: 'Personal',
  },
  {
    name: 'created',
    value: new Date(),
  },
  {
    name: 'done',
    value: false,
  },
  {
    name: 'priority',
    value: 4,
  },
  {
    name: 'percent_complete',
    value: 10.0,
  },
  {
    name: 'description',
    value: 'Learn Cloud Datastore',
    excludeFromIndexes: true,
  },
];
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity(
    $key,
    [
        'category' => 'Personal',
        'created' => new DateTime(),
        'done' => false,
        'priority' => 4,
        'percent_complete' => 10.0,
        'description' => 'Learn Cloud Datastore'
    ],
    ['excludeFromIndexes' => ['description']]
);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

import datetime

key = client.key("Task")
task = datastore.Entity(key, exclude_from_indexes=("description",))
task.update(
    {
        "category": "Personal",
        "description": "Learn Cloud Datastore",
        "created": datetime.datetime.now(tz=datetime.timezone.utc),
        "done": False,
        "priority": 4,
        "percent_complete": 10.5,
    }
)
client.put(task)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = datastore.entity "Task" do |t|
  t["category"] = "Personal"
  t["created"] = Time.now
  t["done"] = false
  t["priority"] = 4
  t["percent_complete"] = 10.0
  t["description"] = "Learn Cloud Datastore"
  t.exclude_from_indexes! "description", true
end
```

### GQL

Not Applicable

The query in the following example won't return any results if the `  description  ` property was excluded:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.Equal("description", "Learn Cloud Datastore")
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Tasks").
 FilterField("Description", "=", "A task description")
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.eq("description", "A task description"))
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(new PropertyFilter('description', '=', 'A task description.'));
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('description', '=', 'A task description.');
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="Task")
query.add_filter(
    filter=datastore.query.PropertyFilter(
        "description", "=", "Learn Cloud Datastore"
    )
)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("description", "=", "A task description.")
```

### GQL

``` text
# Will not return any results!
SELECT * FROM Task WHERE description = 'A task description.'
```

You can later change the property back to indexed.

Note, however, that changing a property from excluded to indexed does not affect any existing entities that may have been created before the change. Queries filtering on the property won't return such existing entities, because the entities weren't written to the query's index when they were created. To make the entities accessible by future queries, you must rewrite them to your database so that they will be entered in the appropriate indexes. That is, you must do the following for each such existing entity:

1.  Lookup (get) the entity.
2.  Write (put) the entity back to your database.

Similarly, changing a property from indexed to excluded only affects entities subsequently written to your database. The index entries for any existing entities with that property will continue to exist until the entities are updated or deleted. To avoid unwanted results, you must purge your code of all queries that filter or sort by the (now excluded) property.

## Index limits

Firestore in Datastore mode imposes limits on the number and overall size of index entries that can be associated with a single entity. These limits are large, and most applications are not affected. However, there are circumstances in which you might encounter the limits.

As described [above](#index_configuration) , a Datastore mode database creates an entry in a predefined index for every property of every entity except those you have explicitly declared as [excluded from your indexes](#unindexed_properties) . The property may also be included in additional, custom indexes declared in your [index configuration file](/datastore/docs/tools/indexconfig) ( `  index.yaml  ` ). Provided that an entity has no list properties, it will have at most one entry in each such custom index (for non-ancestor indexes) or one for each of the entity's ancestors (for ancestor indexes). Each of these index entries must be updated every time the value of the property changes.

For a property that has a single value for each entity, each possible value needs to be stored just once per entity in the property's predefined index. Even so, it is possible for an entity with a large number of such single-valued properties to exceed the index entry or size limit. Similarly, an entity that can have multiple values for the same property requires a separate index entry for each value; again, if the number of possible values is large, such an entity can exceed the entry limit.

The situation becomes worse in the case of entities with multiple properties, each of which can take on multiple values. To accommodate such an entity, the index must include an entry for every possible *combination* of property values. Custom indexes that refer to multiple properties, each with multiple values, can "explode" combinatorially, requiring large numbers of entries for an entity with only a relatively small number of possible property values. Such *exploding indexes* can dramatically increase the [storage size](/datastore/docs/concepts/storage-size) of an entity, because of the large number of index entries that must be stored. Exploding indexes also can cause the entity to exceed the index entry count or size limit.

Consider the following code:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Entity task = new Entity()
{
    Key = _db.CreateKeyFactory("Task").CreateKey("sampleTask"),
    ["tags"] = new ArrayValue() { Values = { "fun", "programming", "learn" } },
    ["collaborators"] = new ArrayValue() { Values = { "alice", "bob", "charlie" } },
    ["created"] = DateTime.UtcNow
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
task := &Task{
 Tags:          []string{"fun", "programming", "learn"},
 Collaborators: []string{"alice", "bob", "charlie"},
 Created:       time.Now(),
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Entity task =
    Entity.newBuilder(taskKey)
        .set("tags", "fun", "programming", "learn")
        .set("collaborators", "alice", "bob", "charlie")
        .set("created", Timestamp.now())
        .build();
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const task = {
  method: 'insert',
  key: datastore.key('Task'),
  data: {
    tags: ['fun', 'programming', 'learn'],
    collaborators: ['alice', 'bob', 'charlie'],
    created: new Date(),
  },
};
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$task = $datastore->entity(
    $datastore->key('Task'),
    [
        'tags' => ['fun', 'programming', 'learn'],
        'collaborators' => ['alice', 'bob', 'charlie'],
        'created' => new DateTime(),
    ]
);
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

import datetime

task = datastore.Entity(client.key("Task"))
task.update(
    {
        "tags": ["fun", "programming", "learn"],
        "collaborators": ["alice", "bob", "charlie"],
        "created": datetime.datetime.now(tz=datetime.timezone.utc),
    }
)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
task = datastore.entity "Task" do |t|
  t["tags"] = ["fun", "programming", "learn"]
  t["collaborators"] = ["alice", "bob", "charlie"]
  t["created"] = Time.now
end
```

### GQL

Not Applicable

It creates a `  Task  ` entity with three values for property `  tags  ` , three values for property `  collaborators  ` , and `  created  ` set to the current date. This will require 9 index entries, one for each possible combination of property values:

( `  'fun'  ` , `  'alice'  ` , `  NOW()  ` )  
( `  'fun'  ` , `  'bob'  ` , `  NOW()  ` )  
( `  'fun'  ` , `  'charlie'  ` , `  NOW()  ` )

( `  'programming'  ` , `  'alice'  ` , `  NOW()  ` )  
( `  'programming'  ` , `  'bob'  ` , `  NOW()  ` )  
( `  'programming'  ` , `  'charlie'  ` , `  NOW()  ` )

( `  'learn'  ` , `  'alice'  ` , `  NOW()  ` )  
( `  'learn'  ` , `  'bob'  ` , `  NOW()  ` )  
( `  'learn'  ` , `  'charlie'  ` , `  NOW()  ` )

When the same property is repeated multiple times, Firestore in Datastore mode can detect exploding indexes and suggest an alternative index. However, in all other circumstances (such as the query defined in this example), a Datastore mode database will generate an exploding index. In this case, you can circumvent the exploding index by manually configuring an index in your index configuration file:

``` text
indexes:
- kind: Task
  properties:
  - name: tags
  - name: created
- kind: Task
  properties:
  - name: collaborators
  - name: created
```

This reduces the number of entries needed to only `  (|tags|  ` `  *  ` `  |created|  ` `  +  ` `  |collaborators|  ` `  *  ` `  |created|)  ` , or 6 entries instead of 9:

( `  'fun'  ` , `  NOW()  ` )  
( `  'programming'  ` , `  NOW()  ` )  
( `  'learn'  ` , `  NOW()  ` )

( `  'alice'  ` , `  NOW()  ` )  
( `  'bob'  ` , `  NOW()  ` )  
( `  'charlie'  ` , `  NOW()  ` )

Any `  commit  ` operation that would cause an index to exceed the index entry or size limit will fail. The text of the error describes which limit was exceeded ( `  "Too many indexed properties"  ` or `  "Index entries too large"  ` ) and which custom index was the cause. If you create a new index that would exceed the limits for any entity when built, queries against the index will fail and the index will appear in the `  Error  ` state in the Google Cloud console. To handle such `  Error  ` indexes,

1.  Remove the index from your index configuration file ( `  index.yaml  ` ).
2.  Using the Google Cloud CLI, remove the index from the database using the `  datastore indexes cleanup  ` command, as described in [Deleting unused indexes](/datastore/docs/tools/indexconfig#Datastore_Deleting_unused_indexes) .
3.  Either
      - reformulate the index definition and corresponding queries, or
      - remove the entities that are causing the index to explode.
4.  Add the index back to `  index.yaml  ` .
5.  Using the Google Cloud CLI, add the index to the database by running the `  datastore indexes create  ` command, as described in [Updating Indexes](/datastore/docs/tools/indexconfig#Datastore_Updating_indexes) .

You can avoid exploding indexes by avoiding queries that would require a custom index using a list property. As described earlier, this includes queries with multiple sort orders or queries with a mix of equality and inequality filters.

## Indexes for projections

[Projection queries](/datastore/docs/concepts/queries#projection_queries) require all properties specified in the projection to be included in an index. The [Datastore emulator](/datastore/docs/tools/datastore-emulator) automatically generates the needed indexes for you in the index configuration file, `  index.yaml  ` , which is uploaded with your application.

One way to minimize the number of indexes required is to project the same properties consistently, even when not all of them are always needed. For example, these queries require two separate indexes:

``` text
SELECT priority, percent_complete FROM Task

SELECT priority, percent_complete, created FROM Task
```

However, if you always project properties `  priority  ` , `  percent_complete  ` , `  created  ` , even when `  created  ` is not required, only one index will be needed.

Converting an existing query into a projection query may require building a new index if the properties in the projection are not already included in another part of the query. For example, suppose you had an existing query like

``` text
SELECT * FROM Task
WHERE priority > 1
ORDER BY priority, percent_complete
```

which requires the index:

``` text
indexes:
- kind: Task
  properties:
  - name: priority
  - name: percent_complete
```

Converting this to either of the projection queries

``` text
SELECT created FROM Task
WHERE priority > 1
ORDER BY priority, percent_complete

SELECT priority, percent_complete, created FROM Task
WHERE priority > 1
ORDER BY priority, percent_complete
```

introduces a new property ( `  created  ` ) and thus will require building a new index:

``` text
indexes:
- kind: Task
  properties:
  - name: priority
  - name: percent_complete
  - name: created
```

However,

``` text
SELECT priority, percent_complete FROM Task
WHERE priority > 1
ORDER BY priority, percent_complete
```

would *not* change the required index, since the projected properties `  priority  ` and `  percent_complete  ` were already included in the existing query.

## Multiple databases

You can use `  gcloud firestore  ` to manage a single index for Datastore mode or use `  gcloud datastore  ` with an index.yaml file to manage all the indexes under a database.

##### gcloud firestore

``` text
gcloud firestore indexes composite create --api-scope=datastore-mode-api  --query-scope=QUERY_SCOPE --database=DATABASE_ID
```

##### gcloud datastore

``` text
gcloud alpha datastore indexes create index.yaml --database=DATABASE_ID
```

Replace the following:

  - DATABASE\_ID : a database ID.
  - QUERY\_SCOPE : either `  collection-recursive  ` for ancestor indexes or `  collection-group  ` for non-ancestor indexes.
