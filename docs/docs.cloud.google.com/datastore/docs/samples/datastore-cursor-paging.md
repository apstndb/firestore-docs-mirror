Use cursor paging.

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
    Limit = pageSize,
};
if (!string.IsNullOrEmpty(pageCursor))
    query.StartCursor = ByteString.FromBase64(pageCursor);

return _db.RunQuery(query).EndCursor?.ToBase64();
```

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// cursorStr is a cursor to start querying at.
cursorStr := ""

const pageSize = 5
query := datastore.NewQuery("Tasks").Limit(pageSize)
if cursorStr != "" {
 cursor, err := datastore.DecodeCursor(cursorStr)
 if err != nil {
     log.Fatalf("Bad cursor %q: %v", cursorStr, err)
 }
 query = query.Start(cursor)
}

// Read the tasks.
it := client.Run(ctx, query)
var tasks []Task
for {
 var task Task
 _, err := it.Next(&task)
 if err == iterator.Done {
     break
 }
 if err != nil {
     log.Fatalf("Failed fetching results: %v", err)
 }
 tasks = append(tasks, task)
}

// Get the cursor for the next page of results.
// nextCursor.String can be used as the next page's token.
nextCursor, err := it.Cursor()
```

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
EntityQuery.Builder queryBuilder =
    Query.newEntityQueryBuilder().setKind("Task").setLimit(pageSize);
if (pageCursor != null) {
  queryBuilder.setStartCursor(pageCursor);
}
QueryResults<Entity> tasks = datastore.run(queryBuilder.build());
while (tasks.hasNext()) {
  Entity task = tasks.next();
  // do something with the task
}
Cursor nextPageCursor = tasks.getCursorAfter();
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// By default, google-cloud-node will automatically paginate through all of
// the results that match a query. However, this sample implements manual
// pagination using limits and cursor tokens.
async function runPageQuery(pageCursor) {
  let query = datastore.createQuery('Task').limit(pageSize);

  if (pageCursor) {
    query = query.start(pageCursor);
  }
  const results = await datastore.runQuery(query);
  const entities = results[0];
  const info = results[1];

  if (info.moreResults !== Datastore.NO_MORE_RESULTS) {
    // If there are more results to retrieve, the end cursor is
    // automatically set on `info`. To get this value directly, access
    // the `endCursor` property.
    const results = await runPageQuery(info.endCursor);

    // Concatenate entities
    results[0] = entities.concat(results[0]);
    return results;
  }

  return [entities, info];
}
```

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
/**
 * Fetch a query cursor.
 *
 * @param int $pageSize
 * @param string $pageCursor
 * @param string $namespaceId
 */
function cursor_paging(int $pageSize, string $pageCursor = '', string $namespaceId = null)
{
    $datastore = new DatastoreClient(['namespaceId' => $namespaceId]);
    $query = $datastore->query()
        ->kind('Task')
        ->limit($pageSize)
        ->start($pageCursor);
    $result = $datastore->runQuery($query);
    $nextPageCursor = '';
    $entities = [];
    /* @var Entity $entity */
    foreach ($result as $entity) {
        $nextPageCursor = $entity->cursor();
        $entities[] = $entity;
    }

    printf('Found %s entities', count($entities));

    $entities = [];
    if (!empty($nextPageCursor)) {
        $query = $datastore->query()
          ->kind('Task')
          ->limit($pageSize)
          ->start($nextPageCursor);
        $result = $datastore->runQuery($query);

        foreach ($result as $entity) {
            $entities[] = $entity;
        }

        printf('Found %s entities with next page cursor', count($entities));
    }
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


def get_one_page_of_tasks(cursor=None):
    query = client.query(kind="Task")
    query_iter = query.fetch(start_cursor=cursor, limit=5)
    page = next(query_iter.pages)

    tasks = list(page)
    next_cursor = query_iter.next_page_token

    return tasks, next_cursor
```

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
page_size = 2
query = datastore.query("Task")
                 .limit(page_size)
tasks = datastore.run query

page_cursor = tasks.cursor

query = datastore.query("Task")
                 .limit(page_size)
                 .start(page_cursor)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
