# Timestamp Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Timestamp Functions**

|                                              |                                                                                      |
| -------------------------------------------- | ------------------------------------------------------------------------------------ |
| Name                                         | Description                                                                          |
| `         CURRENT_TIMESTAMP        `         | Generates a `TIMESTAMP` corresponding to the request time.                           |
| `         TIMESTAMP_TRUNC        `           | Truncates a `TIMESTAMP` to a given granularity.                                      |
| `         UNIX_MICROS_TO_TIMESTAMP        `  | Converts the number of microseconds since `1970-01-01 00:00:00 UTC` to a `TIMESTAMP` |
| `         UNIX_MILLIS_TO_TIMESTAMP        `  | Converts the number of milliseconds since `1970-01-01 00:00:00 UTC` to a `TIMESTAMP` |
| `         UNIX_SECONDS_TO_TIMESTAMP        ` | Converts the number of seconds since `1970-01-01 00:00:00 UTC` to a `TIMESTAMP`      |
| `         TIMESTAMP_ADD        `             | Adds a time interval to a `TIMESTAMP`                                                |
| `         TIMESTAMP_SUB        `             | Subtracts a time interval to a `TIMESTAMP`                                           |
| `         TIMESTAMP_TO_UNIX_MICROS        `  | Converts a `TIMESTAMP` to the number of microseconds since `1970-01-01 00:00:00 UTC` |
| `         TIMESTAMP_TO_UNIX_MILLIS        `  | Converts a `TIMESTAMP` to the number of milliseconds since `1970-01-01 00:00:00 UTC` |
| `         TIMESTAMP_TO_UNIX_SECONDS        ` | Converts a `TIMESTAMP` to the number of seconds since `1970-01-01 00:00:00 UTC`      |
| `         TIMESTAMP_DIFF        `            | Returns the whole number of specified `unit` intervals between two `TIMESTAMP` s.    |
| `         TIMESTAMP_EXTRACT        `         | Extracts a specific `part` (e.g. year, month, day) from a `TIMESTAMP` .              |

### CURRENT\_TIMESTAMP

**Syntax:**

    current_timestamp() -> TIMESTAMP

**Description:**

Gets the timestamp at the beginning of request time `input` (interpreted as the number of microseconds since `1970-01-01 00:00:00 UTC` ).

This is stable within a query, and will always resolve to the same value if called multiple times.

### TIMESTAMP\_TRUNC

**Syntax:**

    timestamp_trunc(timestamp: TIMESTAMP, granularity: STRING[, timezone: STRING]) -> TIMESTAMP

**Description:**

Truncates a timestamp down to a given granularity.

The `granularity` argument must be a string and one of the following:

  - `microsecond`
  - `millisecond`
  - `second`
  - `minute`
  - `hour`
  - `day`
  - `week`
  - `week([weekday])`
  - `month`
  - `quarter`
  - `year`
  - `isoyear`

If the `timezone` argument is provided, truncation will be based on the given timezone's calendar boundaries (e.g. day truncation will truncate to midnight in the given timezone). The truncation will respect daylight savings time.

If `timezone` is not provided, truncation will be based on `UTC` calendar boundaries.

The `timezone` argument should be a string representation of a timezone from the tz database, for example `America/New_York` . A custom time offset can also be used by specifying an offset from `GMT` .

**Examples:**

| `timestamp`                    | `granularity` | `timezone`             | `timestamp_trunc(timestamp, granularity, timezone)` |
| :----------------------------- | :------------ | :--------------------- | :-------------------------------------------------- |
| 2000-01-01 10:20:30:123456 UTC | "second"      | Not provided           | 2001-01-01 10:20:30 UTC                             |
| 1997-05-31 04:30:30 UTC        | "day"         | Not provided           | 1997-05-31 00:00:00 UTC                             |
| 1997-05-31 04:30:30 UTC        | "day"         | "America/Los\_Angeles" | 1997-05-30 07:00:00 UTC                             |
| 2001-03-16 04:00:00 UTC        | "week(friday) | Not provided           | 2001-03-16 00:00:00 UTC                             |
| 2001-03-23 04:00:00 UTC        | "week(friday) | "America/Los\_Angeles" | 2001-03-23 17:00:00 UTC                             |
| 2026-01-24 20:00:00 UTC        | "month"       | "GMT+06:32:43"         | 2026-01-01T06:32:43 UTC                             |

