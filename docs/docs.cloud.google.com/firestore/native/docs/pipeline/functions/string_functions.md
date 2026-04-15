# String Functions Reference

> **Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **String Functions**

|                                       |                                                                                   |
| ------------------------------------- | --------------------------------------------------------------------------------- |
| Name                                  | Description                                                                       |
| `         BYTE_LENGTH        `        | Returns the number of `BYTES` in a `STRING` or `BYTES` value                      |
| `         CHAR_LENGTH        `        | Returns the number of unicode characters in a `STRING` value                      |
| `         STARTS_WITH        `        | Returns `TRUE` if a `STRING` begins with a given prefix                           |
| `         ENDS_WITH        `          | Returns `TRUE` if a `STRING` ends with a given postfix                            |
| `         LIKE        `               | Returns `TRUE` if a `STRING` matches a pattern                                    |
| `         REGEX_CONTAINS        `     | Returns `TRUE` if a value is a partial or full match for a regular expression     |
| `         REGEX_MATCH        `        | Returns `TRUE` if any part of a value matches a regular expression                |
| `         STRING_CONCAT        `      | Concatenates multiple `STRING` into a `STRING`                                    |
| `         STRING_CONTAINS        `    | Returns `TRUE` if a value contains a `STRING`                                     |
| `         STRING_INDEX_OF        `    | Returns the 0-based index of the first occurrence of a `STRING` or `BYTES` value. |
| `         TO_UPPER        `           | Converts a `STRING` or `BYTES` value to uppercase.                                |
| `         TO_LOWER        `           | Converts a `STRING` or `BYTES` value to lowercase.                                |
| `         SUBSTRING        `          | Gets a substring of a `STRING` or `BYTES` value.                                  |
| `         STRING_REVERSE        `     | Reverses a `STRING` or `BYTES` value.                                             |
| `         STRING_REPEAT        `      | Repeats a `STRING` or `BYTES` value a specified number of times.                  |
| `         STRING_REPLACE_ALL        ` | Replaces all occurrences of a `STRING` or `BYTES` value.                          |
| `         STRING_REPLACE_ONE        ` | Replaces the first occurrence of a `STRING` or `BYTES` value.                     |
| `         TRIM        `               | Trims leading and trailing characters from a `STRING` or `BYTES` value.           |
| `         LTRIM        `              | Trims leading characters from a `STRING` or `BYTES` value.                        |
| `         RTRIM        `              | Trims trailing characters from a `STRING` or `BYTES` value.                       |
| `         SPLIT        `              | Splits a `STRING` or `BYTES` value into an array.                                 |

### BYTE\_LENGTH

**Syntax:**

    byte_length[T <: STRING | BYTES](value: T) -> INT64

**Description:**

Returns the number of `BYTES` in a `STRING` or `BYTES` value.

**Examples:**

