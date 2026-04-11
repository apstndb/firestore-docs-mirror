# Shredded Fields

This page describes how to view and control the usage of shredded fields in Firestore with MongoDB compatibility. This is available in Firestore Enterprise edition.

When documents are written, Firestore may determine that specific fields should be stored in a shredded format. Shredded fields optimize query performance by reading only the required fields instead of the full document.

## Queries that benefit from shredded fields

Reads on shredded fields are applied to the following query shapes when available:

  - **Aggregation queries** : Queries that only need to access a subset of fields for aggregation operations. For example:
    
        db.customers.aggregate(
          [
            { $match: { "account_balance" : { $lt : 0 } } },
            { $count: "total" }
          ]
        );
    
    or with group-by:
    
        db.customers.aggregate([
          { $match: { "account_balance" : { $lt : 0 } } },
          {
            $group: {
              _id: "$market_segment",
              avg_balance: { $avg: "$account_balance" }
            }
          }
        ]);

  - **Projection queries** : Queries that only return a specific subset of fields. For example:
    
        db.customers.find({}, { family_name: 1, given_name: 1, _id: 0 });

  - **Filter queries** : Filter queries where the Firestore Query Engine determines that using shredded fields for document filtering is beneficial. For example:
    
        db.customers.find({ given_name: "Alice" });

## View shredded fields usage

You can use query explain to check if a query uses shredded fields. The `TableScan` node in the query plan includes a `Storage` section with the following metrics:

  - **Scan shape** :
      - `shredded_fields_only` : The query reads only from shredded fields.
      - `shredded_fields_backjoin` : The query reads from shredded fields and joins with the original document for other fields.
  - **Shredded fields used** : A list of property names read as shredded fields.
  - **Recheck count** : A map of counters for rechecks. A recheck means falling back to reading from the original full document when scanning the shredded fields. This may happen if the field value in a document exceeds 8 KiB, which is too large for the shredded fields storage.

### Example output

    ...
    └── • TableScan
            source: **/customers
            order: UNDEFINED
            row range: (-∞..+∞)
            filter: $lt($account_balance_1, 0)
            output bindings: {$account_balance_1=account_balance, $market_segment_1=market_segment}
            variables: [$account_balance_1, $market_segment_1]
    
            Execution:
             records returned: 1,374
             latency: 26.58 ms
             post-filtered rows: 13,626
             records scanned: 15,000
             data bytes read: 23.73 MiB (24,887,141 B)
    
            Storage:
             scan shape: shredded_fields_only
             shredded fields used: [account_balance, market_segment]

## Control shredded fields usage

By default, Firestore with MongoDB compatibility uses shredded fields when available. You can control this behavior using the `tableScanMethod` option in query comments.

Supported values for `tableScanMethod` :

  - `shreddedFieldsEnabled` (Default): Use shredded fields when available.
  - `shreddedFieldsDisabled` : Shredded fields will not be used.
  - `forceShreddedFields` : Fail the query if a table scan cannot be fulfilled by scanning shredded fields.

### Find commands

Use the `.comment()` method to specify options for a `find` command:

    db.customers.find(
      { account_balance: 0.0 }
    ).comment(
      {
        firestoreOptions: {
          tableScanMethod: "shreddedFieldsDisabled"
        }
      }
    );

### Aggregate commands

Use the `comment` option in the options parameter of an `aggregate` command:

    db.customers.aggregate(
      [
        { $match: { "account_balance" : { $lt : 0 } } },
        { $count: "total" }
      ],
      {
        comment: {
          firestoreOptions: {
            tableScanMethod: "shreddedFieldsDisabled"
          }
        }
      }
    );

## Query performance warnings

Firestore with MongoDB compatibility may emit performance warnings in the query explain result when inefficient shredded field usage is detected. For example:

  - **Low-selectivity queries** : If a query scans shredded fields for filtering but filters out few documents, making the scan inefficient.

  - **High-recheck queries** : If the query falls back to full document reads frequently, which can impact performance. You can use operators like `$bsonSize` to identify large values that trigger rechecks.

In these cases, consider disabling shredded field reads using query options.

## Limitations

Firestore only attempts to shred top-level fields. It also restricts the number of fields that can be shredded per collection.