### UNIX\_MICROS\_TO\_TIMESTAMP

**Syntax:**

    unix_micros_to_timestamp(input: INT64) -> TIMESTAMP

**Description:**

Converts `input` (interpreted as the number of microseconds since `1970-01-01 00:00:00 UTC` ) to a `TIMESTAMP` . Throws an `error` if `input` cannot be converted to a valid `TIMESTAMP` .

**Examples:**

| `input`    | `unix_micros_to_timestamp(input)` |
| :--------- | :-------------------------------- |
| 0L         | 1970-01-01 00:00:00 UTC           |
| 400123456L | 1970-01-01 00:06:40.123456 UTC    |
| \-1000000L | 1969-12-31 23:59:59 UTC           |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("createdAtMicros").unixMicrosToTimestamp().as("createdAtString")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtMicros").unixMicrosToTimestamp().alias("createdAtString")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(unixMicrosToTimestamp(field("createdAtMicros")).as("createdAtString"))
            .execute()
            .get();PipelineSnippets.java

### UNIX\_MILLIS\_TO\_TIMESTAMP

**Syntax:**

    unix_millis_to_timestamp(input: INT64) -> TIMESTAMP

**Description:**

Converts `input` (interpreted as the number of milliseconds since `1970-01-01 00:00:00 UTC` ) to a `TIMESTAMP` . Throws an `error` if `input` cannot be converted to a valid `TIMESTAMP` .

**Examples:**

| `input`    | `unix_millis_to_timestamp(input)` |
| :--------- | :-------------------------------- |
| 0L         | 1970-01-01 00:00:00 UTC           |
| 4000123L   | 1970-01-01 01:06:40.123 UTC       |
| \-1000000L | 1969-12-31 23:43:20 UTC           |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("createdAtMillis").unixMillisToTimestamp().as("createdAtString")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtMillis").unixMillisToTimestamp().alias("createdAtString")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(unixMillisToTimestamp(field("createdAtMillis")).as("createdAtString"))
            .execute()
            .get();PipelineSnippets.java

### UNIX\_SECONDS\_TO\_TIMESTAMP

**Syntax:**

    unix_seconds_to_timestamp(input: INT64) -> TIMESTAMP

**Description:**

Converts `input` (interpreted as the number of seconds since `1970-01-01 00:00:00 UTC` ) to a `TIMESTAMP` . Throws an `error` if `input` cannot be converted to a valid `TIMESTAMP` .

**Examples:**

| `input` | `unix_seconds_to_timestamp(input)` |
| :------ | :--------------------------------- |
| 0L      | 1970-01-01 00:00:00 UTC            |
| 60L     | 1970-01-01 00:01:00 UTC            |
| \-300L  | 1969-12-31 23:55:00 UTC            |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("createdAtSeconds").unixSecondsToTimestamp().as("createdAtString")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAtSeconds").unixSecondsToTimestamp().alias("createdAtString")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(unixSecondsToTimestamp(field("createdAtSeconds")).as("createdAtString"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_ADD

