Use Cloud NDB client context to query a Datastore model within a function

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Migrate to Cloud NDB](/appengine/migration-center/standard/python/migrate-to-cloud-ndb)

## Code sample

### Python

To learn how to install and use the client library for Datastore mode, see [Datastore mode client libraries](/datastore/docs/reference/libraries) . For more information, see the [Datastore mode Python API reference documentation](https://cloud.google.com/python/docs/reference/datastore/latest) .

To authenticate to Datastore mode, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
from google.cloud import ndb


class Book(ndb.Model):
    title = ndb.StringProperty()


client = ndb.Client()


def list_books():
    with client.context():
        books = Book.query()
        for book in books:
            print(book.to_dict())
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=datastore) .
