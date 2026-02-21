Query property by kind.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore Metadata](/datastore/docs/concepts/metadataqueries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
