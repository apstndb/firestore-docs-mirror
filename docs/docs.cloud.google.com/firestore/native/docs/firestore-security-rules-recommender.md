# Firestore Security Rules recommender

The Firestore Security Rules recommender supports the following recommendation subtype:

  - [Update Insecure Policy](/firestore/docs/security/insecure-rules)

which are security concerns for Firestore customers providing users extra access than the users intend.

This document describes how to enable and view your recommendations and insights to improve the security of your databases.

## Before you begin

Before you can view Firestore Firestore Security rules recommendations and insights, do the following:

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
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasefirebaserulesViewer        </code></td>
    </tr>
    <tr class="even">
    <td>View and update (dismiss) recommendations/insights</td>
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasefirebaserulesAdmin        </code></td>
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
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasefirebaserulesViewer        </code></td>
    <td><code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesRecommendations.get        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesRecommendations.list        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesInsights.get        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesInsights.list        </code></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasefirebaserulesAdmin        </code></td>
    <td><code dir="ltr" translate="no">         roles/recommender.firestoredatabasefirebaserulesViewer        </code> permissions, plus<br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesRecommendations.update        </code><br />
    <code dir="ltr" translate="no">         recommender.firestoreDatabaseFirebaseRulesInsights.update        </code></td>
    </tr>
    </tbody>
    </table>
    
    For more information about roles and about granting access, see the following:
    
      - [Understanding roles](/iam/docs/understanding-roles)
      - [Managing access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access)

You can view Firestore Security rules recommendations only if you have non-empty, in-use databases that have any rules exposed to broad access configured. The project must be at least 30 days old for recommendations to be generated for it.

You can view Firestore Security rules recommendations/insights in different ways:

## View recommendations

### Google Cloud console

You can view your recommendations by doing following:

Go to the Google Cloud console, or use the following button:

Recommendations can be viewed on **Recommendation Hub** or **Database Center** page.

1.  Search for **Recommendations** which will lead to the Recommendation Hub page. You can select specific category of recommendation and view them.

2.  Search for **Database Center** . You can apply product filter and view the specific fleet issues.

### gcloud CLI

To list Firestore Security rules recommendations by using `  gcloud  ` , run the [`  gcloud recommender recommendations list  `](/sdk/gcloud/reference/recommender/recommendations/list) command as follows:

``` text
  gcloud recommender recommendations list \
  --project=PROJECT_ID \
  --location=LOCATION \
  --recommender=google.firestore.database.<var>RECOMMENDER</var>
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID
  - `  LOCATION  ` : A region, such as `  us-central1  `
  - `  RECOMMENDER  ` : The ID of the recommender as `  FirebaseRulesRecommender  ` .

### Recommender API

To list your Firestore Security rules recommendations by using the [Recommendations API](/recommender/docs/using-api) , call the [`  recommendations.list  `](/recommender/docs/reference/rest/v1beta1/projects.locations.recommenders.recommendations/list) method as follows:

``` text
  curl -H "Authorization: Bearer $(gcloud auth print-access-token)"  \
  -H "x-goog-user-project: PROJECT_ID" \
  "https://recommender.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/recommenders/google.firestore.database.RECOMMENDER/recommendations"
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : A region, such as `  us-central1  ` .
  - `  RECOMMENDER  ` : The ID of the recommender as `  FirebaseRulesRecommender  ` .

For more information, see [Using the API - Recommendations](/recommender/docs/using-api) .

## View insights

You can view insights and detailed recommendations about Firestore Security rules in different ways.

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
  - `  INSIGHT_TYPE  ` : The ID of the insight type as `  FirebaseRulesInsight  ` .

### Recommender API

To list your insights by using the Recommender API, run the following command:

``` text
curl -H "Authorization: Bearer $(gcloud auth print-access-token)"  \

"https://recommender.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/insightTypes/google.firestore.database.INSIGHT_TYPE/insights"
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : A region, such as `  us-central1  ` .
  - `  INSIGHT_TYPE  ` : The ID of the insight type as `  FirebaseRulesInsight  ` .

For more information, see [Using the API - Insights](/recommender/docs/insights/using-api) .

## Apply recommendations

For more information about how to improve your database security, see [Structure security rules](/firestore/docs/security/rules-structure) .

## Pricing

Firestore Security rules recommendations and insights are available free of charge. For information about other pricing tiers, see [Recommender pricing](/recommender/pricing) .
