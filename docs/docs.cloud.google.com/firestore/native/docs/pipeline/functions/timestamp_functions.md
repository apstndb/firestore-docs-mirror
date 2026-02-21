# Timestamp Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Timestamp Functions**

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Description</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         CURRENT_TIMESTAMP       </code></td>
<td>Generates a <code dir="ltr" translate="no">       TIMESTAMP      </code> corresponding to the request time.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TRUNC       </code></td>
<td>Truncates a <code dir="ltr" translate="no">       TIMESTAMP      </code> to a given granularity.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNIX_MICROS_TO_TIMESTAMP       </code></td>
<td>Converts the number of microseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         UNIX_MILLIS_TO_TIMESTAMP       </code></td>
<td>Converts the number of milliseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         UNIX_SECONDS_TO_TIMESTAMP       </code></td>
<td>Converts the number of seconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code> to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_ADD       </code></td>
<td>Adds a time interval to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_SUB       </code></td>
<td>Subtracts a time interval to a <code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_MICROS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of microseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_MILLIS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of milliseconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         TIMESTAMP_TO_UNIX_SECONDS       </code></td>
<td>Converts a <code dir="ltr" translate="no">       TIMESTAMP      </code> to the number of seconds since <code dir="ltr" translate="no">       1970-01-01 00:00:00 UTC      </code></td>
</tr>
</tbody>
</table>

### CURRENT\_TIMESTAMP

**Syntax:**

``` text
current_timestamp() -> TIMESTAMP
```

**Description:**

Gets the timestamp at the beginning of request time `  input  ` (interpreted as the number of microseconds since `  1970-01-01 00:00:00 UTC  ` ).

This is stable within a query, and will always resolve to the same value if called multiple times.

### TIMESTAMP\_TRUNC

**Syntax:**

``` text
timestamp_trunc(timestamp: TIMESTAMP, granularity: STRING[, timezone: STRING]) -> TIMESTAMP
```

**Description:**

Truncates a timestamp down to a given granularity.

The `  granularity  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `
  - `  week  `
  - `  week([weekday])  `
  - `  month  `
  - `  quarter  `
  - `  year  `
  - `  isoyear  `

If the `  timezone  ` argument is provided, truncation will be based on the given timezone's calendar boundaries (e.g. day truncation will truncate to midnight in the given timezone). The truncation will respect daylight savings time.

If `  timezone  ` is not provided, truncation will be based on `  UTC  ` calendar boundaries.

