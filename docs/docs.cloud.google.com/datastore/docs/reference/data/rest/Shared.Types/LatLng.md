---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/LatLng
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/LatLng
title: LatLng
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/datastore/docs/reference/data/rest/Shared.Types/LatLng#SCHEMA_REPRESENTATION)

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

**JSON representation**

```
{
  "latitude": number,
  "longitude": number
}
```

| Fields      |                                                                                |
|-------------|--------------------------------------------------------------------------------|
| `latitude`  | `number` The latitude in degrees. It must be in the range \[-90.0, +90.0\].    |
| `longitude` | `number` The longitude in degrees. It must be in the range \[-180.0, +180.0\]. |
