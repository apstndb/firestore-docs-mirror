---
name: documents/docs.cloud.google.com/datastore/docs/reference/data/rpc/google.type
uri: https://docs.cloud.google.com/datastore/docs/reference/data/rpc/google.type
title: Package google.type
description: A highly-scalable NoSQL database for your web and mobile applications that automatically handles sharding and replication.
data_source: docs.cloud.google.com
update_time: "2025-10-17T22:06:14Z"
---

## Index

  - `  LatLng  ` (message)

## LatLng

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

Fields

`latitude`

`double`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude`

`double`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].
