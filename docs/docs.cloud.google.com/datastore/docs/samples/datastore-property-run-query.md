Use a property query

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore Metadata](/datastore/docs/concepts/metadataqueries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
