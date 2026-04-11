# Queries optimized with shredded fields

**Preview — Firestore in Native mode (with Pipeline Operations) for Enterprise Edition**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to view and control the usage of shredded fields in Firestore. This is available in Firestore Enterprise edition.

When documents are written, Firestore may determine that specific fields should be stored in a shredded format. Shredded fields optimize query performance by reading only the required fields instead of the full document.

## Queries that benefit from shredded fields

Reads on shredded fields are applied to the following query shapes where applicable:

  - **Aggregation queries** : Queries that only need to access a subset of fields for aggregation operations. For example:
    
        db.pipeline()
          .collection("/customers")
          .where(lessThan("account_balance", 0))
          .aggregate(
            countAll().as("total"),
          )
    
    or with group-by:
    
        db.pipeline()
          .collection("/customers")
          .where(lessThan("account_balance", 0))
          .aggregate({
            accumulators: [
              field('account_balance').average().as('avg_account_balance')
            ],
            groups: [field('market_segment')]
          })

  - **Projection queries** : Queries that only return a specific subset of fields. For example:
    
        db.pipeline()
          .collection("/customers")
          .select("family_name", "given_name")
          .limit(10)

  - **Filter queries** : Queries where the Firestore query engine determines that using shredded fields for document filtering is beneficial. For example:
    
        db.pipeline()
          .collection("/customers")
          .where(equal("given_name", "alice"))

## View shredded fields usage

You can use query explain to check if a query uses shredded fields. The `TableScan` node in the query plan includes a `Storage` section with the following metrics:

  - **Scan shape** :
      - `shredded_fields_only` : The query reads only from shredded fields.
      - `shredded_fields_backjoin` : The query reads from shredded fields and joins with the original document for other fields.
  - **Shredded fields used** : A list of field names read as shredded fields.
  - **Recheck count** : A map of counters for rechecks. A recheck means falling back to reading from the original full document when scanning the shredded fields. This may happen if the field value in a document exceeds 8 KiB, which is too large for the shredded fields storage.

### Example output

    ...
    └── • TableScan
            source: /customers
            order: UNDEFINED
            row range: (-∞..+∞)
            filter: ($account_balance_1 < 0L)
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

By default, Firestore uses shredded fields when available. You can control this behavior using the `table_scan_method` query option.

Supported values for the `table_scan_method` option:

  - `shredded_fields_enabled` (Default): Use shredded fields when available.
  - `shredded_fields_disabled` : Do not use shredded fields.
  - `force_shredded_fields` : Fail the query if a table scan cannot be fulfilled by scanning shredded fields.

### Example

    var opts = new PipelineExecuteOptions()
        .with("table_scan_method", "shredded_fields_disabled");
    
    var snapshot = db.pipeline()
        .collection("/customers")
        .where(equal("given_name", "alice"))
        .execute(opts)
        .get();

## Query performance warnings

Firestore may emit performance warnings in the query explain result when inefficient shredded field usage is detected. For example:

  - **Low-selectivity queries** : Occurs when a query scans shredded fields for filtering but filters out too few documents, making the scan inefficient.

  - **High-recheck queries** : Occurs when the query falls back to full document reads frequently, which can impact performance. You can use functions like `storage_size` to identify large values that trigger rechecks.

In these cases, consider disabling shredded field reads using query options.

## Limitations

Firestore only shreds top-level fields. It also restricts the number of fields that can be shredded per collection group.
