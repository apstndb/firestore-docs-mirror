---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyMask
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyMask
title: PropertyMask
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/v1/PropertyMask#SCHEMA_REPRESENTATION)

The set of arbitrarily nested property paths used to restrict an operation to only a subset of properties in an entity.

**JSON representation**

```
{
  "paths": [
    string
  ]
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `paths[]` | `string` The paths to the properties covered by this mask. A path is a list of property names separated by dots ( `.` ), for example `foo.bar` means the property `bar` inside the entity property `foo` inside the entity associated with this path. If a property name contains a dot `.` or a backslash `\` , then that name must be escaped. A path must not be empty, and may not reference a value inside an [`array value`](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/Value#FIELDS.array_value) . |
