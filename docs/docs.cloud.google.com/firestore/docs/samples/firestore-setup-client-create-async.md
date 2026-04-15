Creating a Firestore client (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)
  - [Getting data](https://docs.cloud.google.com/firestore/native/docs/query-data/get-data)
  - [Quickstart: Create a Firestore database by using a server client library](https://docs.cloud.google.com/firestore/native/docs/create-database-server-client-library)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    from google.cloud import firestore
    
    # The `project` parameter is optional and represents which project the client
    # will act on behalf of. If not supplied, the client falls back to the default
    # project inferred from the environment.
    db = firestore.AsyncClient(project="my-project-id")

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
