Namespace query.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore Metadata](/datastore/docs/concepts/metadataqueries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("__namespace__")
                 .select("__key__")
                 .where("__key__", ">=", datastore.key("__namespace__", "g"))
                 .where("__key__", "<", datastore.key("__namespace__", "h"))

namespaces = datastore.run(query).map do |entity|
  entity.key.name
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
