Filter range by equality and inequality.

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Filter = Filter.And(Filter.Equal("priority", 4),
        Filter.GreaterThan("created", _startDate),
        Filter.LessThan("created", _endDate))
};
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
query := datastore.NewQuery("Task").
 FilterField("Priority", "=", 4).
 FilterField("Done", "=", false).
 FilterField("Created", ">", time.Date(1990, 1, 1, 0, 0, 0, 0, time.UTC)).
 FilterField("Created", "<", time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC))
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
Query<Entity> query =
    Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(
            CompositeFilter.and(
                PropertyFilter.eq("priority", 4),
                PropertyFilter.gt("created", startDate),
                PropertyFilter.lt("created", endDate)))
        .build();
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
const query = datastore
  .createQuery('Task')
  .filter(
    and([
      new PropertyFilter('priority', '=', 4),
      new PropertyFilter('done', '=', false),
      new PropertyFilter('created', '>', new Date('1990-01-01T00:00:00z')),
      new PropertyFilter('created', '<', new Date('2000-12-31T23:59:59z')),
    ]),
  );
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$query = $datastore->query()
    ->kind('Task')
    ->filter('priority', '=', 4)
    ->filter('done', '=', false)
    ->filter('created', '>', new DateTime('1990-01-01T00:00:00z'))
    ->filter('created', '<', new DateTime('2000-12-31T23:59:59z'));
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

import datetime

start_date = datetime.datetime(1990, 1, 1)
end_date = datetime.datetime(2000, 12, 31, 23, 59, 59)
query = client.query(kind="Task")
query.add_filter(filter=datastore.query.PropertyFilter("priority", "=", 4))
query.add_filter(filter=datastore.query.PropertyFilter("done", "=", False))
query.add_filter(filter=datastore.query.PropertyFilter("created", ">", start_date))
query.add_filter(filter=datastore.query.PropertyFilter("created", "<", end_date))
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
query = datastore.query("Task")
                 .where("done", "=", false)
                 .where("priority", "=", 4)
                 .where("created", ">=", Time.utc(1990, 1, 1))
                 .where("created", "<", Time.utc(2000, 1, 1))
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
