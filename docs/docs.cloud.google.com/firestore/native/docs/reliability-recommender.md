# Reliability recommender

The Reliability recommender supports the following recommendation subtypes:

  - [Enable scheduled backups](/firestore/docs/backups)
  - [Enable PITR](/firestore/docs/pitr)

which are a part of [Disaster Recovery Plan](/firestore/docs/disaster-recovery) to protect your data against data disasters such as accidental deletion or modification of data.

This document describes how to enable and view your recommendations and insights to improve the reliability of your databases.

## Before you begin

Before you can view Firestore reliability recommendations and insights, do the following:

1.  Enable the Recommender API as described in [Enable the API](/recommender/docs/enabling) .

2.  Ensure that you have sufficient permissions. You must have one of the following roles, which provide the necessary permissions:
    
    <table>
    <colgroup>
    <col style="width: 45%" />
    <col style="width: 55%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Task description</th>
    <th>Role</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>View recommendations/insights</td>
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasereliabilityViewer        </code></td>
    </tr>
    <tr class="even">
    <td>View and update (dismiss) recommendations/insights</td>
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasereliabilityAdmin        </code></td>
    </tr>
    <tr class="odd">
    <td>Opt out of recommendations/insights in Transparency and Control Center. For more information, see <a href="/recommender/docs/opting-out">Opting out</a> .</td>
    <td><code dir="ltr" translate="no">         roles/dataprocessing.admin        </code></td>
    </tr>
    </tbody>
    </table>
    
    These Recommender roles provide the following API permissions:
    
    <table>
    <colgroup>
    <col style="width: 45%" />
    <col style="width: 55%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Role</th>
    <th>Included permissions</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasereliabilityViewer        </code></td>
    <td><code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityRecommendations.get        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityRecommendations.list        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityInsights.get        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityInsights.list        </code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasereliabilityAdmin        </code></td>
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasereliabilityViewer        </code> permissions, plus<br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityRecommendations.update        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseReliabilityInsights.update        </code></td>
    </tr>
    </tbody>
    </table>
    
    For more information about roles and about granting access, see the following:
    
      - [Understanding roles](/iam/docs/understanding-roles)
      - [Managing access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access)

## View recommendations

You can list Reliability recommendations in different ways.

You can view reliability recommendations only if you have non-empty, in-use databases that don't have scheduled backups or PITR enabled.

### Google Cloud console

You can view your recommendations by doing following:

1.  Go to the Google Cloud console, or use the following button:

2.  Select the **Recommendations** tab.

### gcloud CLI

To list reliability recommendations by using `  gcloud  ` , run the [`  gcloud recommender recommendations list  `](/sdk/gcloud/reference/recommender/recommendations/list) command as follows:

``` text
  gcloud recommender recommendations list \
  --project=PROJECT_ID \
  --location=LOCATION \
  --recommender=google.firestore.database.<var>RECOMMENDER</var>
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID
  - `  LOCATION  ` : A region, such as `  us-central1  `
  - `  RECOMMENDER  ` : The ID of the recommender as `  ReliabilityRecommender  ` .

### Recommender API

To list your reliability recommendations by using the [Recommendations API](/recommender/docs/using-api) , call the [`  recommendations.list  `](/recommender/docs/reference/rest/v1beta1/projects.locations.recommenders.recommendations/list) method as follows:

``` text
  curl -H "Authorization: Bearer $(gcloud auth print-access-token)"  \
  -H "x-goog-user-project: PROJECT_ID" \
  "https://recommender.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/recommenders/google.firestore.database.RECOMMENDER/recommendations"
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : A region, such as `  us-central1  ` .
  - `  RECOMMENDER  ` : The ID of the recommender as `  ReliabilityRecommender  ` .

For more information, see [Using the API - Recommendations](/recommender/docs/using-api) .

## View insights

You can view insights and detailed recommendations about disaster recovery plan in different ways.

### Console

To view insights and detailed recommendations by using the Google Cloud console, click the recommendation button in the list of databases.

### gcloud CLI

To view insights by using `  gcloud  ` , run the [`  gcloud recommender insights list  `](/sdk/gcloud/reference/recommender/insights/list) command as follows:

``` text
  gcloud recommender insights list \
  --project=PROJECT_ID \
  --location=LOCATION \
  --insight-type=google.firestore.database.INSIGHT_TYPE
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : A region, such as `  us-central1  ` .
  - `  INSIGHT_TYPE  ` : The ID of the insight type as `  ReliabilityInsight  ` .

### Recommender API

To list your insights by using the Recommender API, run the following command:

``` text
curl -H "Authorization: Bearer $(gcloud auth print-access-token)"  \

"https://recommender.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/insightTypes/google.firestore.database.INSIGHT_TYPE/insights"
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : A region, such as `  us-central1  ` .
  - `  INSIGHT_TYPE  ` : The ID of the insight type as `  ReliabilityInsight  ` .

For more information, see [Using the API - Insights](/recommender/docs/insights/using-api) .

## Apply recommendations

For more information about how to improve your disaster recovery plan, see [Plan disaster recovery](/firestore/native/docs/disaster-recovery) .

## Pricing

Reliability recommendations and insights are available free of charge. For information about other pricing tiers, see [Recommender pricing](/recommender/pricing) .
