Use property types.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Entities, Properties, and Keys](/datastore/docs/concepts/entities)
  - [Indexes](/datastore/docs/concepts/indexes)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

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

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
