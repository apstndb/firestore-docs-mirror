# About saved queries

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how saved queries work in Firestore with MongoDB compatibility .

You can use Firestore Studio to create, save, and manage queries. The saved queries capability is available only in the Google Cloud console.

Saved queries have the following characteristics:

  - Google-owned and Google-managed encryption keys encrypt all queries at rest.
  - A saved query is a child of a project.
  - Saved queries are deleted when the project is deleted. If you delete the instance or database, you can still access saved queries in the project using the [**Saved queries** page](/firestore/mongodb-compatibility/docs/create-manage-saved-queries) in the Google Cloud console.
  - You must have the correct [Identity and Access Management (IAM) role or permissions](/firestore/mongodb-compatibility/docs/create-manage-saved-queries#required-roles) to view and manage saved queries.
  - You can only access saved queries using the Firestore Studio or by navigating to the **Saved queries** page in the Google Cloud console. Saved queries aren't accessible through the API.

## Storage location

Firestore with MongoDB compatibility attempts to store queries in the same location as the database. However, storage for saved queries is available in a limited number of locations, so it might select another region by default. To view and update the location where your saved queries are stored, first click **Show Advanced Options** from the save subtask. Then, from the **Region** list, select an available location.

## Limitations

Saved queries has the following limitations:

  - You can't create more than 10,000 saved queries in a project—including saved queries for other Google Cloud products. For more information, see [Quotas and limits](/firestore/mongodb-compatibility/quotas) .
  - You can't use [customer-managed encryption keys](/spanner/docs/cmek) for instances with saved queries.

## Pricing

There is no additional charge for using or storing saved queries.

## What's next

  - Learn how to [create and manage saved queries](/firestore/mongodb-compatibility/docs/create-manage-saved-queries) .
  - Learn how to [manage Firestore with the Google Cloud console](/firestore/native/docs/using-console) .