The `  timezone  ` argument should be a string representation of a timezone from the tz database, for example `  America/New_York  ` . A custom time offset can also be used by specifying an offset from `  GMT  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       granularity      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timezone      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_trunc(timestamp, granularity, timezone)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2000-01-01 10:20:30:123456 UTC</td>
<td style="text-align: left;">"second"</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">2001-01-01 10:20:30 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">1997-05-31 04:30:30 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">1997-05-31 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1997-05-31 04:30:30 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">"America/Los_Angeles"</td>
<td style="text-align: left;">1997-05-30 07:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2001-03-16 04:00:00 UTC</td>
<td style="text-align: left;">"week(friday)</td>
<td style="text-align: left;">Not provided</td>
<td style="text-align: left;">2001-03-16 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2001-03-23 04:00:00 UTC</td>
<td style="text-align: left;">"week(friday)</td>
<td style="text-align: left;">"America/Los_Angeles"</td>
<td style="text-align: left;">2001-03-23 17:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2026-01-24 20:00:00 UTC</td>
<td style="text-align: left;">"month"</td>
<td style="text-align: left;">"GMT+06:32:43"</td>
<td style="text-align: left;">2026-01-01T06:32:43 UTC</td>
</tr>
</tbody>
</table>

### UNIX\_MICROS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_micros_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of microseconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_micros_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">400123456L</td>
<td style="text-align: left;">1970-01-01 00:06:40.123456 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1000000L</td>
<td style="text-align: left;">1969-12-31 23:59:59 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtMicros")
        .unix_micros_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixMicrosToTimestamp(field("createdAtMicros")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### UNIX\_MILLIS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_millis_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of milliseconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_millis_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">4000123L</td>
<td style="text-align: left;">1970-01-01 01:06:40.123 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-1000000L</td>
<td style="text-align: left;">1969-12-31 23:43:20 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtMillis")
        .unix_millis_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixMillisToTimestamp(field("createdAtMillis")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### UNIX\_SECONDS\_TO\_TIMESTAMP

**Syntax:**

``` text
unix_seconds_to_timestamp(input: INT64) -> TIMESTAMP
```

**Description:**

Converts `  input  ` (interpreted as the number of seconds since `  1970-01-01 00:00:00 UTC  ` ) to a `  TIMESTAMP  ` . Throws an `  error  ` if `  input  ` cannot be converted to a valid `  TIMESTAMP  ` .

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unix_seconds_to_timestamp(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">0L</td>
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">60L</td>
<td style="text-align: left;">1970-01-01 00:01:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">-300L</td>
<td style="text-align: left;">1969-12-31 23:55:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("createdAtSeconds")
        .unix_seconds_to_timestamp()
        .as_("createdAtString")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(unixSecondsToTimestamp(field("createdAtSeconds")).as("createdAtString"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_ADD

**Syntax:**

``` text
timestamp_add(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP
```

**Description:**

Adds an `  amount  ` of `  unit  ` from `  timestamp  ` . The `  amount  ` argument can be negative, in that case it is equivalent to [TIMESTAMP\_SUB](#timestamp_sub) .

The `  unit  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `

Throws an error if the resulting timestamp does not fit within the `  TIMESTAMP  ` range.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unit      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       amount      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_add(timestamp, unit, amount)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"minute"</td>
<td style="text-align: left;">2L</td>
<td style="text-align: left;">2025-02-20 00:02:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"hour"</td>
<td style="text-align: left;">-4L</td>
<td style="text-align: left;">2025-02-19 20:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2025-02-20 00:00:00 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">5L</td>
<td style="text-align: left;">2025-02-25 00:00:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("createdAt").timestampAdd("day", 3653).as("expiresAt")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("createdAt").timestampAdd("day", 3653).as("expiresAt")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("createdAt").timestampAdd(3653, .day).as("expiresAt")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAt")
          .timestampAdd("day", 3653)
          .alias("expiresAt")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("createdAt").timestampAdd("day", 3653).alias("expiresAt")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("createdAt").timestamp_add("day", 3653).as_("expiresAt"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampAdd(field("createdAt"), "day", 3653).as("expiresAt"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_SUB

**Syntax:**

``` text
timestamp_sub(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP
```

**Description:**

Subtracts an `  amount  ` of `  unit  ` from `  timestamp  ` . The `  amount  ` argument can be negative, in that case it is equivalent to [TIMESTAMP\_ADD](#timestamp_add) .

The `  unit  ` argument must be a string and one of the following:

  - `  microsecond  `
  - `  millisecond  `
  - `  second  `
  - `  minute  `
  - `  hour  `
  - `  day  `

Throws an error if the resulting timestamp does not fit within the `  TIMESTAMP  ` range.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       unit      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       amount      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_sub(timestamp, unit, amount)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"minute"</td>
<td style="text-align: left;">40L</td>
<td style="text-align: left;">2026-07-03 23:20:00 UTC</td>
</tr>
<tr class="even">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"hour"</td>
<td style="text-align: left;">-24L</td>
<td style="text-align: left;">2026-07-05 00:00:00 UTC</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2026-07-04 00:00:00 UTC</td>
<td style="text-align: left;">"day"</td>
<td style="text-align: left;">3L</td>
<td style="text-align: left;">2026-07-01 00:00:00 UTC</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("expiresAt").timestampSubtract(14, .day).as("sendWarningTimestamp")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("expiresAt")
          .timestampSubtract("day", 14)
          .alias("sendWarningTimestamp")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("expiresAt").timestampSubtract("day", 14).alias("sendWarningTimestamp")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(
        Field.of("expiresAt")
        .timestamp_subtract("day", 14)
        .as_("sendWarningTimestamp")
    )
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampSubtract(field("expiresAt"), "day", 14).as("sendWarningTimestamp"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_MICROS

**Syntax:**

``` text
timestamp_to_unix_micros(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of microseconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the microsecond.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_micros(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 00:06:40.123456 UTC</td>
<td style="text-align: left;">400123456L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:59:59 UTC</td>
<td style="text-align: left;">-1000000L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMicros().as("unixMicros")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMicros().as("unixMicros")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixMicros().as("unixMicros")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMicros().alias("unixMicros")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMicros().alias("unixMicros")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_micros().as_("unixMicros"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixMicros(field("dateString")).as("unixMicros"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_MILLIS

**Syntax:**

``` text
timestamp_to_unix_millis(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of milliseconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the millisecond.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_millis(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 01:06:40.123 UTC</td>
<td style="text-align: left;">4000123L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:43:20</td>
<td style="text-align: left;">-1000000L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMillis().as("unixMillis")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixMillis().as("unixMillis")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixMillis().as("unixMillis")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMillis().alias("unixMillis")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixMillis().alias("unixMillis")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_millis().as_("unixMillis"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixMillis(field("dateString")).as("unixMillis"))
        .execute()
        .get();PipelineSnippets.java
```

### TIMESTAMP\_TO\_UNIX\_SECONDS

**Syntax:**

``` text
timestamp_to_unix_seconds(input: TIMESTAMP) -> INT64
```

**Description:**

Converts `  input  ` to the number of seconds since `  1970-01-01 00:00:00 UTC  ` . Truncates higher levels of precision by rounding down to the beginning of the second.

**Examples:**

<table>
<thead>
<tr class="header">
<th style="text-align: left;"><code dir="ltr" translate="no">       input      </code></th>
<th style="text-align: left;"><code dir="ltr" translate="no">       timestamp_to_unix_seconds(input)      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1970-01-01 00:00:00 UTC</td>
<td style="text-align: left;">0L</td>
</tr>
<tr class="even">
<td style="text-align: left;">1970-01-01 00:01:00 UTC</td>
<td style="text-align: left;">60L</td>
</tr>
<tr class="odd">
<td style="text-align: left;">1969-12-31 23:55:00 UTC</td>
<td style="text-align: left;">-300L</td>
</tr>
</tbody>
</table>

##### Node.js

``` javascript
const result = await db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixSeconds().as("unixSeconds")
  )
  .execute();test.firestore.js
```

### Web

``` javascript
const result = await execute(db.pipeline()
  .collection("documents")
  .select(
    field("dateString").timestampToUnixSeconds().as("unixSeconds")
  )
);test.firestore.js
```

##### Swift

``` swift
let result = try await db.pipeline()
  .collection("documents")
  .select([
    Field("dateString").timestampToUnixSeconds().as("unixSeconds")
  ])
  .execute()PipelineSnippets.swift
```

##### Kotlin  
Android

``` kotlin
val result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixSeconds().alias("unixSeconds")
    )
    .execute()DocSnippets.kt
```

##### Java  
Android

``` text
Task<Pipeline.Snapshot> result = db.pipeline()
    .collection("documents")
    .select(
        field("dateString").timestampToUnixSeconds().alias("unixSeconds")
    )
    .execute();DocSnippets.java
```

##### Python

``` python
from google.cloud.firestore_v1.pipeline_expressions import Field

result = (
    client.pipeline()
    .collection("documents")
    .select(Field.of("dateString").timestamp_to_unix_seconds().as_("unixSeconds"))
    .execute()
)firestore_pipelines.py
```

##### Java

``` java
Pipeline.Snapshot result =
    firestore
        .pipeline()
        .collection("documents")
        .select(timestampToUnixSeconds(field("dateString")).as("unixSeconds"))
        .execute()
        .get();PipelineSnippets.java
```

## What's next

  - See the [Pipeline Queries overview](/firestore/docs/pipeline/overview)
