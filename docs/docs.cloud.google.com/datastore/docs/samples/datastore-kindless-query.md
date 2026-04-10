Use a kindless query.

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Datastore queries](https://docs.cloud.google.com/datastore/docs/concepts/queries)

## Code sample

### C\#

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode C\# API reference documentation](https://cloud.google.com/dotnet/docs/reference/Google.Cloud.Datastore.V1/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query query = new Query()
    {
        Filter = Filter.GreaterThan("__key__",
            _keyFactory.CreateKey("aTask"))
    };

### Go

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Go API reference documentation](https://cloud.google.com/go/docs/reference/cloud.google.com/go/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    query := datastore.NewQuery("").FilterField("__key__", ">", lastSeenKey)

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    Query<Entity> query =
        Query.newEntityQueryBuilder().setFilter(PropertyFilter.gt("__key__", lastSeenKey)).build();

### Node.js

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Node.js API reference documentation](https://cloud.google.com/nodejs/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const query = datastore
      .createQuery()
      .filter(new PropertyFilter('__key__', '>', lastSeenKey))
      .limit(1);

### PHP

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode PHP API reference documentation](https://googleapis.github.io/google-cloud-php/#/docs/cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    $query = $datastore->query()
        ->filter('__key__', '>', $lastSeenKey);

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    from google.cloud import datastore
    
    # For help authenticating your client, visit
    # https://cloud.google.com/docs/authentication/getting-started
    client = datastore.Client()
    
    last_seen_key = client.key("Task", "a")
    query = client.query()
    query.key_filter(last_seen_key, ">")

### Ruby

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Ruby API reference documentation](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    query = Google::Cloud::Datastore::Query.new
    query.where "__key__", ">", last_seen_key

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=datastore) .
