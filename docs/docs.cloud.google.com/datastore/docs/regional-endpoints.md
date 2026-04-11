This page describes how to configure the Firestore in Datastore mode client libraries to use a regional or multi-regional endpoint.

When you use Firestore in Datastore mode client libraries, you can use any of the following endpoints:

  - **Global endpoint** : By default, the Firestore in Datastore mode client libraries send API requests to a global service endpoint named `datastore.googleapis.com` . The global service endpoint routes the request to your database. During routing, the request might pass through a server in a location that's different from your database location.

  - **Regional endpoint** : A regional endpoint enforces restrictions ensuring that data is transmitted, stored and processed in a specified Google Cloud region. To ensure that the service endpoint processes your app's Firestore in Datastore mode requests in the same region as your database, specify a *regional endpoint* in the client library.

  - **Multi-regional endpoint** : A multi-regional endpoint enforces restrictions ensuring that data is transmitted, stored and processed in a specified Google Cloud multi-region. To ensure that the service endpoint processes your app's Firestore in Datastore mode requests in the same multi-region as your database, specify a *multi-regional endpoint* in the client library.

## Set a regional or multi-regional endpoint

The method for configuring a regional or multi-regional endpoint is the same: you provide the endpoint string when initializing the client library. The following examples show how to set the endpoint string using a regional endpoint ( `datastore.us-central1.rep.googleapis.com` ). To use a multi-regional endpoint, provide a multi-regional endpoint string corresponding to your database's location (for example, `datastore.us.rep.googleapis.com` for `nam5` ).

**Note:** Setting an endpoint for a location other than where your data resides might result in a `PermissionDeniedError` .

### Java

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Java API reference documentation](https://cloud.google.com/java/docs/reference/google-cloud-datastore/latest/history) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.datastore.Datastore;
    import com.google.cloud.datastore.DatastoreOptions;
    
    public class RegionalEndpoint {
    
      public Datastore createClient() throws Exception {
        // Instantiates a client
        DatastoreOptions options =
            DatastoreOptions.newBuilder().setHost("https://datastore.us-central1.rep.googleapis.com").build();
        Datastore datastore = options.getService();
        return datastore;
      }
    }

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](https://docs.cloud.google.com/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    from google.cloud import datastore
    from google.api_core.client_options import ClientOptions
    
    ENDPOINT = "https://datastore.africa-south1.rep.googleapis.com"
    client_options = ClientOptions(api_endpoint=ENDPOINT)
    client = datastore.Client(client_options=client_options)
    
    query = client.query(kind="Task")
    results = list(query.fetch())
    for r in results:
        print(r)

### Regional and multi-regional endpoint semantics

**Regional Endpoints (REP):**

Firestore in Datastore mode supports regional endpoints for the regional locations listed here [Firestore in Datastore mode locations](https://docs.cloud.google.com/datastore/docs/locations#location-r) .

Use the following format to define regional endpoints:

### Java

``` 
    datastore.REGION_NAME.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` 
    datastore.REGION_NAME.rep.googleapis.com
```

### Go

``` 
    datastore.REGION_NAME.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional hostname.

Some examples of hostnames are:

  - `datastore.us-central1.rep.googleapis.com`
  - `datastore.europe-west1.rep.googleapis.com`

**Multi-regional Endpoints (MREP)**

For multi-regional endpoints, use `us` for locations `nam5` and `nam7` , and `eu` for location `eur3` (see [Multi-regional locations](https://docs.cloud.google.com/datastore/docs/locations#location-mr) ).

### Java

``` 
    datastore.us.rep.googleapis.com:443
    datastore.eu.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Python

``` 
    datastore.us.rep.googleapis.com
    datastore.eu.rep.googleapis.com
```

### Go

``` 
    datastore.us.rep.googleapis.com:443
    datastore.eu.rep.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

### Locational Endpoints (Deprecated)

Locational endpoints are now deprecated. Use regional or multi-regional endpoints instead.

Firestore in Datastore mode previously supported locational endpoints with the following format:

### Java

``` 
  https://REGION_NAME-datastore.googleapis.com:443
```

Make sure that the complete `https` URL is used and that the port number is defined along with the endpoint.

### Python

``` 
  https://REGION_NAME-datastore.googleapis.com
```

Make sure that the complete `https` URL is set as the locational endpoint.

### Go

``` 
  REGION_NAME-datastore.googleapis.com:443
```

Make sure that the port number is defined along with the endpoint.

Replace REGION\_NAME with the name of a regional or multi-regional hostnames.

Some examples of hostnames are:

  - `eur3-datastore.googleapis.com`
  - `nam5-datastore.googleapis.com`
  - `europe-west6-datastore.googleapis.com`
  - `asia-northeast2-datastore.googleapis.com`

For a complete list of multi-regional and regional hostnames, see [Firestore in Datastore mode locations](https://docs.cloud.google.com/datastore/docs/locations) .

## Restrict global API endpoint usage

To help enforce the use of regional and multi-regional endpoints, use the `constraints/gcp.restrictEndpointUsage` organization policy constraint to block requests to the global API endpoint. For more information, see [Restrict endpoint usage](https://docs.cloud.google.com/docs/security/compliance/restrict-endpoint-usage) .

## What's next

  - Learn about the Firestore in Datastore mode data model. See [Entities, properties, and keys](https://docs.cloud.google.com/datastore/docs/concepts/entities) .
  - See the [Best practices](https://docs.cloud.google.com/datastore/docs/best-practices) for Firestore in Datastore mode.
