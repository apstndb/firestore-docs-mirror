Example datastore merged index tag queries

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Optimizing Indexes](/datastore/docs/concepts/optimize-indexes)

## Code sample

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import datastore

# For help authenticating your client, visit
# https://cloud.google.com/docs/authentication/getting-started
client = datastore.Client()

query_tag = client.query(
    kind="Photo",
    filters=[
        ("tag", "=", "family"),
        ("tag", "=", "outside"),
        ("tag", "=", "camping"),
    ],
)

query_owner_size_color_tags = client.query(
    kind="Photo",
    filters=[
        ("owner_id", "=", "user1234"),
        ("size", "=", 2),
        ("coloration", "=", 2),
        ("tag", "=", "family"),
        ("tag", "=", "outside"),
        ("tag", "=", "camping"),
    ],
)
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
