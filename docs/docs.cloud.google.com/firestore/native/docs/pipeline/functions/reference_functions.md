# Reference Functions Reference

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## **Reference Functions**

The `  REFERENCE  ` type acts as a "pointer" to other documents in the database (or even other databases). The following functions allow manipulating this type during query execution.

|                                     |                                                              |
| ----------------------------------- | ------------------------------------------------------------ |
| Name                                | Description                                                  |
| `          COLLECTION_ID        `   | Returns the ID of the leaf collection in the given reference |
| `          DOCUMENT_ID        `     | Returns the ID of the document in the given reference        |
| `          PARENT        `          | Returns the parent reference                                 |
| `          REFERENCE_SLICE        ` | Returns a subset of segments from the given reference        |

### COLLECTION\_ID

**Syntax:**

    collection_id(ref: REFERENCE) -> STRING

**Description:**

Returns the leaf collection ID of the given `  REFERENCE  ` .

**Examples:**

| `        ref       `                     | `        collection_id(ref)       ` |
| :--------------------------------------- | :---------------------------------- |
| `        users/user1       `             | `        "users"       `            |
| `        users/user1/posts/post1       ` | `        "posts"       `            |

### DOCUMENT\_ID

**Syntax:**

    document_id(ref: REFERENCE) -> ANY

**Description:**

Returns the document ID of the given `  REFERENCE  ` .

**Examples:**

| `        ref       `                     | `        document_id(ref)       ` |
| :--------------------------------------- | :-------------------------------- |
| `        users/user1       `             | `        "user1"       `          |
| `        users/user1/posts/post1       ` | `        "post1"       `          |

### PARENT

**Syntax:**

    parent(ref: REFERENCE) -> REFERENCE

**Description:**

Returns the parent `  REFERENCE  ` of the given reference, or `  NULL  ` if the ref is a root reference already.

**Examples:**

| `        ref       `                     | `        parent(ref)       ` |
| :--------------------------------------- | :--------------------------- |
| `        /       `                       | `        NULL       `        |
| `        users/user1       `             | `        /       `           |
| `        users/user1/posts/post1       ` | `        users/user1       ` |

### REFERENCE\_SLICE

**Syntax:**

    reference_slice(ref: REFERENCE, offset: INT, length: INT) -> REFERENCE

**Description:**

A `  REFERENCE  ` is a list of `  (collection_id, document_id)  ` tuples and this allows getting a view of that list, just like `  array_slice(...)  ` .

Returns a new `  REFERENCE  ` that is a subset of the segments of the given `  ref  ` .

  - `  offset  ` : The starting index (0-based) of the slice. If negative, it is an offset from the end of the reference.
  - `  length  ` : The number of segments to include in the slice.

**Examples:**

| `        ref       `         | `        offset       ` | `        length       ` | `        reference_slice(ref, offset, length)       ` |
| :--------------------------- | :---------------------- | :---------------------- | :---------------------------------------------------- |
| `        a/1/b/2/c/3       ` | 1L                      | 2L                      | `        b/2/c/3       `                              |
| `        a/1/b/2/c/3       ` | 0L                      | 2L                      | `        a/1/b/2       `                              |
| `        a/1/b/2/c/3       ` | \-2L                    | 2L                      | `        c/3       `                                  |

## What's next

  - See the [Pipeline Queries overview](https://docs.cloud.google.com/firestore/docs/pipeline/overview)
