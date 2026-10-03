---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/GqlQuery
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/GqlQuery
title: GqlQuery
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/GqlQuery#SCHEMA_REPRESENTATION)

A [GQL query](https://cloud.google.com/datastore/docs/apis/gql/gql_reference) .

**JSON representation**

```
{
  "queryString": string,
  "allowLiterals": boolean,
  "namedBindings": {
    string: {
      object (GqlQueryParameter)
    },
    ...
  },
  "positionalBindings": [
    {
      object (GqlQueryParameter)
    }
  ]
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `queryString`          | `string` A string of the format described [here](https://cloud.google.com/datastore/docs/apis/gql/gql_reference) .                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `allowLiterals`        | `boolean` When false, the query string must not contain any literals and instead must bind all values. For example, `SELECT * FROM Kind WHERE a = 'string literal'` is not allowed, while `SELECT * FROM Kind WHERE a = @value` is.                                                                                                                                                                                                                                                                                                           |
| `namedBindings`        | `map (key: string, value: object ( `[`GqlQueryParameter`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter)` ))` For each non-reserved named binding site in the query string, there must be a named parameter with that name, but not necessarily the inverse. Key must match regex `[A-Za-z_$][A-Za-z_$0-9]*` , must not match regex `__.*__` , and must not be `""` . An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `positionalBindings[]` | `object ( `[`GqlQueryParameter`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/GqlQueryParameter)` )` Numbered binding site @1 references the first numbered parameter, effectively using 1-based indexing, rather than the usual 0. For each binding site numbered i in `queryString` , there must be an i-th numbered parameter. The inverse must also be true.                                                                                                                                             |
