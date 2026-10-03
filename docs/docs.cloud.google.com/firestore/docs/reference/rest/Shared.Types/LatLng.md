---
name: documents/docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/LatLng
uri: https://docs.cloud.google.com/firestore/docs/reference/rest/Shared.Types/LatLng
title: LatLng
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
---

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
