Use a custom type on the client for Firestore documents (async).

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](https://docs.cloud.google.com/firestore/native/docs/manage-data/add-data)
  - [Query and filter data](https://docs.cloud.google.com/firestore/native/docs/query-data/queries)

## Code sample

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    class City:
        def __init__(self, name, state, country, capital=False, population=0, regions=[]):
            self.name = name
            self.state = state
            self.country = country
            self.capital = capital
            self.population = population
            self.regions = regions
    
        @staticmethod
        def from_dict(source):
            # ...
    
        def to_dict(self):
            # ...
    
        def __repr__(self):
            return f"City(\
                    name={self.name}, \
                    country={self.country}, \
                    population={self.population}, \
                    capital={self.capital}, \
                    regions={self.regions}\
                )"

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](https://docs.cloud.google.com/docs/samples?product=firestore) .
