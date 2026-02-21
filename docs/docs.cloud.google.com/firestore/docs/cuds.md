# Committed use discounts

Committed use discounts (CUDs) provide deeply discounted prices in exchange for your commitment to continuously spend a certain amount on Firestore operations — *Read/Write/Delete* — for one year or three years.

CUDs are ideal when your spending on Firestore operations involves a predictable minimum that you can commit to for at least a year.

**Note** : This document discusses some spend-based committed use discounts (CUDs) that automatically migrate to a new consumption model, which leverages discounts rather than credits. The migration date is indicated by a notification in the Google Cloud console Billing Overview page. For more information about the improvements, the affected CUDs, and any required actions on your part, see [Spend-based CUDs](/docs/cuds-multiprice) .

## Firestore CUD pricing

Firestore offers two levels of discounts, depending on the commitment period:

  - **20% discount** : You get this by committing to a 1-year term. For the duration of your term, you pay the Firestore CUD 1-year price (consumption model ID 3892-BA17-92A7) as your committed hourly spend amount.
  - **40% discount** : You get this by committing to a 3-year term. For the duration of your term, you pay the Firestore CUD 3-year price (consumption model ID 2FD9-44B6-D2AC) as your committed hourly spend amount.

When you purchase a commitment, you choose a one-year or three-year period. You also specify a *commitment amount* , which is your expected Firestore expenditure on Read/Write/Delete operations per hour over that period. This commitment amount becomes your *commitment fee* . You then receive the CUD, and you are billed for the commitment fee on a monthly basis for the duration of the CUD period.

The discount applies to all eligible operations usage in Firestore databases associated with projects under the Cloud Billing account used to purchase the commitment, regardless of the region of the database.

Any expenditure beyond the commitment is billed at the on-demand rate. As your Firestore usage grows, you can purchase additional commitments to receive discounts on increased expenditures that are not covered by previous commitments.

If the on-demand prices for Firestore Read/Write/Delete operations change after you purchase a commitment, your commitment fee does not change and you still receive the same discount percentage on applicable usage.

## Eligible resources

Firestore CUDs automatically apply to your spending on Firestore operations usage as measured in Read/Write/Delete operations across projects.

Firestore CUDs don't apply to your spending on Firestore resources other than Read/Write/Delete operations.

For a list of applicable SKUs, see [Firestore Eligible SKUs](https://cloud.google.com/skus/sku-groups/cloud-firestore-cud-eligible-skus) .

## Purchase a commitment

Before you purchase a commitment, read the [Service Specific Terms](https://cloud.google.com/terms/service-terms) regarding Committed Units.

After you purchase a commitment, the discount goes into effect within the next hour and is automatically applied to subsequent eligible usage.

Make sure that the size and duration of your commitment aligns with both your historical and your expected minimum expenditure on Firestore operations.

**Caution:** After you purchase a commitment, you can't cancel the CUD.

To purchase or manage CUDs for a Cloud Billing account, follow the instructions at [Purchasing spend-based commitments](https://cloud.google.com/docs/cuds-spend-based#purchasing) .

## An example Firestore CUD scenario

Ideally, your commitment represents at least your expected minimum hourly expenditure on Firestore Read/Write/Delete operations across your projects over the next one or three years.

**Note:** The prices in this section are examples. See [Firestore Pricing](/firestore/pricing) for current prices.

As an example, say that you have a Firestore database that is in region: `  us-central1  ` (Iowa).

From the [pricing page](/firestore/pricing) , you can calculate the approximate hourly one-year commitment cost as follows:

  - Monthly cost of a 1-year, $1.92/hour commitment: ($2.40 per hour - 20% discount) \* 730 hours = $1,401.60 per month
  - Total savings per month: $1,752 - $1,401.60 = $350.40

If you expect to spend that minimum of $1.92 per hour continuously for the next year or more, then you can make a commitment for that amount. In other words, when purchasing that CUD, you would enter " `  $1.92  ` " as the hourly commitment amount.

In the legacy CUDs program, your commitment amount is the on-demand price instead. For more information about the differences between the legacy and new spend-based CUDs program, see [Improvements to the spend-based CUDs program](https://cloud.google.com/docs/cuds-multiprice) .

If, on the other hand, you expect to scale down the capacity occasionally, you can make a commitment for a lower amount. Any expenditure higher than that limit is charged at the on-demand rate.

As a basis for comparison, compute the on-demand cost of Firestore capacity, without the application of any commitment discounts:

  - Read operations expenditure: 2 million document reads per hour \* $0.03 per 100,000 document reads = $0.60 per hour

  - Write operations expenditure: 2 million document writes per hour \* $0.09 per 100,000 document writes = $1.80 per hour

  - Total expenditure: $0.60 + $1.80 = $2.40 per hour

  - Monthly cost based on on-demand pricing: $2.40 per hour \* 730 hours = $1,752 per month.

From here, you can calculate the monthly costs and savings that you would see under a 1-year commitment with a 20% discount compared to a year of paying the full rates:

  - Monthly cost of a 1-year, $1.92/hour commitment: ($2.40 per hour - 20% discount) \* 730 hours = $1,401.60 per month
  - Total savings per month: $1,752 - $1,401.60 = $350.40
  - Total savings with a 1-year, $1.92/hour commitment: $350.40 per month \* 12 months = **$4,204.80**

You can apply similar math to calculating the costs and savings of a 3-year CUD, a 40% discount compared to the on-demand rates:

  - Monthly cost of a 3-year, $1.44/hour commitment: ($2.40 per hour - 40% discount) \* 730 hours = $1,051.20 per month
  - Total savings per month: $1,752 - $1,051.20 = $700.80
  - Total savings with a 3-year, $1.44/hour commitment: $700.80 per month \* 36 months = **$25,228.80**

A commitment that covers your expected minimum Firestore usage over the years to come can lead to significant savings.

## Recommendations for choosing a commitment amount

While considering Firestore CUDs and the amount that you want to commit to, keep in mind the following:

  - **Regions:** Firestore CUDs apply to all Read/Write/Delete operations in a project, regardless of which region they are in. If you have Firestore databases in multiple regions, calculate the expenditure across all the regions that your projects use before deciding whether to purchase a commitment.

  - **Projects:** Determine the consistent baseline expenditure per project while calculating total commitment. Consider that production loads usually run 100% of the time, while development or staging environments might often run intermittently.

Your commitment fee applies to every hour during the term of the commitment, regardless of actual usage. Choose your commitment amount carefully, based on both your historical Firestore usage and your future expectations. As long as your use of Firestore Read/Write/Delete operations stays above your committed expenditure level, you receive the maximum possible discount for the length of the commitment.

## What's next

  - Read an [overview of Firestore pricing](https://cloud.google.com/firestore/pricing) .
  - Understand [reads and writes at scale](/firestore/docs/understand-reads-writes-scale)
  - Learn how to [view your CUD reports](/billing/docs/how-to/cud-analysis) .
  - Understand savings with [cost breakdown reports](/billing/docs/how-to/cost-breakdown) .
  - View the [list of Google Cloud services that offer CUDs](/docs/cuds) .
