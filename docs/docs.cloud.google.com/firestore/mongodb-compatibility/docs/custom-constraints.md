# Manage Firestore with MongoDB compatibility resources using custom constraints

This page shows you how to use Organization Policy Service custom constraints to restrict specific operations on the following Google Cloud resources:

  - `  firestore.googleapis.com/Database  `

To learn more about Organization Policy, see [Custom organization policies](/resource-manager/docs/organization-policy/overview#custom-organization-policies) .

## About organization policies and constraints

The Google Cloud Organization Policy Service gives you centralized, programmatic control over your organization's resources. As the [organization policy administrator](/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) , you can define an organization policy, which is a set of restrictions called *constraints* that apply to Google Cloud resources and descendants of those resources in the [Google Cloud resource hierarchy](/resource-manager/docs/cloud-platform-resource-hierarchy) . You can enforce organization policies at the organization, folder, or project level.

Organization Policy provides built-in [managed constraints](/resource-manager/docs/organization-policy/org-policy-constraints) for various Google Cloud services. However, if you want more granular, customizable control over the specific fields that are restricted in your organization policies, you can also create *custom constraints* and use those custom constraints in an organization policy.

### Policy inheritance

By default, organization policies are inherited by the descendants of the resources on which you enforce the policy. For example, if you enforce a policy on a folder, Google Cloud enforces the policy on all projects in the folder. To learn more about this behavior and how to change it, refer to [Hierarchy evaluation rules](/resource-manager/docs/organization-policy/understanding-hierarchy#disallow_inheritance) .

### Benefits

  - **Security, compliance, and governance** : you can use custom organization policies as follows:
    
      - To enforce disaster recovery requirements, you can require specific disaster recovery settings on databases like delete protection, and point in time recovery.
    
      - You can restrict database creation to only certain locations.
    
      - You can require CMEK (Customer Managed Encryption Key) for databases.

  - **Auditing** : Custom org policy constraints are audit logged. Any operation including constraint modifications and constraint checks will generate corresponding Cloud Audit Logs.

## Before you begin

1.  Ensure that you know your [organization ID](/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id) .

### Required roles

To get the permissions that you need to manage custom organization policies, ask your administrator to grant you the [Organization Policy Administrator](/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) ( `  roles/orgpolicy.policyAdmin  ` ) IAM role on the organization resource. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Set up a custom constraint

A custom constraint is defined in a YAML file by the resources, methods, conditions, and actions that are supported by the service on which you are enforcing the organization policy. Conditions for your custom constraints are defined using [Common Expression Language (CEL)](https://github.com/google/cel-spec/blob/master/doc/intro.md) . For more information about how to build conditions in custom constraints using CEL, see the CEL section of [Creating and managing custom constraints](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) .

### Console

To create a custom constraint, do the following:

In the Google Cloud console, go to the **Organization policies** page.

From the project picker, select the project that you want to set the organization policy for.

Click add **Custom constraint** .

In the **Display name** box, enter a human-readable name for the constraint. This name is used in error messages and can be used for identification and debugging. Don't use PII or sensitive data in display names because this name could be exposed in error messages. This field can contain up to 200 characters.

In the **Constraint ID** box, enter the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example `  custom.disableGkeAutoUpgrade  ` . This field can contain up to 70 characters, not counting the prefix ( `  custom.  ` ), for example, `  organizations/123456789/customConstraints/custom  ` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.

In the **Description** box, enter a human-readable description of the constraint. This description is used as an error message when the policy is violated. Include details about why the policy violation occurred and how to resolve the policy violation. Don't include PII or sensitive data in your description, because it could be exposed in error messages. This field can contain up to 2000 characters.

In the **Resource type** box, select the name of the Google Cloud REST resource containing the object and field that you want to restrict—for example, `  container.googleapis.com/NodePool  ` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.

Under **Enforcement method** , select whether to enforce the constraint on a REST **CREATE** method or on both **CREATE** and **UPDATE** methods. If you enforce the constraint with the **UPDATE** method on a resource that violates the constraint, changes to that resource are blocked by the organization policy unless the change resolves the violation.

Not all Google Cloud services support both methods. To see supported methods for each service, find the service in [Supported services](/resource-manager/docs/organization-policy/custom-constraint-supported-services) .

To define a condition, click edit **Edit condition** .

1.  In the **Add condition** panel, create a CEL condition that refers to a supported service resource, for example, `  resource.management.autoUpgrade == false  ` . This field can contain up to 1000 characters. For details about CEL usage, see [Common Expression Language](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) . For more information about the service resources you can use in your custom constraints, see [Custom constraint supported services](/resource-manager/docs/organization-policy/custom-constraint-supported-services) .
2.  Click **Save** .

Under **Action** , select whether to allow or deny the evaluated method if the condition is met.

The deny action means that the operation to create or update the resource is blocked if the condition evaluates to true.

The allow action means that the operation to create or update the resource is permitted only if the condition evaluates to true. Every other case except ones explicitly listed in the condition is blocked.

Click **Create constraint** .

When you have entered a value into each field, the equivalent YAML configuration for this custom constraint appears on the right.

### gcloud

To create a custom constraint, create a YAML file using the following format:

``` text
name: organizations/ORGANIZATION_ID/customConstraints/CONSTRAINT_NAME
resourceTypes: RESOURCE_NAME
methodTypes:
  - CREATE
- UPDATE 
condition: "CONDITION"
actionType: ACTION
displayName: DISPLAY_NAME
description: DESCRIPTION
```

Replace the following:

  - `  ORGANIZATION_ID  ` : your organization ID, such as `  123456789  ` .
  - `  CONSTRAINT_NAME  ` : the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example, `  custom.deleteProtectionRequired  ` . This field can contain up to 70 characters.
  - `  RESOURCE_NAME  ` : the fully qualified name of the Google Cloud resource containing the object and field that you want to restrict. For example, `  firestore.googleapis.com/Database  ` .
  - `  CONDITION  ` : a [CEL condition](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) that is written against a representation of a supported service resource. This field can contain up to 1000 characters. For example, `  "resource.deleteProtectionState == \"DELETE_PROTECTION_ENABLED\""  ` .
  - `  ACTION  ` : the action to take if the `  condition  ` is met. Possible values are `  ALLOW  ` and `  DENY  ` .
  - `  DISPLAY_NAME  ` : a human-friendly name for the constraint. This field can contain up to 200 characters.
  - `  DESCRIPTION  ` : a human-friendly description of the constraint to display as an error message when the policy is violated. This field can contain up to 2000 characters.

After you have created the YAML file for a new custom constraint, you must set it up to make it available for organization policies in your organization. To set up a custom constraint, use the [`  gcloud org-policies set-custom-constraint  `](/sdk/gcloud/reference/org-policies/set-custom-constraint) command:

``` text
gcloud org-policies set-custom-constraint CONSTRAINT_PATH
```

Replace `  CONSTRAINT_PATH  ` with the full path to your custom constraint file. For example, `  /home/user/customconstraint.yaml  ` .

After this operation is complete, your custom constraints are available as organization policies in your list of Google Cloud organization policies.

To verify that the custom constraint exists, use the [`  gcloud org-policies list-custom-constraints  `](/sdk/gcloud/reference/org-policies/list-custom-constraints) command:

``` text
gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID
```

Replace `  ORGANIZATION_ID  ` with the ID of your organization resource.

For more information, see [Viewing organization policies](/resource-manager/docs/organization-policy/creating-managing-policies#viewing_organization_policies) .

## Enforce a custom organization policy

You can enforce a constraint by creating an organization policy that references it, and then applying that organization policy to a Google Cloud resource.

### Console

1.  In the Google Cloud console, go to the **Organization policies** page.
2.  From the project picker, select the project that you want to set the organization policy for.
3.  From the list on the **Organization policies** page, select your constraint to view the **Policy details** page for that constraint.
4.  To configure the organization policy for this resource, click **Manage policy** .
5.  On the **Edit policy** page, select **Override parent's policy** .
6.  Click **Add a rule** .
7.  In the **Enforcement** section, select whether this organization policy is enforced or not.
8.  Optional: To make the organization policy conditional on a tag, click **Add condition** . Note that if you add a conditional rule to an organization policy, you must add at least one unconditional rule or the policy cannot be saved. For more information, see [Setting an organization policy with tags](/resource-manager/docs/organization-policy/tags-organization-policy) .
9.  Click **Test changes** to simulate the effect of the organization policy. For more information, see [Test organization policy changes with Policy Simulator](/policy-intelligence/docs/test-organization-policies) .
10. To enforce the organization policy in dry-run mode, click **Set dry run policy** . For more information, see [Create an organization policy in dry-run mode](/resource-manager/docs/organization-policy/dry-run-policy) .
11. After you verify that the organization policy in dry-run mode works as intended, set the live policy by clicking **Set policy** .

### gcloud

To create an organization policy with boolean rules, create a policy YAML file that references the constraint:

``` text
name: projects/PROJECT_ID/policies/CONSTRAINT_NAME
spec:
  rules:
  - enforce: true

dryRunSpec:
  rules:
  - enforce: true
```

Replace the following:

  - `  PROJECT_ID  ` : the project that you want to enforce your constraint on.
  - `  CONSTRAINT_NAME  ` : the name you defined for your custom constraint. For example, `  custom.deleteProtectionRequired  ` .

To enforce the organization policy in [dry-run mode](/resource-manager/docs/organization-policy/dry-run-policy) , run the following command with the `  dryRunSpec  ` flag:

``` text
gcloud org-policies set-policy POLICY_PATH --update-mask=dryRunSpec
```

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

After you verify that the organization policy in dry-run mode works as intended, set the live policy with the `  org-policies set-policy  ` command and the `  spec  ` flag:

``` text
gcloud org-policies set-policy POLICY_PATH --update-mask=spec
```

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

## Test the custom organization policy

Before you begin, you must know the following:

  - Your organization ID

<!-- end list -->

1.  Create the `  deleteProtectionRequired.yaml  ` file as follows:
    
    ``` text
     name: organizations/ORGANIZATION_ID/customConstraints/custom.deleteProtectionRequired
     resourceTypes:
     - firestore.googleapis.com/Database
     methodTypes:
     - CREATE
     - UPDATE
     condition: "resource.deleteProtectionState == \"DELETE_PROTECTION_ENABLED\""
     actionType: ALLOW
     displayName: Firestore with MongoDB compatibility Delete Protection Required
     description: To ensure the data security, Delete Protection is required to be enabled for Firestore databases.
    ```
    
    This makes sure that all `  CREATE  ` and `  UPDATE  ` methods on a Firestore with MongoDB compatibility database meet the constraint of `  deleteProtectionState  ` being `  DELETE_PROTECTION_ENABLED  ` . As a result, any databases create/update/restore/clone operations without explicitly enabling Delete Protection are rejected.

2.  Set up the custom constraint at the organization level:
    
    ``` text
    gcloud org-policies set-custom-constraint deleteProtectionRequired.yaml
    ```

### Test the policy

Try to create a database without setting the `  --delete-protection  ` flag in a project in the organization:

``` text
gcloud firestore database create \
   --project=PROJECT_ID \
   --database=DATABASE_ID \
```

The output is the following:

``` text
Operation denied by custom org policies: ["customConstraints/custom.deleteProtectionRequired": "To ensure the data security, Delete Protection is required to be enabled for Firestore databases"]
```

### Test and analyze organization policy changes

We recommend that you test and dry-run all changes to your organization policies, to better understand the state of your environment and how changes affect it.

Policy Simulator for Organization Policy helps you understand the effect of a constraint and organization policy on your current environment. Using this tool, you can review all resource configurations to see where violations occur, before it is enforced on your production environment. For detailed instructions, see [Test organization policy changes with Policy Simulator](https://cloud.google.com/policy-intelligence/docs/test-organization-policies) .

When you understand the current effect, you can create an organization policy in dry-run mode to understand the impact and potential violations of a policy over the next 30 days. An organization policy in dry-run mode is a type of organization policy where violations of the policy are audit-logged, but the violating actions aren't denied. You can create an organization policy in dry-run mode from a custom constraint using the Google Cloud console or Google Cloud CLI. For detailed instructions, see [Create an organization policy in dry-run mode](https://cloud.google.com/resource-manager/docs/organization-policy/dry-run-policy#create_dry_run_boolean_policy) .

## Example custom organization policies for common use cases

This table provides syntax examples for some common custom constraints.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Constraint syntax</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Database names must follow a certain pattern. Note that the format of a database name in custom organization policies is <code dir="ltr" translate="no">       projects/               project-id              /databases/               database-id       </code> while only database-id is specified in database management operations.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.nameSuffixMobile
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
condition: &quot;resource.name.endsWith(&#39;-mobile&#39;)&quot;
actionType: ALLOW
displayName: Firestore database names end with &quot;-mobile&quot;
description: Only allow the creation of database names ending with suffix &quot;-mobile&quot;</code></pre></td>
</tr>
<tr class="even">
<td>Databases can only be created in specified <a href="/firestore/mongodb-compatibility/docs/locations">locations</a> .</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.locationUsCentral1
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
condition: &quot;resource.locationId == &#39;us-central1&#39;&quot;
actionType: ALLOW
displayName: Firestore database location id us-central1
description: Only allow the creation of databases in region us-central1</code></pre></td>
</tr>
<tr class="odd">
<td>Databases must enable <a href="/firestore/mongodb-compatibility/docs/use-pitr">point-in-time-recovery</a> .</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.pitrEnforce
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
- UPDATE
condition: &quot;resource.pointInTimeRecoveryEnablement == &quot;POINT_IN_TIME_RECOVERY_ENABLED&quot;&quot;
actionType: ALLOW
displayName: Firestore database enables PiTR
description: Only allow the creation and updating of a databases if PiTR is enabled.</code></pre></td>
</tr>
<tr class="even">
<td>Don't allow creation of databases unless delete protection is enabled.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.deleteProtectionRequired
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
- UPDATE
condition: &quot;resource.deleteProtectionState == &quot;DELETE_PROTECTION_ENABLED&quot;&quot;
actionType: ALLOW
displayName: Firestore with MongoDB compatibility Delete Protection Required
description: To ensure the data security, Delete Protection is required to be enabled for Firestore databases.
    </code></pre></td>
</tr>
<tr class="odd">
<td>Databases must use the specified <a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases#cmekconfig">CMEK (Customer Managed Encryption Key) configuration</a> .</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.cmekKeyNotDev
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
- UPDATE
condition: &quot;resource.cmekConfig.kmsKeyName.matches(&#39;dev$&#39;)&quot;
actionType: DENY
displayName: Firestore database CMEK key not dev
description: Disallow the creation and updating of databases with CMEK KMS keys ending with &quot;dev&quot;.</code></pre></td>
</tr>
<tr class="even">
<td>Databases must use the specified <a href="https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases#databaseedition">Database Edition</a> .</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>name: organizations/ORGANIZATION_ID/customConstraints/custom.enterpriseEditionRequired
resourceTypes:
- firestore.googleapis.com/Database
methodTypes:
- CREATE
- UPDATE
condition: &quot;resource.databaseEdition == &quot;ENTERPRISE&quot;&quot;
actionType: ALLOW
displayName: Firestore Enterprise Edition Required
description: Only allow the creation and updating of databases with Enterprise Edition.</code></pre></td>
</tr>
</tbody>
</table>

## Firestore with MongoDB compatibility supported resources

The following table lists the Firestore with MongoDB compatibility resources that you can reference in custom constraints.

Resource

Field

firestore.googleapis.com/Database

`  resource.appEngineIntegrationMode  `

`  resource.cmekConfig.kmsKeyName  `

`  resource.concurrencyMode  `

`  resource.deleteProtectionState  `

`  resource.locationId  `

`  resource.name  `

`  resource.pointInTimeRecoveryEnablement  `

`  resource.type  `

## What's next

  - Learn more about [Organization Policy Service](/resource-manager/docs/organization-policy/overview) .
  - Learn more about how to [create and manage organization policies](/resource-manager/docs/organization-policy/using-constraints) .
  - See the full list of managed [organization policy constraints](/resource-manager/docs/organization-policy/org-policy-constraints) .
