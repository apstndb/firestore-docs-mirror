---
name: documents/docs.cloud.google.com/firestore/docs/reference/rpc/google.type
uri: https://docs.cloud.google.com/firestore/docs/reference/rpc/google.type
title: Package google.type
description: A cloud-hosted NoSQL database that's simple enough for rapid prototyping yet scalable and flexible enough to grow to any size.
data_source: docs.cloud.google.com
update_time: "2025-10-17T23:18:34Z"
---

## Index

  - `  DayOfWeek  ` (enum)
  - `  LatLng  ` (message)

## DayOfWeek

Represents a day of the week.

Enums

`DAY_OF_WEEK_UNSPECIFIED`

The day of the week is unspecified.

`MONDAY`

Monday

`TUESDAY`

Tuesday

`WEDNESDAY`

Wednesday

`THURSDAY`

Thursday

`FRIDAY`

Friday

`SATURDAY`

Saturday

`SUNDAY`

Sunday

## LatLng

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

Fields

`latitude`

`double`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude`

`double`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].
