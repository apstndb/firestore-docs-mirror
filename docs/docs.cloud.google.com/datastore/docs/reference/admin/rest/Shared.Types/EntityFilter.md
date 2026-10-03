---
name: documents/docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/EntityFilter
uri: https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/EntityFilter
title: EntityFilter
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/admin/rest/Shared.Types/EntityFilter#SCHEMA_REPRESENTATION)

Identifies a subset of entities in a project. This is specified as combinations of kinds and namespaces (either or both of which may be all, as described in the following examples). Example usage:

Entire project: kinds=\[\], namespaceIds=\[\]

Kinds Foo and Bar in all namespaces: kinds=\['Foo', 'Bar'\], namespaceIds=\[\]

Kinds Foo and Bar only in the default namespace: kinds=\['Foo', 'Bar'\], namespaceIds=\[''\]

Kinds Foo and Bar in both the default and Baz namespaces: kinds=\['Foo', 'Bar'\], namespaceIds=\['', 'Baz'\]

The entire Baz namespace: kinds=\[\], namespaceIds=\['Baz'\]

**JSON representation**

```
{
  "kinds": [
    string
  ],
  "namespaceIds": [
    string
  ]
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kinds[]`        | `string` If empty, then this represents all kinds.                                                                                                                                                                                                                                                                                   |
| `namespaceIds[]` | `string` An empty list represents all namespaces. This is the preferred usage for projects that don't use namespaces. An empty string element represents the default namespace. This should be used if the project has data in non-default namespaces, but doesn't want to include them. Each namespace in this list must be unique. |
