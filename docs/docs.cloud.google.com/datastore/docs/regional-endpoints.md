This page describes how to configure the Firestore in Datastore mode client libraries to use a locational endpoint.

When you use Firestore in Datastore mode client libraries, you can use either of the following endpoints:

  - **Global endpoint** : By default, the Firestore in Datastore mode client libraries send API requests to a global service endpoint named `  datastore.googleapis.com  ` . The global service endpoint routes the request to your database. During routing, the request might pass through a locational service endpoint in a location that's different from your database location.

  - **Locational endpoint** : A locational endpoint enforces regional restrictions, ensuring that data is stored and processed in a specified region. To guarantee that the service endpoint processes your app's Firestore in Datastore mode requests in the same region as your database, specify a *locational endpoint* in the client library.

## Set a locational endpoint

The following examples show how to set a locational endpoint when you initialize a Firestore in Datastore mode client.

**Note:** Setting a locational endpoint other than where your data resides might result in a `  PermissionDeniedError  ` error.

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.datastore.Datastore;
import com.google.cloud.datastore.DatastoreOptions;

public class RegionalEndpoint {

  public Datastore createClient() throws Exception {
    // Instantiates a client
    DatastoreOptions options =
        DatastoreOptions.newBuilder().setHost("https://nam5-datastore.googleapis.com").build();
    Datastore datastore = options.getService();
    return datastore;
  }
}
```

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
ENDPOINT = "https://eur3-datastore.googleapis.com"
client_options = ClientOptions(api_endpoint=ENDPOINT)
client = datastore.Client(client_options=client_options)

query = client.query(kind="Task")
results = list(query.fetch())
for r in results:
    print(r)
```

### Locational endpoint semantics

Firestore in Datastore mode supports locational endpoints for both region and multi-region locations.

Use the following format to define locational endpoints:

### Java

``` text
  https://REGION_NAME-firestore.googleapis.com:443
```

Make sure that the complete `  https  ` URL is used and that the port number is defined along with the endpoint.

### Python

``` text
  https://REGION_NAME-firestore.googleapis.com
```

Make sure that the complete `  https  ` URL is set as the locational endpoint.

### Go

``` text
  REGION_NAME-firestore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional or multi-regional hostnames.

Some examples of hostnames are:

  - `  eur3-datastore.googleapis.com  `
  - `  nam5-datastore.googleapis.com  `
  - `  europe-west6-datastore.googleapis.com  `
  - `  asia-northeast2-datastore.googleapis.com  `

For a complete list of multi-regional and regional hostnames, see [Firestore in Datastore mode locations](/datastore/docs/locations) .

## What's next

  - Learn about the Firestore in Datastore mode data model. See [Entities, properties, and keys](/datastore/docs/concepts/entities) .
  - See the [Best practices](/datastore/docs/best-practices) for Firestore in Datastore mode.
