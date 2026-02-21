This snippet creates the union (logical OR) of two queries, where the results of each query is combined in the final results.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore queries](/datastore/docs/concepts/queries)

## Code sample

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;
import com.google.cloud.datastore.Entity;
import com.google.cloud.datastore.Query;
import com.google.cloud.datastore.QueryResults;
import com.google.cloud.datastore.StructuredQuery.CompositeFilter;
import com.google.cloud.datastore.StructuredQuery.Filter;
import com.google.cloud.datastore.StructuredQuery.PropertyFilter;

public class OrFilterQuery {
  public static void invoke() throws Exception {

    // Instantiates a client
    Datastore datastore = DatastoreOptions.getDefaultInstance().getService();
    String propertyName = "description";

    // Create the two filters
    Filter orFilter =
        CompositeFilter.or(
            PropertyFilter.eq(propertyName, "Feed cats"),
            PropertyFilter.eq(propertyName, "Buy milk"));

    // Build the query
    Query<Entity> query = Query.newEntityQueryBuilder().setKind("Task").setFilter(orFilter).build();

    // Get the results back from Datastore
    QueryResults<Entity> results = datastore.run(query);

    if (!results.hasNext()) {
      throw new Exception("query yielded no results");
    }

    while (results.hasNext()) {
      Entity entity = results.next();
      System.out.printf("Entity: %s%n", entity);
    }
  }
}
```

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
/**
 * TODO(developer): Uncomment these variables before running the sample.
 */
// const projectId = "your Google Cloud project id";

// Imports the Cloud Datastore
const {Datastore, PropertyFilter, or} = require('@google-cloud/datastore');

async function queryFilterOr() {
  // Instantiate the Datastore
  const datastore = new Datastore();
  const query = datastore
    .createQuery('Task')
    .filter(
      or([
        new PropertyFilter('description', '=', 'Buy milk'),
        new PropertyFilter('description', '=', 'Feed cats'),
      ]),
    );

  const [entities] = await datastore.runQuery(query);
  for (const entity of entities) {
    console.log(`Entity found: ${entity['description']}`);
  }
}

queryFilterOr();
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore
from google.cloud.datastore import query


def query_filter_or(project_id: str) -> None:
    """Builds a union of two queries (OR) filter.

    Arguments:
        project_id: your Google Cloud Project ID
    """
    client = datastore.Client(project=project_id)

    or_query = client.query(kind="Task")
    or_filter = query.Or(
        [
            query.PropertyFilter("description", "=", "Buy milk"),
            query.PropertyFilter("description", "=", "Feed cats"),
        ]
    )

    or_query.add_filter(filter=or_filter)

    results = list(or_query.fetch())
    for result in results:
        print(result["description"])
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