| value    | `byte_length(value)` |
| :------- | :------------------- |
| "abc"    | 3                    |
| "xyzabc" | 6                    |
| b"abc"   | 3                    |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("title").byteLength().as("titleByteLength")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("title").byteLength().as("titleByteLength")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("title").byteLength().as("titleByteLength")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("title").byteLength().alias("titleByteLength")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("title").byteLength().alias("titleByteLength")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("title").byte_length().as_("titleByteLength"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(byteLength(field("title")).as("titleByteLength"))
            .execute()
            .get();PipelineSnippets.java

### CHAR\_LENGTH

**Syntax:**

    char_length(value: STRING) -> INT64

**Description:**

Returns the number of unicode code points in `STRING` value.

**Examples:**

| value   | `char_length(value)` |
| :------ | :------------------- |
| "abc"   | 3                    |
| "hello" | 5                    |
| "world" | 5                    |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("title").charLength().as("titleCharLength")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("title").charLength().as("titleCharLength")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("title").charLength().as("titleCharLength")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("title").charLength().alias("titleCharLength")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("title").charLength().alias("titleCharLength")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("title").char_length().as_("titleCharLength"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(charLength(field("title")).as("titleCharLength"))
            .execute()
            .get();PipelineSnippets.java

### STARTS\_WITH

**Syntax:**

    starts_with(value: STRING, prefix: STRING) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` begins with `prefix` .

**Examples:**

| value | prefix | `starts_with(value, prefix)` |
| :---- | :----- | :--------------------------- |
| "abc" | "a"    | true                         |
| "abc" | "b"    | false                        |
| "abc" | ""     | true                         |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("title").startsWith("The")
          .as("needsSpecialAlphabeticalSort")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("title").startsWith("The")
          .as("needsSpecialAlphabeticalSort")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("title").startsWith("The")
          .as("needsSpecialAlphabeticalSort")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("title").startsWith("The")
                .alias("needsSpecialAlphabeticalSort")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("title").startsWith("The")
                .alias("needsSpecialAlphabeticalSort")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(
            Field.of("title").starts_with("The").as_("needsSpecialAlphabeticalSort")
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(startsWith(field("title"), "The").as("needsSpecialAlphabeticalSort"))
            .execute()
            .get();PipelineSnippets.java

### ENDS\_WITH

**Syntax:**

    ends_with(value: STRING, postfix: STRING) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` ends with `postfix` .

**Examples:**

| value | postfix | `ends_with(value, postfix)` |
| :---- | :------ | :-------------------------- |
| "abc" | "c"     | true                        |
| "abc" | "b"     | false                       |
| "abc" | ""      | true                        |

##### Node.js

    const result = await db.pipeline()
      .collection("inventory/devices/laptops")
      .select(
        field("name").endsWith("16 inch")
          .as("16InLaptops")
      )
      .execute();test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("inventory/devices/laptops")
      .select([
        Field("name").endsWith("16 inch")
          .as("16InLaptops")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("inventory/devices/laptops")
        .select(
            field("name").endsWith("16 inch")
                .alias("16InLaptops")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("inventory/devices/laptops")
        .select(
            field("name").endsWith("16 inch")
                .alias("16InLaptops")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("inventory/devices/laptops")
        .select(Field.of("name").ends_with("16 inch").as_("16InLaptops"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("inventory/devices/laptops")
            .select(endsWith(field("name"), "16 inch").as("16InLaptops"))
            .execute()
            .get();PipelineSnippets.java

### LIKE

**Syntax:**

    like(value: STRING, pattern: STRING) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` matches `pattern` .

**Examples:**

| value       | pattern      | `like(value, pattern)` |
| :---------- | :----------- | :--------------------- |
| "Firestore" | "Fire%"      | true                   |
| "Firestore" | "%store"     | true                   |
| "Datastore" | "Data\_tore" | true                   |
| "100%"      | "100\\%"     | true                   |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("genre").like("%Fiction")
          .as("anyFiction")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("genre").like("%Fiction")
          .as("anyFiction")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("genre").like("%Fiction")
          .as("anyFiction")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("genre").like("%Fiction")
                .alias("anyFiction")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("genre").like("%Fiction")
                .alias("anyFiction")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("genre").like("%Fiction").as_("anyFiction"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(like(field("genre"), "%Fiction").as("anyFiction"))
            .execute()
            .get();PipelineSnippets.java

### REGEX\_CONTAINS

**Syntax:**

    regex_contains(value: STRING, pattern: STRING) -> BOOLEAN

**Description:**

Returns `TRUE` if some part of `value` matches `pattern` . If `pattern` is not a valid regular expression, this function returns an `error` .

Regular expressions follow the syntax of the [re2](https://github.com/google/re2/wiki/Syntax) library.

**Examples:**

| value       | pattern  | `regex_contains(value, pattern)` |
| :---------- | :------- | :------------------------------- |
| "Firestore" | "Fire"   | true                             |
| "Firestore" | "store$" | true                             |
| "Firestore" | "data"   | false                            |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("title").regexContains("Firestore (Enterprise|Standard)")
          .as("isFirestoreRelated")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("title").regexContains("Firestore (Enterprise|Standard)")
          .as("isFirestoreRelated")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("title").regexContains("Firestore (Enterprise|Standard)")
          .as("isFirestoreRelated")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("title").regexContains("Firestore (Enterprise|Standard)")
                .alias("isFirestoreRelated")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("title").regexContains("Firestore (Enterprise|Standard)")
                .alias("isFirestoreRelated")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(
            Field.of("title")
            .regex_contains("Firestore (Enterprise|Standard)")
            .as_("isFirestoreRelated")
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(
                regexContains(field("title"), "Firestore (Enterprise|Standard)")
                    .as("isFirestoreRelated"))
            .execute()
            .get();PipelineSnippets.java

### REGEX\_MATCH

**Syntax:**

    regex_match(value: STRING, pattern: STRING) -> BOOLEAN

**Description:**

Returns `TRUE` if `value` fully matches `pattern` . If `pattern` is not a valid regular expression, this function returns an `error` .

Regular expressions follow the syntax of the [re2](https://github.com/google/re2/wiki/Syntax) library.

**Examples:**

| value       | pattern     | `regex_match(value, pattern)` |
| :---------- | :---------- | :---------------------------- |
| "Firestore" | "F.\*store" | true                          |
| "Firestore" | "Fire"      | false                         |
| "Firestore" | "^F.\*e$"   | true                          |

##### Node.js

    const result = await db.pipeline()
      .collection("documents")
      .select(
        field("title").regexMatch("Firestore (Enterprise|Standard)")
          .as("isFirestoreExactly")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("documents")
      .select(
        field("title").regexMatch("Firestore (Enterprise|Standard)")
          .as("isFirestoreExactly")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("documents")
      .select([
        Field("title").regexMatch("Firestore (Enterprise|Standard)")
          .as("isFirestoreExactly")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("documents")
        .select(
            field("title").regexMatch("Firestore (Enterprise|Standard)")
                .alias("isFirestoreExactly")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("documents")
        .select(
            field("title").regexMatch("Firestore (Enterprise|Standard)")
                .alias("isFirestoreExactly")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("documents")
        .select(
            Field.of("title")
            .regex_match("Firestore (Enterprise|Standard)")
            .as_("isFirestoreExactly")
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("documents")
            .select(
                regexMatch(field("title"), "Firestore (Enterprise|Standard)")
                    .as("isFirestoreExactly"))
            .execute()
            .get();PipelineSnippets.java

### STRING\_CONCAT

**Syntax:**

    string_concat(values: STRING...) -> STRING

**Description:**

Concatenates two or more `STRING` values into a single result.

**Examples:**

| arguments        | `string_concat(values...)` |
| :--------------- | :------------------------- |
| `()`             | error                      |
| `("a")`          | "a"                        |
| `("abc", "def")` | "abcdef"                   |
| `("a", "", "c")` | "ac"                       |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("title").stringConcat(" by ", field("author"))
          .as("fullyQualifiedTitle")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("title").stringConcat(" by ", field("author"))
          .as("fullyQualifiedTitle")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("title").concat([" by ", Field("author")])
          .as("fullyQualifiedTitle")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("title").concat(" by ", field("author"))
                .alias("fullyQualifiedTitle")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("title").concat(" by ", field("author"))
                .alias("fullyQualifiedTitle")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(
            Field.of("title")
            .concat(" by ", Field.of("author"))
            .as_("fullyQualifiedTitle")
        )
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(stringConcat(field("title"), " by ", field("author")).as("fullyQualifiedTitle"))
            .execute()
            .get();PipelineSnippets.java

### STRING\_CONTAINS

**Syntax:**

    string_contains(value: STRING, substring: STRING) -> BOOLEAN

**Description:**

Checks if `value` contains the literal String `substring` .

**Examples:**

| value | substring | `string_contains(value, substring)` |
| :---- | :-------- | :---------------------------------- |
| "abc" | "b"       | true                                |
| "abc" | "d"       | false                               |
| "abc" | ""        | true                                |
| "a.c" | "."       | true                                |
| "☃☃☃" | "☃"       | true                                |

##### Node.js

    const result = await db.pipeline()
      .collection("articles")
      .select(
        field("body").stringContains("Firestore")
          .as("isFirestoreRelated")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("articles")
      .select(
        field("body").stringContains("Firestore")
          .as("isFirestoreRelated")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("articles")
      .select([
        Field("body").stringContains("Firestore")
          .as("isFirestoreRelated")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("articles")
        .select(
            field("body").stringContains("Firestore")
                .alias("isFirestoreRelated")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("articles")
        .select(
            field("body").stringContains("Firestore")
                .alias("isFirestoreRelated")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("articles")
        .select(Field.of("body").string_contains("Firestore").as_("isFirestoreRelated"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("articles")
            .select(stringContains(field("body"), "Firestore").as("isFirestoreRelated"))
            .execute()
            .get();PipelineSnippets.java

### STRING\_INDEX\_OF

**Syntax:**

    string_index_of[T <: STRING | BYTES](value: T, search: T) -> INT64

**Description:**

Returns the 0-based index of the first occurrence of `search` in `value` .

  - Returns `-1` if `search` is not found.
  - If `value` is a `STRING` value, the result is measured in unicode code points. If it is a `BYTES` value, it is measured in bytes.
  - If `search` is an empty `STRING` or `BYTES` value, the result is `0` .

**Examples:**

| value         | search | `string_index_of(value, search)` |
| :------------ | :----- | :------------------------------- |
| "hello world" | "o"    | 4                                |
| "hello world" | "l"    | 2                                |
| "hello world" | "z"    | \-1                              |
| "banana"      | "na"   | 2                                |
| "abc"         | ""     | 0                                |
| b"abc"        | b"b"   | 1                                |
| "é"           | "é"    | 0                                |
| b"é"          | b"é"   | 0                                |

### TO\_UPPER

**Syntax:**

    to_upper[T <: STRING | BYTES](value: T) -> T

**Description:**

Converts a `STRING` or `BYTES` value to uppercase.

If a byte or char does not correspond to a UTF-8 lowercase alphabetic character, it is passed through unchanged.

**Examples:**

| value  | `to_upper(value)` |
| :----- | :---------------- |
| "abc"  | "ABC"             |
| "AbC"  | "ABC"             |
| b"abc" | b"ABC"            |
| b"a1c" | b"A1C"            |

##### Node.js

    const result = await db.pipeline()
      .collection("authors")
      .select(
        field("name").toUpper()
          .as("uppercaseName")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("authors")
      .select(
        field("name").toUpper()
          .as("uppercaseName")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("authors")
      .select([
        Field("name").toUpper()
          .as("uppercaseName")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("authors")
        .select(
            field("name").toUpper()
                .alias("uppercaseName")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("authors")
        .select(
            field("name").toUpper()
                .alias("uppercaseName")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("authors")
        .select(Field.of("name").to_upper().as_("uppercaseName"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("authors")
            .select(toUpper(field("name")).as("uppercaseName"))
            .execute()
            .get();PipelineSnippets.java

### TO\_LOWER

**Syntax:**

    to_lower[T <: STRING | BYTES](value: T) -> T

**Description:**

Converts a `STRING` or `BYTES` value to lowercase.

If a byte or char does not correspond to a UTF-8 uppercase alphabetic character, it is passed through unchanged.

**Examples:**

| value  | `to_lower(value)` |
| :----- | :---------------- |
| "ABC"  | "abc"             |
| "AbC"  | "abc"             |
| "A1C"  | "a1c"             |
| b"ABC" | b"abc"            |

##### Node.js

    const result = await db.pipeline()
      .collection("authors")
      .select(
        field("genre").toLower().equal("fantasy")
          .as("isFantasy")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("authors")
      .select(
        field("genre").toLower().equal("fantasy")
          .as("isFantasy")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("authors")
      .select([
        Field("genre").toLower().equal("fantasy")
          .as("isFantasy")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("authors")
        .select(
            field("genre").toLower().equal("fantasy")
                .alias("isFantasy")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("authors")
        .select(
            field("genre").toLower().equal("fantasy")
                .alias("isFantasy")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("authors")
        .select(Field.of("genre").to_lower().equal("fantasy").as_("isFantasy"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("authors")
            .select(equal(toLower(field("genre")), "fantasy").as("isFantasy"))
            .execute()
            .get();PipelineSnippets.java

### SUBSTRING

**Syntax:**

    substring[T <: STRING | BYTES](input: T, position: INT64) -> T
    substring[T <: STRING | BYTES](input: T, position: INT64, length: INT64) -> T

**Description:**

Returns a substring of `input` starting at `position` (zero-based index) and including up to `length` entries. If no `length` is provided, returns the substring from `position` to the end of the `input` .

  - If `input` is a `STRING` value, `position` and `length` are measured in unicode code points. If it is a `BYTES` value, they are measured in bytes.

  - If `position` is greater than the length of the `input` , an empty substring is returned. If `position` plus `length` is greater than the length of `input` , the substring is truncated to the end of `input` .

  - If `position` is negative, the position is taken from the end of the input. If the negative `position` is greater than the size of the input, the position is set to zero. `length` must be non-negative.

**Examples:**

When `length` is not provided:

| input  | position | `substring(input, position)` |
| :----- | :------- | :--------------------------- |
| "abc"  | 0        | "abc"                        |
| "abc"  | 1        | "bc"                         |
| "abc"  | 3        | ""                           |
| "abc"  | \-1      | "c"                          |
| b"abc" | 1        | b"bc"                        |

When `length` is provided:

| input  | position | length | `substring(input, position, length)` |
| :----- | :------- | :----- | :----------------------------------- |
| "abc"  | 0        | 1      | "a"                                  |
| "abc"  | 1        | 2      | "bc"                                 |
| "abc"  | \-1      | 1      | "c"                                  |
| b"abc" | 0        | 1      | b"a"                                 |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .where(field("title").startsWith("The "))
      .select(
        field("title").substring(4)
          .as("titleWithoutLeadingThe")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .where(field("title").startsWith("The "))
      .select(
        field("title").substring(4)
          .as("titleWithoutLeadingThe")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .where(Field("title").startsWith("The "))
      .select([
        Field("title").substring(position: 4)
          .as("titleWithoutLeadingThe")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .where(field("title").startsWith("The "))
        .select(
            field("title")
              .substring(constant(4),
                field("title").charLength().subtract(4))
                .alias("titleWithoutLeadingThe")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .where(field("title").startsWith("The "))
        .select(
            field("title").substring(
              constant(4),
                field("title").charLength().subtract(4))
                .alias("titleWithoutLeadingThe")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .where(Field.of("title").starts_with("The "))
        .select(Field.of("title").substring(4).as_("titleWithoutLeadingThe"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .where(startsWith(field("title"), "The "))
            .select(
                substring(field("title"), constant(4), field("title").charLength())
                    .as("titleWithoutLeadingThe"))
            .execute()
            .get();PipelineSnippets.java

### STRING\_REVERSE

**Syntax:**

    string_reverse[T <: STRING | BYTES](input: T) -> T

**Description:**

Returns the supplied input in reverse order.

Characters are delineated by Unicode code points when the input is a `STRING` , and bytes when the input is a `BYTES` value.

**Examples:**

| input   | `string_reverse(input)` |
| :------ | :---------------------- |
| "abc"   | "cba"                   |
| "a🌹b"   | "b🌹a"                   |
| "hello" | "olleh"                 |
| b"abc"  | b"cba"                  |

##### Node.js

    const result = await db.pipeline()
      .collection("books")
      .select(
        field("name").reverse().as("reversedName")
      )
      .execute();test.firestore.js

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("name").reverse().as("reversedName")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("name").reverse().as("reversedName")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("name").reverse().alias("reversedName")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("name").reverse().alias("reversedName")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("name").string_reverse().as_("reversedName"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(reverse(field("name")).as("reversedName"))
            .execute()
            .get();PipelineSnippets.java

### STRING\_REPEAT

**Syntax:**

    string_repeat[T <: STRING | BYTES](input: T, repetitions: INT64) -> T

**Description:**

Returns the `input` repeated `repetitions` times.

  - `repetitions` must be a non-negative integer.
  - If `repetitions` is `0` , returns an empty value of the same type as `input` .
  - If the result exceeds the maximum allowed size (1 MB), an error is returned.

**Examples:**

| input | repetitions | `string_repeat(input, repetitions)` |
| :---- | :---------- | :---------------------------------- |
| "foo" | 3           | "foofoofoo"                         |
| "foo" | 0           | ""                                  |
| "a "  | 3           | "a a a "                            |
| b"ab" | 2           | b"abab"                             |
| "é🦆"  | 2           | "é🦆é🦆"                              |

### STRING\_REPLACE\_ALL

**Syntax:**

    string_replace_all[T <: STRING | BYTES](input: T, find: T, replacement: T) -> T

**Description:**

Replaces all non-overlapping occurrences of `find` in `input` with `replacement` .

  - Matches are case-sensitive.
  - If `find` is empty, no replacements are made.

**Examples:**

| input       | find  | replacement | `string_replace_all(input, find, replacement)` |
| :---------- | :---- | :---------- | :--------------------------------------------- |
| "foobarfoo" | "foo" | "baz"       | "bazbarbaz"                                    |
| "ababab"    | "aba" | "c"         | "cbab"                                         |
| "foobar"    | "o"   | ""          | "fbar"                                         |
| "é🦆🌎🦆"      | "🦆"   | "a"         | "éa🌎a"                                         |
| b"abc"      | b"b"  | b"d"        | b"adc"                                         |

### STRING\_REPLACE\_ONE

**Syntax:**

    string_replace_one[T <: STRING | BYTES](input: T, find: T, replacement: T) -> T

**Description:**

Replaces the first occurrence of `find` in `input` with `replacement` .

  - Matches are case-sensitive.
  - If `find` is empty, no replacements are made.

**Examples:**

| input       | find  | replacement | `string_replace_one(input, find, replacement)` |
| :---------- | :---- | :---------- | :--------------------------------------------- |
| "foobarfoo" | "foo" | "baz"       | "bazbarfoo"                                    |
| "é"         | "é"   | "a"         | "a"                                            |
| b"foobar"   | b"o"  | b"z"        | b"fzoobar"                                     |

### TRIM

**Syntax:**

    trim[T <: STRING | BYTES](input: T, values_to_trim: T) -> T
    trim[T <: STRING | BYTES](input: T) -> T

**Description:**

Trims a specified set of `BYTES` or `CHARS` from the beginning and end of the supplied `input` .

  - If no `values_to_trim` are provided, trims whitespace characters.

**Examples:**

When `values_to_trim` is not provided:

| input                      | `trim(input)` |
| :------------------------- | :------------ |
| " foo "                    | "foo"         |
| b" foo "                   | b"foo"        |
| "foo"                      | "foo"         |
| ""                         | ""            |
| " "                        | ""            |
| "\\t foo \\n"              | "foo"         |
| b"\\t foo \\n"             | b"foo"        |
| "\\r\\f\\v foo \\r\\f\\v"  | "foo"         |
| b"\\r\\f\\v foo \\r\\f\\v" | b"foo"        |

When `values_to_trim` is provided:

| input          | values\_to\_trim | `trim(input, values_to_trim)` |
| :------------- | :--------------- | :---------------------------- |
| "abcbfooaacb"  | "abc"            | "foo"                         |
| "abcdaabadbac" | "abc"            | "daabad"                      |
| b"C1C2C3"      | b"C1"            | b"C2C3"                       |
| b"C1C2"        | "foo"            | error                         |
| "foo"          | b"C1"            | error                         |

### Web

    const result = await execute(db.pipeline()
      .collection("books")
      .select(
        field("name").trim().as("whitespaceTrimmedName")
      )
    );test.firestore.js

##### Swift

    let result = try await db.pipeline()
      .collection("books")
      .select([
        Field("name").trim(" \n\t").as("whitespaceTrimmedName")
      ])
      .execute()PipelineSnippets.swift

##### Kotlin  
Android

    val result = db.pipeline()
        .collection("books")
        .select(
            field("name").trim().alias("whitespaceTrimmedName")
        )
        .execute()DocSnippets.kt

##### Java  
Android

    Task<Pipeline.Snapshot> result = db.pipeline()
        .collection("books")
        .select(
            field("name").trim().alias("whitespaceTrimmedName")
        )
        .execute();DocSnippets.java

##### Python

    from google.cloud.firestore_v1.pipeline_expressions import Field
    
    result = (
        client.pipeline()
        .collection("books")
        .select(Field.of("name").trim().as_("whitespaceTrimmedName"))
        .execute()
    )firestore_pipelines.py

##### Java

    Pipeline.Snapshot result =
        firestore
            .pipeline()
            .collection("books")
            .select(trim(field("name")).as("whitespaceTrimmedName"))
            .execute()
            .get();PipelineSnippets.java

### LTRIM

**Syntax:**

    ltrim[T <: STRING | BYTES](value: T, to_trim: T) -> T
    ltrim[T <: STRING | BYTES](value: T) -> T

**Description:**

Trims a specified set of `BYTES` or `CHARS` from the beginning of the supplied `value` .

  - If `to_trim` is not provided, trims leading whitespace characters.

**Examples:**

When `to_trim` is not provided:

| value   | `ltrim(value)` |
| :------ | :------------- |
| " foo " | "foo "         |
| "foo"   | "foo"          |

When `to_trim` is provided:

| value     | to\_trim | `ltrim(value, to_trim)` |
| :-------- | :------- | :---------------------- |
| "aaabc"   | "a"      | "bc"                    |
| "abacaba" | "ba"     | "caba"                  |
| "é"       | "é"      | ""                      |

### RTRIM

**Syntax:**

    rtrim[T <: STRING | BYTES](value: T, to_trim: T) -> T
    rtrim[T <: STRING | BYTES](value: T) -> T

**Description:**

Trims a specified set of `BYTES` or `CHARS` from the end of the supplied `value` .

  - If `to_trim` is not provided, trims trailing whitespace characters.

**Examples:**

When `to_trim` is not provided:

| value   | `rtrim(value)` |
| :------ | :------------- |
| " foo " | " foo"         |
| "foo"   | "foo"          |

When `to_trim` is provided:

| value     | to\_trim | `rtrim(value, to_trim)` |
| :-------- | :------- | :---------------------- |
| "abccc"   | "c"      | "ab"                    |
| "abacaba" | "ba"     | "abac"                  |
| "é"       | "é"      | ""                      |

### SPLIT

**Syntax:**

    split(input: STRING) -> ARRAY<STRING>
    split[T <: STRING | BYTES](input: T, delimiter: T) -> ARRAY<T>

**Description:**

Splits a `STRING` or `BYTES` value, using a delimiter.

  - For `STRING` the default delimiter is the comma `,` . The delimiter is treated as a single string.

  - For `BYTES` , you must specify a delimiter.

  - Splitting on an empty delimiter produces an array of Unicode codepoints for `STRING` values, and an array of `BYTES` for `BYTES` values.

  - Splitting an empty `STRING` returns an `ARRAY` with a single empty `STRING` .

**Examples:**

When `delimiter` is not provided:

| input         | `split(input)`          |
| :------------ | :---------------------- |
| "foo,bar,foo" | \["foo", "bar", "foo"\] |
| "foo"         | \["foo"\]               |
| ",foo,"       | \["", "foo", ""\]       |
| ""            | \[""\]                  |
| b"C120C2C4"   | error                   |

When `delimiter` is provided:

| input         | delimiter | `split(input, delimiter)` |
| :------------ | :-------- | :------------------------ |
| "foo bar foo" | " "       | \["foo", "bar", "foo"\]   |
| "foo bar foo" | "z"       | \["foo bar foo"\]         |
| "abc"         | ""        | \["a", "b", "c"\]         |
| b"C1,C2,C4"   | b","      | \[b"C1", b"C2", b"C4"\]   |
| b"ABC"        | b""       | \[b"A", b"B", b"C"\]      |
| "foo"         | b"C1"     | error                     |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
