Run a projection query.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore queries](/datastore/docs/concepts/queries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
Query query = new Query("Task")
{
    Projection = { "priority", "percent_complete" }
};
List<long> priorities = new List<long>();
List<double> percentCompletes = new List<double>();
foreach (var entity in _db.RunQuery(query).Entities)
{
    priorities.Add((long)entity["priority"]);
    percentCompletes.Add((double)entity["percent_complete"]);
}
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
var priorities []int
var percents []float64
it := client.Run(ctx, query)
for {
 var task Task
 if _, err := it.Next(&task); err == iterator.Done {
     break
 } else if err != nil {
     log.Fatal(err)
 }
 priorities = append(priorities, task.Priority)
 percents = append(percents, task.PercentComplete)
}
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
List<Long> priorities = new LinkedList<>();
List<Double> percentCompletes = new LinkedList<>();
QueryResults<ProjectionEntity> tasks = datastore.run(query);
while (tasks.hasNext()) {
  ProjectionEntity task = tasks.next();
  priorities.add(task.getLong("priority"));
  percentCompletes.add(task.getDouble("percent_complete"));
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
async function runProjectionQuery() {
  const priorities = [];
  const percentCompletes = [];
  const [tasks] = await datastore.runQuery(query);
  tasks.forEach(task => {
    priorities.push(task.priority);
    percentCompletes.push(task.percent_complete);
  });

  return {
    priorities: priorities,
    percentCompletes: percentCompletes,
  };
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
$priorities = array();
$percentCompletes = array();
$result = $datastore->runQuery($query);
/* @var Entity $task */
foreach ($result as $task) {
    $priorities[] = $task['priority'];
    $percentCompletes[] = $task['percent_complete'];
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
priorities = []
percent_completes = []

for task in query.fetch():
    priorities.append(task["priority"])
    percent_completes.append(task["percent_complete"])
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
priorities = []
percent_completes = []
datastore.run(query).each do |task|
  priorities << task["priority"]
  percent_completes << task["percent_complete"]
end
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
