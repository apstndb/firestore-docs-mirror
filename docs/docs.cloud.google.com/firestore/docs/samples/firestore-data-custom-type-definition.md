Use a custom type on the client for Firestore documents

## Explore further

For detailed documentation that includes this code sample, see the following:

  - [Add and update data](/firestore/native/docs/manage-data/add-data)
  - [Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)
  - [Get data with Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/get-data)
  - [Getting data](/firestore/native/docs/query-data/get-data)
  - [Perform simple and compound queries in Cloud Firestore](https://firebase.google.com/docs/firestore/query-data/queries)
  - [Query and filter data](/firestore/native/docs/query-data/queries)

## Code sample

### C\#

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
[FirestoreData]
public class City
{
    [FirestoreProperty]
    public string Name { get; set; }

    [FirestoreProperty]
    public string State { get; set; }

    [FirestoreProperty]
    public string Country { get; set; }

    [FirestoreProperty]
    public bool Capital { get; set; }

    [FirestoreProperty]
    public long Population { get; set; }
}
```

### Go

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
// City represents a city.
type City struct {
 Name       string   `firestore:"name,omitempty"`
 State      string   `firestore:"state,omitempty"`
 Country    string   `firestore:"country,omitempty"`
 Capital    bool     `firestore:"capital,omitempty"`
 Population int64    `firestore:"population,omitempty"`
 Density    int64    `firestore:"density,omitempty"`
 Regions    []string `firestore:"regions,omitempty"`
}
```

### Java

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
public City() {
  // Must have a public no-argument constructor
}

// Initialize all fields of a city
public City(
    String name,
    String state,
    String country,
    Boolean capital,
    Long population,
    List<String> regions) {
  this.name = name;
  this.state = state;
  this.country = country;
  this.capital = capital;
  this.population = population;
  this.regions = regions;
}
```

### PHP

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` php
class City
{
    /** @var string */
    public $name;
    /** @var string */
    public $state;
    /** @var string */
    public $country;
    /** @var bool */
    public $capital;
    /** @var int */
    public $population;
    /** @var array<string> */
    public $regions;

    /**
     * @param array<string> $regions
     */
    public function __construct(
        string $name,
        string $state,
        string $country,
        bool $capital = false,
        int $population = 0,
        array $regions = []
    ) {
        $this->name = $name;
        $this->state = $state;
        $this->country = $country;
        $this->capital = $capital;
        $this->population = $population;
        $this->regions = $regions;
    }

    /**
     * @param array<mixed> $source
     */
    public static function fromArray(array $source): City
    {
        // implementation of fromArray is excluded for brevity
        # ...
    }

    /**
     * @return array<mixed>
     */
    public function toArray(): array
    {
        // implementation of toArray is excluded for brevity
        # ...
    }

    public function __toString()
    {
        // implementation of __toString is excluded for brevity
        # ...
    }
}
```

### Python

To authenticate to Firestore, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
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
```

## What's next

To search and filter code samples for other Google Cloud products, see the [Google Cloud sample browser](/docs/samples?product=firestore) .
