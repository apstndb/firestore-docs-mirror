# Map Functions Reference

> **Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Map Functions**

|                                    |                                                         |
| ---------------------------------- | ------------------------------------------------------- |
| Name                               | Description                                             |
| `         MAP        `             | Constructs a map value from a series of key-value pairs |
| `         MAP_GET        `         | Returns the value in a map given a specified key        |
| `         MAP_SET        `         | Returns a copy of a map with a series of updated keys   |
| `         MAP_REMOVE        `      | Returns a copy of a map with a series of keys removed   |
| `         MAP_MERGE        `       | Merges a series of maps together.                       |
| `         CURRENT_CONTEXT        ` | Returns the current context as a map.                   |
| `         MAP_KEYS        `        | Returns an array of all keys in a map.                  |
| `         MAP_VALUES        `      | Returns an array of all values in a map.                |
| `         MAP_ENTRIES        `     | Returns an array of key-value pairs of a map.           |

### MAP

**Syntax:**

    map(key: STRING, value: ANY, ...) -> MAP

**Description:**

Constructs a map from a series of key-value pairs.

### MAP\_GET

**Syntax:**

    map_get(map: ANY, key: STRING) -> ANY

**Description:**

Returns the value in a map given a specified key. Returns an `ABSENT` value if the `key` does not exist in the map, or if the `map` argument is not a `MAP` .

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("awards").mapGet("pulitzer").as("hasPulitzerAward")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("awards").mapGet("pulitzer").as("hasPulitzerAward")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("awards").mapGet("pulitzer").as("hasPulitzerAward")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("awards").mapGet("pulitzer").alias("hasPulitzerAward")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("awards").mapGet("pulitzer").alias("hasPulitzerAward")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("awards").map_get("pulitzer").as_("hasPulitzerAward"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(mapGet(field("awards"), "pulitzer").as("hasPulitzerAward"))
            .execute()
            .get();PipelineSnippets.java

### MAP\_SET

**Syntax:**

    map_set(map: MAP, key: STRING, value: ANY, ...) -> MAP

**Description:**

Returns a copy of the `map` value with its contents updated by a series of key-value pairs.

If the given resolves to an absent value, the associated key is removed from the map.

If the `map` argument is not a `MAP` , returns an absent value.

### MAP\_REMOVE

**Syntax:**

    map_remove(map: MAP, key: STRING...) -> MAP

**Description:**

Returns a copy of the `map` value with a series of keys removed.

### MAP\_MERGE

**Syntax:**

    map_merge(maps: MAP...) -> MAP

Merges the contents of 2 or more maps. If multiple maps have conflicting values, the last value is used.

### CURRENT\_CONTEXT

**Syntax:**

    current_context() -> MAP

Returns a map consisting of all available fields in the current point of execution.

### MAP\_KEYS

**Syntax:**

    map_keys(map: MAP) -> ARRAY<STRING>

**Description:**

Returns an array containing all keys of the `map` value.

### MAP\_VALUES

**Syntax:**

    map_values(map: MAP) -> ARRAY<ANY>

**Description:**

Returns an array containing all values of the `map` value.

### MAP\_ENTRIES

**Syntax:**

    map_entries(map: MAP) -> ARRAY<MAP>

**Description:**

Returns an array containing all key-value pairs in the `map` value.

Each key-value pair will be in the form of a map with two entries, `k` and `v` .

**Examples:**

| `map`                          | `map_entries(map)`                                        |
| :----------------------------- | :-------------------------------------------------------- |
| {}                             | \[\]                                                      |
| {"foo" : 2L}                   | \[{"k": "foo", "v" : 2L}\]                                |
| {"foo" : "bar", "bar" : "foo"} | \[{"k": "foo", "v" : "bar" }, {"k" : "bar", "v": "foo"}\] |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
