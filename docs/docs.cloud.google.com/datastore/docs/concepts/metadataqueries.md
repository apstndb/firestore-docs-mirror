Firestore in Datastore mode provides access to metadata that includes information about entity groups, namespaces, entity kinds, properties, and [property representations](#property_queries_property_representations) for each property. You can use metadata, for example, to build a custom datastore viewer for your application or for backend administrative functions.

The [Datastore Dashboard](https://console.cloud.google.com/project/_/datastore/stats) in the Google Cloud console also provides some metadata about your application, but the data displayed there differs in some important respects from that returned by these functions.

  - **Freshness.** Reading metadata using the API gets current data, whereas data in the dashboard is updated only once daily.
  - **Contents.** Some metadata in the dashboard is not available through the APIs; the reverse is also true.
  - **Speed.** Metadata gets and queries are [billed in the same way as datastore gets and queries](/appengine/docs/pricing#costs-for-datastore-calls) . Metadata queries that fetch information on namespaces, kinds, and properties are generally slow to execute. As a rule of thumb, expect a metadata query that returns *N* entities to take about the same time as *N* ordinary queries each returning a single entity. Furthermore, [property representation queries](#property_queries_property_representations) (non-keys-only property queries) are slower than keys-only [property queries](#property_queries) . Metadata gets of entity group metadata are somewhat faster than getting a regular entity.

## Metadata queries

Three special entity kinds are reserved for metadata queries:

<table>
<thead>
<tr class="header">
<th>Entity</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       __namespace__      </code></td>
<td>Used to find all the namespaces used in your application entities.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __kind__      </code></td>
<td>Used to query a specific kind.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       __property__      </code></td>
<td>Used to query by a property of a kind.</td>
</tr>
</tbody>
</table>

These kinds will not conflict with others of the same names that may already exist in your application. By querying on these special kinds, you can retrieve entities containing the desired metadata.

The entities returned by metadata queries are generated dynamically, based on the current state of your database. While you can create local entity objects of kinds `  __namespace__  ` , `  __kind__  ` , or `  __property__  ` , any attempt to store them in the database will fail.

## Namespace queries

You can use a *namespace query* to find all namespaces used in the application's entities. This allows you to perform activities such as administrative functions across multiple namespaces.

Namespace queries return entities of the special kind `  __namespace__  ` whose key name is the name of a namespace. (An exception is the default namespace designated by the empty string `  ""  ` : since the empty string is not a valid key name, this namespace is keyed with the numeric ID `  1  ` instead.) Queries of this type support filtering only for ranges over the special pseudoproperty `  __key__  ` , whose value is the entity's key. The results can be sorted by ascending (but not descending) `  __key__  ` value. Because `  __namespace__  ` entities have no properties, both keys-only and non-keys-only queries return the same information.

The following example returns a list of an application's namespaces in the range between the values assigned to the `  startNamespace  ` and `  endNamespace  ` variables:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
KeyFactory keyFactory = _db.CreateKeyFactory("__namespace__");
// List all the namespaces between a lower and upper bound.
string lowerBound = _db.NamespaceId.Substring(0,
    _db.NamespaceId.Length - 1);
string upperBound = _db.NamespaceId + "z";
Key startNamespace = keyFactory.CreateKey(lowerBound);
Key endNamespace = keyFactory.CreateKey(upperBound);
Query query = new Query("__namespace__")
{
    Filter = Filter.And(
        Filter.GreaterThan("__key__", startNamespace),
        Filter.LessThan("__key__", endNamespace))
};
var namespaces = new List<string>();
foreach (Entity entity in _db.RunQuery(query).Entities)
{
    namespaces.Add(entity.Key.Path[0].Name);
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
func metadataNamespaces(w io.Writer, projectID string) error {
 // projectID := "my-project"

 ctx := context.Background()
 client, err := datastore.NewClient(ctx, projectID)
 if err != nil {
     return fmt.Errorf("datastore.NewClient: %w", err)
 }
 defer client.Close()

 start := datastore.NameKey("__namespace__", "g", nil)
 end := datastore.NameKey("__namespace__", "h", nil)
 query := datastore.NewQuery("__namespace__").
     FilterField("__key__", ">=", start).
     FilterField("__key__", "<", end).
     KeysOnly()
 keys, err := client.GetAll(ctx, query, nil)
 if err != nil {
     return fmt.Errorf("client.GetAll: %w", err)
 }

 fmt.Fprintln(w, "Namespaces:")
 for _, k := range keys {
     fmt.Fprintf(w, "\t%v", k.Name)
 }
 return nil
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
KeyFactory keyFactory = datastore.newKeyFactory().setKind("__namespace__");
Key startNamespace = keyFactory.newKey("g");
Key endNamespace = keyFactory.newKey("h");
Query<Key> query =
    Query.newKeyQueryBuilder()
        .setKind("__namespace__")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.gt("__key__", startNamespace),
                PropertyFilter.lt("__key__", endNamespace)))
        .build();
List<String> namespaces = new ArrayList<>();
QueryResults<Key> results = datastore.run(query);
while (results.hasNext()) {
  namespaces.add(results.next().getName());
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runNamespaceQuery(startNamespace, endNamespace) {
  const startKey = datastore.key(['__namespace__', startNamespace]);
  const endKey = datastore.key(['__namespace__', endNamespace]);

  const query = datastore
    .createQuery('__namespace__')
    .select('__key__')
    .filter(
      and([
        new PropertyFilter('__key__', '>=', startKey),
        new PropertyFilter('__key__', '<', endKey),
      ]),
    );

  const [entities] = await datastore.runQuery(query);
  const namespaces = entities.map(entity => entity[datastore.KEY].name);

  console.log('Namespaces:');
  namespaces.forEach(namespace => console.log(namespace));

  return namespaces;
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('__namespace__')
    ->projection(['__key__'])
    ->filter('__key__', '>=', $datastore->key('__namespace__', $start))
    ->filter('__key__', '<', $datastore->key('__namespace__', $end));
$result = $datastore->runQuery($query);
/* @var array<string> $namespaces */
$namespaces = [];
foreach ($result as $namespace) {
    $namespaces[] = $namespace->key()->pathEnd()['name'];
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

# All namespaces
query = client.query(kind="__namespace__")
query.keys_only()

all_namespaces = [entity.key.id_or_name for entity in query.fetch()]

# Filtered namespaces
start_namespace = client.key("__namespace__", "g")
end_namespace = client.key("__namespace__", "h")
query = client.query(kind="__namespace__")
query.key_filter(start_namespace, ">=")
query.key_filter(end_namespace, "<")

filtered_namespaces = [entity.key.id_or_name for entity in query.fetch()]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("__namespace__")
                 .select("__key__")
                 .where("__key__", ">=", datastore.key("__namespace__", "g"))
                 .where("__key__", "<", datastore.key("__namespace__", "h"))

namespaces = datastore.run(query).map do |entity|
  entity.key.name
end
```

### GQL

``` text
SELECT __key__ FROM __namespace__
WHERE __key__ >= KEY(__namespace__, 'namespace-a')
  AND __key__ <  KEY(__namespace__, 'namespace-b')
```

## Kind queries

*Kind queries* return entities of kind `  __kind__  ` whose key name is the name of an entity kind. Queries of this type are implicitly restricted to the current namespace and support filtering only for ranges over the `  __key__  ` pseudoproperty. The results can be sorted by ascending (but not descending) `  __key__  ` value. Because `  __kind__  ` entities have no properties, both keys-only and non-keys-only queries return the same information.

The following example prints a list of the kinds used in an application:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("__kind__");
var kinds = new List<string>();
foreach (Entity entity in _db.RunQuery(query).Entities)
{
    kinds.Add(entity.Key.Path[0].Name);
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("__kind__").KeysOnly()
keys, err := client.GetAll(ctx, query, nil)
if err != nil {
 log.Fatalf("client.GetAll: %v", err)
}

kinds := make([]string, 0, len(keys))
for _, k := range keys {
 kinds = append(kinds, k.Name)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Key> query = Query.newKeyQueryBuilder().setKind("__kind__").build();
List<String> kinds = new ArrayList<>();
QueryResults<Key> results = datastore.run(query);
while (results.hasNext()) {
  kinds.add(results.next().getName());
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runKindQuery() {
  const query = datastore.createQuery('__kind__').select('__key__');

  const [entities] = await datastore.runQuery(query);
  const kinds = entities.map(entity => entity[datastore.KEY].name);

  console.log('Kinds:');
  kinds.forEach(kind => console.log(kind));

  return kinds;
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('__kind__')
    ->projection(['__key__']);
$result = $datastore->runQuery($query);
/* @var array<string> $kinds */
$kinds = [];
foreach ($result as $kind) {
    $kinds[] = $kind->key()->pathEnd()['name'];
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query = client.query(kind="__kind__")
query.keys_only()

kinds = [entity.key.id_or_name for entity in query.fetch()]
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("__kind__")
                 .select("__key__")

kinds = datastore.run(query).map do |entity|
  entity.key.name
end
```

### GQL

``` text
SELECT __key__ FROM __kind__
```

## Property queries

*Property queries* return entities of kind `  __property__  ` denoting the indexed properties associated with an entity kind. (Unindexed properties are not included.) The entity representing property *p* of kind *k* is built as follows:

  - The entity's key has kind `  __property__  ` and key name *p* .
  - The entity's parent key has kind `  __kind__  ` and key name *k* .
  - The entity's `  property_representation  ` array property contains all the property's [representations](#property_queries_property_representations) .

For example, if your database contains exactly two `  Task  ` entities with `  name  ` and `  done  ` properties:

``` text
Key: 'Task:1'
name: 'Read some properties'
done: true

Key: 'Task:2'
name: 'Climb'
done: null
```

then the two entities returned by a `  __property__  ` query will be:

``` text
Key: '__kind__:Task/__property__:name'
property_representation: [ 'STRING' ]

Key: '__kind__:Task/__property__:done'
property_representation: [ 'BOOLEAN', 'NULL' ]
```

Property queries are implicitly restricted to the current namespace, and support limited [filtering](#property_queries_filtering) with an ancestor or a range over the `  __key__  ` pseudoproperty.

A *keys-only* property query is more efficient than a non-keys-only query, as it does not need to collect the property's representations. The following example retrieves the names of all of an application's entity kinds and the properties associated with each:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("__property__");
var properties = new List<string>();
foreach (Entity entity in _db.RunQuery(query).Entities)
{
    string kind = entity.Key.Path[0].Name;
    string property = entity.Key.Path[1].Name;
    if (kind == "Task")
        properties.Add(property);
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("__property__").KeysOnly()
keys, err := client.GetAll(ctx, query, nil)
if err != nil {
 log.Fatalf("client.GetAll: %v", err)
}

props := make(map[string][]string) // Map from kind to slice of properties.
for _, k := range keys {
 prop := k.Name
 kind := k.Parent.Name
 props[kind] = append(props[kind], prop)
}
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Key> query = Query.newKeyQueryBuilder().setKind("__property__").build();
QueryResults<Key> keys = datastore.run(query);
Map<String, Collection<String>> propertiesByKind = new HashMap<>();
while (keys.hasNext()) {
  Key key = keys.next();
  String kind = key.getParent().getName();
  String propertyName = key.getName();
  Collection<String> properties = propertiesByKind.get(kind);
  if (properties == null) {
    properties = new HashSet<>();
    propertiesByKind.put(kind, properties);
  }
  properties.add(propertyName);
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runPropertyQuery() {
  const query = datastore.createQuery('__property__').select('__key__');
  const [entities] = await datastore.runQuery(query);
  // @TODO convert below object to map
  const propertiesByKind = {};

  entities.forEach(entity => {
    const key = entity[datastore.KEY];
    const kind = key.path[1];
    const property = key.path[3];

    propertiesByKind[kind] = propertiesByKind[kind] || [];
    propertiesByKind[kind].push(property);
  });

  console.log('Properties by Kind:');
  for (const key in propertiesByKind) {
    console.log(key, propertiesByKind[key]);
  }

  return propertiesByKind;
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('__property__')
    ->projection(['__key__']);
$result = $datastore->runQuery($query);
/* @var array<string> $properties */
$properties = [];
/* @var Entity $entity */
foreach ($result as $entity) {
    $kind = $entity->key()->path()[0]['name'];
    $propertyName = $entity->key()->path()[1]['name'];
    $properties[] = "$kind.$propertyName";
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

from collections import defaultdict

query = client.query(kind="__property__")
query.keys_only()

properties_by_kind = defaultdict(list)

for entity in query.fetch():
    kind = entity.key.parent.name
    property_ = entity.key.name

    properties_by_kind[kind].append(property_)
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("__property__")
                 .select("__key__")

entities = datastore.run query
properties_by_kind = entities.each_with_object({}) do |entity, memo|
  kind = entity.key.parent.name
  prop = entity.key.name
  memo[kind] ||= []
  memo[kind] << prop
end
```

### GQL

``` text
SELECT __key__ FROM __property__
```

### Property queries: property representations

Non-keys-only property queries, known as *property representation queries* , return additional information on the value types used for each property. The `  property_representation  ` property in the entity representing property *p* of kind *k* is an array containing all *representations* of *p* 's value in any entity of kind *k* .

Each [value](/datastore/docs/concepts/entities#properties_and_value_types) has the following *representation* (note that some value types share representations):

<table>
<thead>
<tr class="header">
<th>Value type</th>
<th>Representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Integer</td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="even">
<td>Floating-point number</td>
<td><code dir="ltr" translate="no">       DOUBLE      </code></td>
</tr>
<tr class="odd">
<td>Boolean</td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
</tr>
<tr class="even">
<td>Text string</td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td>Byte string</td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td>Date and time</td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td>Datastore key</td>
<td><code dir="ltr" translate="no">       REFERENCE      </code></td>
</tr>
<tr class="even">
<td>Embedded entity</td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td>Array</td>
<td>representation of the array's elements</td>
</tr>
<tr class="even">
<td>Geographical point</td>
<td><code dir="ltr" translate="no">       POINT      </code></td>
</tr>
<tr class="odd">
<td>Null</td>
<td><code dir="ltr" translate="no">       NULL      </code></td>
</tr>
</tbody>
</table>

The following example finds all representations of properties of kind `  Task  ` , using an [ancestor property query](#property_queries_filtering) :

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key key = _db.CreateKeyFactory("__kind__").CreateKey("Task");
Query query = new Query("__property__")
{
    Filter = Filter.HasAncestor(key)
};
var properties = new List<string>();
foreach (Entity entity in _db.RunQuery(query).Entities)
{
    string kind = entity.Key.Path[0].Name;
    string property = entity.Key.Path[1].Name;
    var representations = entity["property_representation"]
        .ArrayValue.Values.Select(x => x.StringValue)
        .OrderBy(x => x);
    properties.Add($"{property}:" +
        string.Join(",", representations));
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
kindKey := datastore.NameKey("__kind__", "Task", nil)
query := datastore.NewQuery("__property__").Ancestor(kindKey)

type Prop struct {
 Repr []string `datastore:"property_representation"`
}

var props []Prop
keys, err := client.GetAll(ctx, query, &props)
```

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key key = datastore.newKeyFactory().setKind("__kind__").newKey("Task");
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("__property__")
        .setFilter(PropertyFilter.hasAncestor(key))
        .build();
QueryResults<Entity> results = datastore.run(query);
Map<String, Collection<String>> representationsByProperty = new HashMap<>();
while (results.hasNext()) {
  Entity result = results.next();
  String propertyName = result.getKey().getName();
  List<StringValue> representations = result.getList("property_representation");
  Collection<String> currentRepresentations = representationsByProperty.get(propertyName);
  if (currentRepresentations == null) {
    currentRepresentations = new HashSet<>();
    representationsByProperty.put(propertyName, currentRepresentations);
  }
  for (StringValue value : representations) {
    currentRepresentations.add(value.get());
  }
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runPropertyByKindQuery() {
  const ancestorKey = datastore.key(['__kind__', 'Account']);

  const query = datastore
    .createQuery('__property__')
    .hasAncestor(ancestorKey);
  const [entities] = await datastore.runQuery(query);

  const representationsByProperty = {};

  entities.forEach(entity => {
    const key = entity[datastore.KEY];
    const propertyName = key.name;
    const propertyType = entity.property_representation;

    representationsByProperty[propertyName] = propertyType;
  });

  console.log('Task property representations:');
  for (const key in representationsByProperty) {
    console.log(key, representationsByProperty[key]);
  }

  return representationsByProperty;
}
```

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$ancestorKey = $datastore->key('__kind__', 'Task');
$query = $datastore->query()
    ->kind('__property__')
    ->hasAncestor($ancestorKey);
$result = $datastore->runQuery($query);
/* @var array<string,string> $properties */
$properties = [];
/* @var Entity $entity */
foreach ($result as $entity) {
    $propertyName = $entity->key()->path()[1]['name'];
    $propertyType = $entity['property_representation'];
    $properties[$propertyName] = $propertyType;
}
// Example values of $properties: ['description' => ['STRING']]
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

ancestor = client.key("__kind__", "Task")
query = client.query(kind="__property__", ancestor=ancestor)

representations_by_property = {}

for entity in query.fetch():
    property_name = entity.key.name
    property_types = entity["property_representation"]

    representations_by_property[property_name] = property_types
```

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
ancestor_key = datastore.key "__kind__", "Task"
query = datastore.query("__property__")
                 .ancestor(ancestor_key)

entities = datastore.run query
representations = entities.each_with_object({}) do |entity, memo|
  property_name = entity.key.name
  property_types = entity["property_representation"]
  memo[property_name] = property_types
end
```

### GQL

``` text
SELECT * FROM __property__
WHERE __key__ HAS ANCESTOR KEY(__kind__, 'Task')
```

### Property queries: filtering

Property queries support ancestor filtering on a `  __kind__  ` or `  __property__  ` key, to limit the query results to a single kind or property, as seen in the property representation query above.

Property queries can also be filtered with a range over the pseudoproperty `  __key__  ` , where the keys denote either `  __kind__  ` or `  __property__  ` entities. The results can be sorted by ascending (but not descending) `  __key__  ` value. Filtering is applied to kind-property pairs, ordered first by kind and second by property. For instance, suppose you have entities with these properties:

  - kind `  Task  ` with properties
      - `  created  `
      - `  priority  `
      - `  tags  `
  - kind `  TaskList  ` with properties
      - `  created  `

The following keys-only property query:

### C\#

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Key key = _db.CreateKeyFactory("__kind__").CreateKey("Task");
Key startKey = new KeyFactory(key, "__property__")
    .CreateKey("priority");
Query query = new Query("__property__")
{
    Filter = Filter.GreaterThanOrEqual("__key__", startKey)
};
var properties = new List<string>();
foreach (Entity entity in _db.RunQuery(query).Entities)
{
    string kind = entity.Key.Path[0].Name;
    string property = entity.Key.Path[1].Name;
    properties.Add($"{kind}.{property}");
};
```

### Go

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Java

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Key startKey =
    datastore
        .newKeyFactory()
        .setKind("__property__")
        .addAncestors(PathElement.of("__kind__", "Task"))
        .newKey("priority");
Query<Key> query =
    Query.newKeyQueryBuilder()
        .setKind("__property__")
        .setFilter(PropertyFilter.ge("__key__", startKey))
        .build();
Map<String, Collection<String>> propertiesByKind = new HashMap<>();
QueryResults<Key> keys = datastore.run(query);
while (keys.hasNext()) {
  Key key = keys.next();
  String kind = key.getParent().getName();
  String propertyName = key.getName();
  Collection<String> properties = propertiesByKind.get(kind);
  if (properties == null) {
    properties = new HashSet<String>();
    propertiesByKind.put(kind, properties);
  }
  properties.add(propertyName);
}
```

### Node.js

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### PHP

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$ancestorKey = $datastore->key('__kind__', 'Task');
$startKey = $datastore->key('__property__', 'priority')
    ->ancestorKey($ancestorKey);
$query = $datastore->query()
    ->kind('__property__')
    ->filter('__key__', '>=', $startKey);
$result = $datastore->runQuery($query);
/* @var array<string> $properties */
$properties = [];
/* @var Entity $entity */
foreach ($result as $entity) {
    $kind = $entity->key()->path()[0]['name'];
    $propertyName = $entity->key()->path()[1]['name'];
    $properties[] = "$kind.$propertyName";
}
```

### Python

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

Not Applicable

### Ruby

To learn how to install and use the client library for Cloud Datastore, see [Cloud Datastore client libraries](/datastore/docs/reference/libraries) . For more information, see the [Cloud Datastore Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Cloud Datastore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
start_key = datastore.key [["__kind__", "Task"], ["__property__", "priority"]]
query = datastore.query("__property__")
                 .select("__key__")
                 .where("__key__", ">=", start_key)

entities = datastore.run query
properties_by_kind = entities.each_with_object({}) do |entity, memo|
  kind = entity.key.parent.name
  prop = entity.key.name
  memo[kind] ||= []
  memo[kind] << prop
end
```

### GQL

``` text
SELECT __key__ FROM __property__
WHERE __key__ >= KEY(__kind__, 'Task', __property__, 'priority')
```

will collect the following kind, property name pairs:

``` text
Task, priority
Task, tags
TaskList, created
```

Notice that the results include properties from kinds `  Task  ` and `  TaskList  ` , but do not include the `  created  ` property of kind `  Task  ` , because it falls outside the range specified for the query.

**Note:** Since the `  __key__  ` kind filters on kind-property pairs, you can't use a single query for the same property name in different kinds. You can query for all properties in all kinds (or in a range of kinds), but you cannot construct a single query that retrieves, for example, all properties with names between *m* and *q* in all kinds (or in kinds *A* and *B* ).
