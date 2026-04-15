# Configure data locality with regional endpoints

This page describes how to configure the Firestore client libraries to use a regional or multi-regional endpoint.

When you use Firestore client libraries, you can use any of the following endpoints:

  - **Global endpoint** : By default, the Firestore client libraries send API requests to a global service endpoint named `firestore.googleapis.com` . The global service endpoint routes the request to your database. During routing, a request might pass through a server in a location that's different from your database location.

  - **Regional endpoint** : A regional endpoint enforces restrictions ensuring that data is transmitted, stored and processed in a specified Google Cloud region. To ensure that the service endpoint processes your app's Firestore requests in the same region as your database, specify a *regional endpoint* in the client library.

  - **Multi-regional endpoint** : A multi-regional endpoint enforces restrictions ensuring that data is transmitted, stored and processed in a specified Google Cloud multi-region. To ensure that the service endpoint processes your app's Firestore requests in the same multi-region as your database, specify a *multi-regional endpoint* in the client library.

## Set a regional or multi-regional endpoint

The method for configuring a regional or multi-regional endpoint is the same: you provide the endpoint string when initializing the client library. The following examples show how to set the endpoint string using a regional endpoint ( `firestore.us-central1.rep.googleapis.com` ). To use a multi-regional endpoint, provide a multi-regional endpoint string corresponding to your database's location (for example, `firestore.us.rep.googleapis.com` for `nam5` ).

> **Note:** You can set regional and multi-regional endpoints in the server client libraries, namely C\#, Go, Java, Node.js, PHP, Python, and Ruby. The mobile and web SDKs, namely, Android, IOS, and Web are not supported.

> **Note:** Setting an endpoint for a location other than where your data resides might result in a `PermissionDeniedError` .

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

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
                // set endpoint like firestore.us-central1.rep.googleapis.com:443
                .setHost(endpoint)
                .build();
        Firestore dbWithEndpoint = firestoreOptions.getService();
    
        return dbWithEndpoint;
      }
    
    }

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    ENDPOINT = "firestore.africa-south1.rep.googleapis.com"
    client_options = ClientOptions(api_endpoint=ENDPOINT)
    db = firestore.Client(client_options=client_options)
    
    cities_query = db.collection("cities").limit(2).get()
    for r in cities_query:
        print(r)

### Regional and multi-regional endpoint semantics

**Regional Endpoints (REP):**

Firestore supports regional endpoints for the regional locations listed here [Firestore locations](https://docs.cloud.google.com/firestore/docs/locations#location-r) .

Use the following format to define regional endpoints:

### Java

``` 
    firestore.REGION_NAME.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` 
    firestore.REGION_NAME.rep.googleapis.com
```

### Go

``` 
    firestore.REGION_NAME.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional hostname.

Some examples of hostnames are:

  - `firestore.us-central1.rep.googleapis.com`
  - `firestore.europe-west1.rep.googleapis.com`

**Multi-regional Endpoints (MREP)**

For multi-regional endpoints, use `us` for locations `nam5` and `nam7` , and `eu` for location `eur3` (see [Multi-regional locations](https://docs.cloud.google.com/firestore/docs/locations#location-mr) ).

### Java

``` 
    firestore.us.rep.googleapis.com:443
    firestore.eu.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` 
    firestore.us.rep.googleapis.com
    firestore.eu.rep.googleapis.com
```

### Go

``` 
    firestore.us.rep.googleapis.com:443
    firestore.eu.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Limitations

  - Regional and multi-regional endpoints don't support [real-time listeners](https://docs.cloud.google.com/firestore/native/docs/query-data/listen) .

### Locational Endpoints (Deprecated)

Locational endpoints are now deprecated. Use regional or multi-regional endpoints instead.

Firestore previously supported locational endpoints with the following format:

### Java

``` 
  REGION_NAME-firestore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` 
  REGION_NAME-firestore.googleapis.com
```

### Go

``` 
  REGION_NAME-firestore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional or multi-regional hostnames.

Some examples of hostnames are:

  - `eur3-firestore.googleapis.com`
  - `nam5-firestore.googleapis.com`
  - `europe-west6-firestore.googleapis.com`
  - `asia-northeast2-firestore.googleapis.com`

For a complete list of multi-regional and regional hostnames, see [Firestore locations](https://docs.cloud.google.com/firestore/docs/locations) .

## Restrict global API endpoint usage

To help enforce the use of regional and multi-regional endpoints, use the `constraints/gcp.restrictEndpointUsage` organization policy constraint to block requests to the global API endpoint. For more information, see [Restrict endpoint usage](https://docs.cloud.google.com/docs/security/compliance/restrict-endpoint-usage) .

## What's next

  - Learn about the Firestore [data model](https://docs.cloud.google.com/firestore/docs/data-model) .
  - [Best practices](https://docs.cloud.google.com/firestore/docs/best-practices) for using Firestore.