**Syntax:**

    timestamp_add(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP

**Description:**

Adds an `amount` of `unit` from `timestamp` . The `amount` argument can be negative, in that case it is equivalent to [TIMESTAMP\_SUB](https://docs.cloud.google.com/firestore/native/docs/pipeline/functions/timestamp_functions#timestamp_sub) .

The `unit` argument must be a string and one of the following:

  - `microsecond`
  - `millisecond`
  - `second`
  - `minute`
  - `hour`
  - `day`

Throws an error if the resulting timestamp does not fit within the `TIMESTAMP` range.

**Examples:**

| `timestamp`             | `unit`   | `amount` | `timestamp_add(timestamp, unit, amount)` |
| :---------------------- | :------- | :------- | :--------------------------------------- |
| 2025-02-20 00:00:00 UTC | "minute" | 2L       | 2025-02-20 00:02:00 UTC                  |
| 2025-02-20 00:00:00 UTC | "hour"   | \-4L     | 2025-02-19 20:00:00 UTC                  |
| 2025-02-20 00:00:00 UTC | "day"    | 5L       | 2025-02-25 00:00:00 UTC                  |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("createdAt").timestampAdd("day", 3653).as("expiresAt")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("createdAt").timestampAdd("day", 3653).as("expiresAt")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("createdAt").timestampAdd(3653, .day).as("expiresAt")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAt")
              .timestampAdd("day", 3653)
              .alias("expiresAt")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("createdAt").timestampAdd("day", 3653).alias("expiresAt")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(Field.of("createdAt").timestamp_add("day", 3653).as_("expiresAt"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(timestampAdd(field("createdAt"), "day", 3653).as("expiresAt"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_SUB

**Syntax:**

    timestamp_sub(timestamp: TIMESTAMP, unit: STRING, amount: INT64) -> TIMESTAMP

**Description:**

Subtracts an `amount` of `unit` from `timestamp` . The `amount` argument can be negative, in that case it is equivalent to [TIMESTAMP\_ADD](https://docs.cloud.google.com/firestore/native/docs/pipeline/functions/timestamp_functions#timestamp_add) .

The `unit` argument must be a string and one of the following:

  - `microsecond`
  - `millisecond`
  - `second`
  - `minute`
  - `hour`
  - `day`

Throws an error if the resulting timestamp does not fit within the `TIMESTAMP` range.

**Examples:**

| `timestamp`             | `unit`   | `amount` | `timestamp_sub(timestamp, unit, amount)` |
| :---------------------- | :------- | :------- | :--------------------------------------- |
| 2026-07-04 00:00:00 UTC | "minute" | 40L      | 2026-07-03 23:20:00 UTC                  |
| 2026-07-04 00:00:00 UTC | "hour"   | \-24L    | 2026-07-05 00:00:00 UTC                  |
| 2026-07-04 00:00:00 UTC | "day"    | 3L       | 2026-07-01 00:00:00 UTC                  |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("expiresAt").timestampSubtract("day", 14).as("sendWarningTimestamp")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("expiresAt").timestampSubtract(14, .day).as("sendWarningTimestamp")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("expiresAt")
              .timestampSubtract("day", 14)
              .alias("sendWarningTimestamp")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("expiresAt").timestampSubtract("day", 14).alias("sendWarningTimestamp")
        )
        .execute();DocSnippets.java

##### Python

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

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(timestampSubtract(field("expiresAt"), "day", 14).as("sendWarningTimestamp"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_TO\_UNIX\_MICROS

**Syntax:**

    timestamp_to_unix_micros(input: TIMESTAMP) -> INT64

**Description:**

Converts `input` to the number of microseconds since `1970-01-01 00:00:00 UTC` . Truncates higher levels of precision by rounding down to the beginning of the microsecond.

**Examples:**

| `input`                        | `timestamp_to_unix_micros(input)` |
| :----------------------------- | :-------------------------------- |
| 1970-01-01 00:00:00 UTC        | 0L                                |
| 1970-01-01 00:06:40.123456 UTC | 400123456L                        |
| 1969-12-31 23:59:59 UTC        | \-1000000L                        |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixMicros().as("unixMicros")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixMicros().as("unixMicros")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("dateString").timestampToUnixMicros().as("unixMicros")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixMicros().alias("unixMicros")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixMicros().alias("unixMicros")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(Field.of("dateString").timestamp_to_unix_micros().as_("unixMicros"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(timestampToUnixMicros(field("dateString")).as("unixMicros"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_TO\_UNIX\_MILLIS

**Syntax:**

    timestamp_to_unix_millis(input: TIMESTAMP) -> INT64

**Description:**

Converts `input` to the number of milliseconds since `1970-01-01 00:00:00 UTC` . Truncates higher levels of precision by rounding down to the beginning of the millisecond.

**Examples:**

| `input`                     | `timestamp_to_unix_millis(input)` |
| :-------------------------- | :-------------------------------- |
| 1970-01-01 00:00:00 UTC     | 0L                                |
| 1970-01-01 01:06:40.123 UTC | 4000123L                          |
| 1969-12-31 23:43:20         | \-1000000L                        |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixMillis().as("unixMillis")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixMillis().as("unixMillis")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("dateString").timestampToUnixMillis().as("unixMillis")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixMillis().alias("unixMillis")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixMillis().alias("unixMillis")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(Field.of("dateString").timestamp_to_unix_millis().as_("unixMillis"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(timestampToUnixMillis(field("dateString")).as("unixMillis"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_TO\_UNIX\_SECONDS

**Syntax:**

    timestamp_to_unix_seconds(input: TIMESTAMP) -> INT64

**Description:**

Converts `input` to the number of seconds since `1970-01-01 00:00:00 UTC` . Truncates higher levels of precision by rounding down to the beginning of the second.

**Examples:**

| `input`                 | `timestamp_to_unix_seconds(input)` |
| :---------------------- | :--------------------------------- |
| 1970-01-01 00:00:00 UTC | 0L                                 |
| 1970-01-01 00:01:00 UTC | 60L                                |
| 1969-12-31 23:55:00 UTC | \-300L                             |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixSeconds().as("unixSeconds")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("dateString").timestampToUnixSeconds().as("unixSeconds")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("dateString").timestampToUnixSeconds().as("unixSeconds")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixSeconds().alias("unixSeconds")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("dateString").timestampToUnixSeconds().alias("unixSeconds")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(Field.of("dateString").timestamp_to_unix_seconds().as_("unixSeconds"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(timestampToUnixSeconds(field("dateString")).as("unixSeconds"))
            .execute()
            .get();PipelineSnippets.java

### TIMESTAMP\_DIFF

**Syntax:**

    timestamp_diff(end: TIMESTAMP, start: TIMESTAMP, unit: STRING) -> INT64

**Description:**

Returns the whole number of specified `unit` intervals between two `TIMESTAMP` s.

  - Returns a negative value if `end` is before `start` .
  - Truncates any fractional unit. For example, `timestamp_diff("2021-01-01 00:00:01", "2021-01-01 00:00:00", "minute")` returns `0` .

The `unit` argument must be a string and one of the following:

  - `microsecond`
  - `millisecond`
  - `second`
  - `minute`
  - `hour`
  - `day`

**Examples:**

| `end`                   | `start`                 | `unit`   | `timestamp_diff(end, start, unit)` |
| :---------------------- | :---------------------- | :------- | :--------------------------------- |
| 2026-07-04 00:01:00 UTC | 2026-07-04 00:00:00 UTC | "second" | 60L                                |
| 2026-07-04 00:00:00 UTC | 2026-07-05 00:00:00 UTC | "day"    | \-1L                               |
| 2026-07-04 00:00:59 UTC | 2026-07-04 00:00:00 UTC | "minute" | 0L                                 |

### TIMESTAMP\_EXTRACT

**Syntax:**

    timestamp_extract(timestamp: TIMESTAMP, part: STRING[, timezone: STRING]) -> INT64

**Description:**

Extracts a specific `part` (e.g. year, month, day) from `timestamp` .

The `part` argument must be a string and one of the following:

  - `microsecond`
  - `millisecond`
  - `second`
  - `minute`
  - `hour`
  - `day`
  - `dayofweek` : Returns a value between 1 (Sunday) and 7 (Saturday).
  - `dayofyear`
  - `week` : Returns the week number of the year, starting at 1 for the first Sunday of the year.
  - `week([weekday])` : Returns the week number of the year, starting on the specified `weekday` .
  - `month`
  - `quarter`
  - `year`
  - `isoweek` : Returns the ISO 8601 week number.
  - `isoyear` : Returns the ISO 8601 week-numbering year.

If the `timezone` argument is provided, the extraction will be based on the given timezone's calendar. The extraction will respect daylight savings time.

If `timezone` is not provided, extraction will be based on `UTC` .

The `timezone` argument should be a string representation of a timezone from the timezone database, for example `America/New_York` . A custom time offset can also be used by specifying an offset from `GMT` .

**Examples:**

| `timestamp`             | `part` | `timezone`   | `timestamp_extract(timestamp, part, timezone)` |
| :---------------------- | :----- | :----------- | :--------------------------------------------- |
| 2025-02-20 10:20:30 UTC | "year" | Not provided | 2025                                           |
| 2025-02-20 10:20:30 UTC | "day"  | Not provided | 20                                             |
| 2025-12-31 23:59:59 UTC | "year" | "Asia/Tokyo" | 2026                                           |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
