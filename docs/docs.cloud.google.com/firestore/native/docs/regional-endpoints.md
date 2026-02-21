# Configure data locality with locational endpoints

This page describes how to configure the Firestore client libraries to use a locational endpoint.

When you use Firestore client libraries, you can use either of the following endpoints:

  - **Global endpoint** : By default, the Firestore client libraries send API requests to a global service endpoint named `  firestore.googleapis.com  ` . The global service endpoint routes the request to your database. During routing, a request might pass through a locational service endpoint in a location that's different from your database location.

  - **Locational endpoint** : A locational endpoint enforces regional restrictions, ensuring that data is stored and processed in a specified region. To guarantee that the service endpoint processes your app's Firestore requests in the same region as your database, specify a *locational endpoint* in the client library.

## Set a locational endpoint

The following examples show how to set a locational endpoint when you initialize a Firestore client. Setting a locational endpoint other than where your data resides might result in a `  PermissionDeniedError  ` error.

**Note:** You can set locational endpoints in the server client libraries, namely C\#, Go, Java, Node.js, PHP, Python, and Ruby. The mobile and web SDKs, namely, Android, IOS, and Web are not supported.

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.auth.oauth2.GoogleCredentials;
import com.google.cloud.firestore.Firestore;
import com.google.cloud.firestore.FirestoreOptions;


/**
 * Demonstrate how to set a regional endpoint.
 */
public class RegionalEndpointSnippets {

  /**
   * Create a client with a regional endpoint.
   **/
  public Firestore regionalEndpoint(String projectId, String endpoint) throws Exception {
    FirestoreOptions firestoreOptions =
        FirestoreOptions.newBuilder()
            .setProjectId(projectId)
            .setCredentials(GoogleCredentials.getApplicationDefault())
            // set endpoint like nam5-firestore.googleapis.com:443
            .setHost(endpoint)
            .build();
    Firestore dbWithEndpoint = firestoreOptions.getService();

    return dbWithEndpoint;
  }

}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
ENDPOINT = "nam5-firestore.googleapis.com"
client_options = ClientOptions(api_endpoint=ENDPOINT)
db = firestore.Client(client_options=client_options)

cities_query = db.collection("cities").limit(2).get()
for r in cities_query:
    print(r)
```

### Locational endpoint semantics

Firestore supports locational endpoints for both region and multi-region locations.

Use the following format to define locational endpoints:

### Java

``` text
  REGION_NAME-firestore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` text
  REGION_NAME-firestore.googleapis.com
```

### Go

``` text
  REGION_NAME-firestore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional or multi-regional hostnames.

Some examples of hostnames are:

  - `  eur3-firestore.googleapis.com  `
  - `  nam5-firestore.googleapis.com  `
  - `  europe-west6-firestore.googleapis.com  `
  - `  asia-northeast2-firestore.googleapis.com  `

For a complete list of multi-regional and regional hostnames, see [Firestore locations](/firestore/docs/locations) .

## Restrict global API endpoint usage

To help enforce the use of regional endpoints, use the `  constraints/gcp.restrictEndpointUsage  ` organization policy constraint to block requests to the global API endpoint. For more information, see [Restricting endpoint usage](/assured-workloads/docs/restrict-endpoint-usage) .

## What's next

  - Learn about the Firestore [data model](/firestore/docs/data-model) .
  - [Best practices](/firestore/docs/best-practices) for using Firestore.
