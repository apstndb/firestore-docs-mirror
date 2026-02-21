This page describes how to access a Firestore in Datastore mode database from different platforms.

## Before you begin

This document assumes that you've already created a Datastore mode database. If you haven't created a database, follow the instructions in the [Firestore in Datastore mode Quickstart](/datastore/docs/store-query-data) .

## Access your database from App Engine

To get started with Datastore mode and App Engine, see one of the following language-specific pages:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><a href="/appengine/docs/standard">App Engine Standard Environment</a></th>
<th><a href="/appengine/docs/flexible">App Engine Flexible Environment</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><a href="/appengine/docs/standard/python/datastore#connecting_to_datastore_name_short_with_app_engine">Python</a></li>
<li><a href="/appengine/docs/standard/java/datastore#connecting_to_datastore_name_short_with_app_engine">Java</a></li>
<li><a href="/appengine/docs/standard/go/datastore#connecting_to_datastore_name_short_with_app_engine">Go</a></li>
<li><a href="/appengine/docs/standard/nodejs/using-cloud-datastore">Node.js</a></li>
</ul></td>
<td><ul>
<li><a href="/appengine/docs/flexible/python/using-cloud-datastore">Python</a></li>
<li><a href="/appengine/docs/flexible/java/using-cloud-datastore">Java</a></li>
<li><a href="/appengine/docs/flexible/nodejs/using-cloud-datastore">Node.js</a></li>
<li><a href="/appengine/docs/flexible/go/using-cloud-datastore">Go</a></li>
<li><a href="/appengine/docs/flexible/ruby/using-cloud-datastore">Ruby</a></li>
<li><a href="/appengine/docs/flexible/php/using-cloud-datastore">PHP</a></li>
</ul></td>
</tr>
</tbody>
</table>

### Datastore mode permissions for App Engine

App Engine apps can access a Datastore mode database in the same project by default. Each App Engine app uses an [App Engine default service account](/appengine/docs/standard/python/service-account) to manage access to Google Cloud services such as Firestore. By default, the App Engine default service account has the Project Editor [IAM role](/iam/docs/overview#roles) , which includes full read and write access to Datastore mode.

You can [modify the IAM permissions of your App Engine default service account](/appengine/docs/standard/python/service-account#changing_service_account_permissions_) , but your app might lose access to Firestore unless you assign an IAM role with the [required Firestore permissions](/datastore/docs/access/iam#required_permissions) . The [Datastore Owner](/datastore/docs/access/iam#iam_roles) and [Datastore User](/datastore/docs/access/iam#iam_roles) IAM roles, for example, grant read and write access to Firestore in Datastore mode.

If you disable or delete your App Engine default service account, your App Engine app will lose access to your Datastore mode database. If you disabled your App Engine service account, you can re-enable it, see [enabling a service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts#enabling) . If you deleted your App Engine service account within the last 30 days, you can restore your service account, see [undeleting a service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts#undeleting) .

## Access your database from a Compute Engine instance

This section shows how to activate and access a Datastore mode database from a [Compute Engine](/compute) VM instance in a new or existing project.

### Datastore mode permissions for Compute Engine

Compute Engine apps can access a Datastore mode database in the same project by default. Each Compute Engine app uses an [Compute Engine default service account](/compute/docs/access/service-accounts#default_service_account) to manage access to Google Cloud services such as Firestore. By default, the Compute Engine default service account has the Project Editor [IAM role](/iam/docs/overview#roles) , which includes full read and write access to Datastore mode.

To access your database from a Compute Engine instance, complete the following steps:

1.  Enable the Google Compute Engine API for your project.  

2.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Create a Compute Engine instance.

### Console

1.  In the Google Cloud console, go to the [**VM Instances**](https://console.cloud.google.com/compute/instances) page.
2.  Click the **Create instance** button.
3.  In the **Identity and API access** section, set **Access scopes** to provide access for Datastore. Either click **Allow full access to all Cloud APIs** to grant access to all Google Cloud APIs, or click **Set access for each API** , click the dropdown for **Datastore** , and then click **Enabled** to grant access to Datastore.
4.  Click the **Create** button to create the VM instance.
5.  Confirm that your [instance is running](/compute/docs/instances/checking-instance-status) .
6.  To use this new Compute Engine VM instance, [connect](/compute/docs/instances/connecting-to-instance) to it using your browser.

### gcloud

1.  If you haven't already done this, [install](/sdk/docs/install) the Google Cloud CLI and [set up `  gcloud compute  `](/compute/docs/gcloud-compute) .

2.  Add a Compute Engine VM instance and start it, following the instructions for [starting an instance](/compute/docs/instances/creating-and-starting-an-instance#startinstancegcloud) in the Compute Engine documentation. Specify the project ID, the VM instance name, and either the `  cloud-platform  ` or the `  datastore  ` [scope](/compute/docs/access/service-accounts#accesscopesiam) as shown in the following example.
    
    ``` text
    export PROJECT_ID=[YOUR_PROJECT_ID]
    export INSTANCE_NAME=[YOUR_INSTANCE_NAME]
    gcloud compute instances create $INSTANCE_NAME --project $PROJECT_ID --scopes datastore
    ```
    
    Replace `  [YOUR_PROJECT_ID]  ` with the ID of the project you created previously and `  [YOUR_INSTANCE_NAME]  ` with the name you want to use for your VM instance.

3.  Confirm that your [instance is running](/compute/docs/instances/checking-instance-status) .

4.  To use this new VM instance, [connect](/compute/docs/instances/connecting-to-instance) to the VM.

At this point all services and authorizations are configured for your project and you can start [writing code](/datastore/docs/datastore-api-tutorial) or [exploring the API](https://developers.google.com/apis-explorer/#search/datastore/) .

## Access your database from another platform

This section shows how to access your Datastore mode database from an external application running on a platform outside of Google Cloud.

First, create a service account:

1.  In the Google Cloud console, go to the **Create service account** page.

2.  Select a project.

3.  In the **Service account name** field, enter a name. The Google Cloud console fills in the **Service account ID** field based on this name.

4.  Optional: In the **Service account description** field, enter a description.

5.  Click **Create** .

6.  Click the **Select a role** field.
    
    Under **All roles** , select a role that grants access to your database, such as **Datastore** \> **Cloud Datastore User** .

7.  Click **Continue** .

8.  Click **Done** to finish creating the service account.
    
    Do not close your browser window. You will use it in the next procedure.

Then create a service account key:

1.  In the Google Cloud console, click the email address for the service account that you created.
2.  Click **Keys** .
3.  Click **Add key** , then **Create new key** .
4.  Click **Create** . A JSON key file is downloaded to your computer.
5.  Click **Close** .

Use this service account to configure credentials for your application code as described in [Providing service account credentials](/docs/authentication/production#providing_service_account_credentials) .

## Quotas and billing

A certain amount of free quota is available, as described in [Pricing and Quota](/datastore/docs/pricing) . This means you aren't required to enable billing to get started or to use Firestore in Datastore mode up to the free quota limits. However, if you need more resources than is provided by the free quota, you must enable billing.

## What's next

  - Learn about [setting up authentication with client libraries](/datastore/docs/reference/libraries#setting_up_authentication) .
  - Understand the [how your credentials are used by client libraries](/docs/authentication#adc) .

To enable billing, see [Enable billing for a project](/billing/docs/how-to/modify-project#enable_billing_for_a_project) .
