# Use the Firestore remote MCP server

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to use the Firestore remote Model Context Protocol (MCP) server to connect to Firestore from AI applications such as Gemini CLI, Claude, or in AI applications that you're developing. The Firestore remote MCP server lets you interact with documents stored in a Firestore database from you AI application. .

[Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) standardizes how large language models (LLMs) and AI applications or agents connect to external data sources. MCP servers let you use their tools, resources, and prompts to take actions and get updated data from their backend service.

## What's the difference between local and remote MCP servers?

  - Local MCP servers  
    Typically run on your local machine and use the standard input and output streams (stdio) for communication between services on the same device.
  - Remote MCP servers  
    Run on the service's infrastructure and offer an HTTP endpoint to AI applications for communication between the AI MCP client and the MCP server. For more information about MCP architecture, see [MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture) .

## Before you begin

1.  Select a Firestore in Native mode database to use or [create one](/firestore/native/docs/manage-databases#create_a_database) . Only Native mode databases in Enterprise or Standard edition support the remote MCP server.

### Required roles

To get the permissions that you need to enable the Firestore MCP server and interact with Firestore documents, ask your administrator to grant you the following IAM roles on the project where you want to enable the Firestore MCP server:

  - [Service Usage Admin](/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageAdmin) ( `  roles/serviceusage.serviceUsageAdmin  ` )
  - Make MCP tool calls: [MCP Tool User](/iam/docs/roles-permissions/mcp#mcp.toolUser) ( `  roles/mcp.toolUser  ` )
  - Read and edit Firestore documents: [Firestore User](/iam/docs/roles-permissions/firestore#datastore.user) ( `  roles/datastore.user  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to enable the Firestore MCP server and interact with Firestore documents. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to enable the Firestore MCP server and interact with Firestore documents:

  - `  serviceusage.mcppolicy.get  `
  - `  serviceusage.mcppolicy.update  `
  - Make MCP tool calls: `  mcp.tools.call  `
  - Read and edit Firestore documents:
      - `  datastore.entities.allocateIds  `
      - `  datastore.entities.create  `
      - `  datastore.entities.delete  `
      - `  datastore.entities.get  `
      - `  datastore.entities.list  `
      - `  datastore.entities.update  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Enable or disable the Firestore MCP server

You can enable or disable the Firestore MCP server in a project with the `  gcloud beta services mcp enable  ` command. For more information, see the following sections.

### Enable the Firestore MCP server in a project

**Note:** After March 17, 2026, the Firestore remote MCP server is automatically enabled when you enable Firestore.

If you are using different projects for your client credentials, such as service account keys, OAuth client ID or API keys, and for hosting your resources, then you must enable the Firestore service and the Firestore remote MCP server on both projects.

To enable the Firestore MCP server in your Google Cloud project, run the following command:

``` text
gcloud beta services mcp enable firestore.googleapis.com \
    --project=PROJECT_ID
```

Replace `  PROJECT_ID  ` with the Google Cloud project ID.

The Firestore remote MCP server is enabled for use in your Google Cloud Project. If the Firestore service isn't enabled for your Google Cloud project, you are prompted to enable the service before enabling the Firestore remote MCP server.

As a security best practice, we recommend that you enable MCP servers only for the services required for your AI application to function.

### Disable the Firestore MCP server in a project

To disable the Firestore MCP server in your Google Cloud project, run the following command:

``` text
gcloud beta services mcp disable SERVICE \
    --project=PROJECT_ID
```

The Firestore MCP server is disabled for use in your Google Cloud Project.

## Authentication and authorization

Firestore MCP servers use the [OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) protocol with [Identity and Access Management (IAM)](/iam/docs/overview) for authentication and authorization. All [Google Cloud identities](/docs/authentication/identity-products) are supported for authentication to MCP servers.

We recommend creating a separate identity for agents using MCP tools so that access to resources can be controlled and monitored. For more information on authentication, see [Authenticate to MCP servers](/mcp/authenticate-mcp) .

## Firestore MCP OAuth scopes

OAuth 2.0 uses scopes and credentials to determine if an authenticated principal is authorized to take a specific action on a resource. For more information about OAuth 2.0 scopes at Google, read [Using OAuth 2.0 to access Google APIs](https://developers.google.com/identity/protocols/oauth2) .

Firestore has the following MCP tool OAuth scopes:

<table>
<thead>
<tr class="header">
<th>Scope URI for gcloud CLI</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       https://www.googleapis.com/auth/cloud-platform      </code></td>
<td>See, edit, configure, and delete your Google Cloud data and see the email address for your Google Account.</td>
</tr>
</tbody>
</table>

Additional scopes might be required on the resources accessed during a tool call. To view a list of scopes required for Firestore, see [Firestore API](https://developers.google.com/identity/protocols/oauth2/scopes#firestore) .

## Configure an MCP client to use the Firestore MCP server

AI applications and agents, such as Claude or Gemini CLI, can instantiate an MCP client that connects to a single MCP server. An AI application can have multiple clients that connect to different MCP servers. To connect to a remote MCP server, the MCP client must know at a minimum the URL of the remote MCP server.

In your AI application, look for a way to connect to a remote MCP server. You are prompted to enter details about the server, such as its name and URL.

For the Firestore MCP server, enter the following as required:

  - **Server name** : Firestore MCP server
  - **Server URL** or **Endpoint** : firestore.googleapis.com/mcp
  - **Transport** : HTTP
  - **Authentication details** : Depending on how you want to authenticate, you can enter your Google Cloud credentials, your OAuth Client ID and secret, or an agent identity and credentials. For more information on authentication, see [Authenticate to MCP servers](/mcp/authenticate-mcp) .
  - **OAuth scope** : the [OAuth 2.0 scope](https://developers.google.com/identity/protocols/oauth2/scopes) that you want to use when connecting to the Firestore MCP server.

For host specific guidance, see the following:

  - [Claude.ai](/mcp/configure-mcp-ai-application#claude-ai)
  - [Gemini CLI](/mcp/configure-mcp-ai-application#gemini-cli)

For more general guidance, see the following resources:

  - [Connect to remote MCP servers](https://modelcontextprotocol.io/docs/develop/connect-remote-servers) .
  - [Configure MCP in an AI application](/mcp/configure-mcp-ai-application) .

## Available tools

To view details of available MCP tools and their descriptions for the Firestore MCP server, see the [Firestore MCP reference](/firestore/docs/reference/mcp) .

### List tools

Use the [MCP inspector](https://modelcontextprotocol.io/docs/tools/inspector) to list tools, or send a `  tools/list  ` HTTP request directly to the Firestore remote MCP server. The `  tools/list  ` method doesn't require authentication.

``` text
POST /mcp HTTP/1.1
Host: firestore.googleapis.com
Content-Type: application/json

{
  "jsonrpc": "2.0",
  "method": "tools/list",
}
```

## Sample use cases

The following are sample use cases and prompts for the Firestore MCP server:

  - "What tools are available for the Firestore MCP server?"
  - "Add a document with collection "book" under my Firestore database "my-database" with the Google Cloud project "my-project" with generated book info."
  - "Get the information for the book with ID 3VyGFIAPRHUNeuH5h2eb from the book collection."
  - "Update the year field of document 3VyGFIAPRHUNeuH5h2eb to 1995."
  - "List all books under the book collection."
  - "List all collections IDs under the root of the "my-database" Firestore database."
  - "Delete the document 3VyGFIAPRHUNeuH5h2eb under the book collection."

## Optional security and safety configurations

MCP introduces new security risks and considerations due to the wide variety of actions that can be taken with MCP tools. To minimize and manage these risks, Google Cloud offers defaults and customizable policies to control the use of MCP tools in your Google Cloud organization or project.

For more information about MCP security and governance, see [AI security and safety](/mcp/ai-security-safety) .

### Use Model Armor

Model Armor is a Google Cloud service designed to enhance the security and safety of your AI applications. It works by proactively screening LLM prompts and responses, protecting against various risks and supporting responsible AI practices. Whether you are deploying AI in your cloud environment, or on external cloud providers, Model Armor can help you prevent malicious input, verify content safety, protect sensitive data, maintain compliance, and enforce your AI safety and security policies consistently across your diverse AI landscape.

Model Armor is only available in specific regional locations. If Model Armor is enabled for a project, and a call to that project comes from an unsupported region, Model Armor makes a cross-regional call. For more information, see [Model Armor locations](/model-armor/locations) .

**Caution:** Model Armor logs the entire payload if a request fails. This might expose sensitive information in the logs.

#### Enable Model Armor

You must enable Model Armor APIs before you can use Model Armor.

### Console

1.  Enable the Model Armor API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

2.  Select the project where you want to activate Model Armor.

### gcloud

Before you begin, follow these steps using the Google Cloud CLI with the Model Armor API:

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  Run the following command to set the API endpoint for the Model Armor service.
    
    ``` text
    gcloud config set api_endpoint_overrides/modelarmor "https://modelarmor.LOCATION.rep.googleapis.com/"
    ```
    
    Replace `  LOCATION  ` with the region where you want to use Model Armor.

#### Configure protection for Google and Google Cloud remote MCP servers

To protect your MCP tool calls and responses, you create a Model Armor floor setting and then enable MCP content security for your project. A floor setting defines the minimum security filters that apply across the project. This configuration applies a consistent set of filters to all MCP tool calls and responses within the project.

**Tip:** Don't enable the prompt injection and jailbreak filter unless your MCP traffic carries natural language data.

1.  Set up a Model Armor floor setting with MCP sanitization enabled. For more information, see [Configure Model Armor floor settings](https://docs.cloud.google.com/model-armor/configure-floor-settings) .
    
    **Note:** If the agent and the MCP server are in different projects, you can create floor settings in both projects (the client project and the resource project). In this case, Model Armor is invoked twice, once for each project.
    
    See the following example command:
    
    ``` text
    gcloud model-armor floorsettings update \
    --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
    --enable-floor-setting-enforcement=TRUE \
    --add-integrated-services=GOOGLE_MCP_SERVER \
    --google-mcp-server-enforcement-type=INSPECT_AND_BLOCK \
    --enable-google-mcp-server-cloud-logging \
    --malicious-uri-filter-settings-enforcement=ENABLED \
    --add-rai-settings-filters='[{"confidenceLevel": "HIGH", "filterType": "DANGEROUS"}]'
    ```
    
    Replace `  PROJECT_ID  ` with your Google Cloud project ID.
    
    Note the following settings:
    
      - `  INSPECT_AND_BLOCK  ` : The enforcement type that inspects content for the Google MCP server and blocks prompts and responses that match the filters.
      - `  ENABLED  ` : The setting that enables a filter or enforcement.
      - `  HIGH  ` : The confidence level for the Responsible AI - Dangerous filter settings. You can modify this setting, though lower values might result in more false positives. For more information, see [Configure floor settings](https://docs.cloud.google.com/model-armor/configure-floor-settings) .

2.  For your project, enable Model Armor protection for remote MCP servers.
    
    ``` text
    gcloud beta services mcp content-security add modelarmor.googleapis.com --project=PROJECT_ID
    ```
    
    Replace `  PROJECT_ID  ` with your Google Cloud project ID. After you run this command, Model Armor sanitizes all MCP tool calls and responses from the project, regardless of where the calls and responses originate.

3.  To confirm that Google MCP traffic is sent to Model Armor, run the following command:
    
    ``` text
    gcloud beta services mcp content-security get --project=PROJECT_ID
    ```
    
    Replace `  PROJECT_ID  ` with the Google Cloud project ID.

#### Disable scanning MCP traffic with Model Armor

If you want to use Model Armor in a project, and you want to stop scanning Google MCP traffic with Model Armor, run the following command:

``` text
gcloud model-armor floorsettings update \
  --full-uri='projects/PROJECT_ID/locations/global/floorSetting' \
  --remove-integrated-services=GOOGLE_MCP_SERVER
```

Replace `  PROJECT_ID  ` with the Google Cloud project ID.

Model Armor won't scan MCP traffic in the project.

### Control MCP use with IAM deny policies

[Identity and Access Management (IAM) deny policies](/iam/docs/deny-overview) help you secure Google Cloud remote MCP servers. Configure these policies to block unwanted MCP tool access.

For example, you can deny or allow access based on:

  - The principal.
  - Tool properties like read-only.
  - The application's OAuth client ID.

For more information, see [Control MCP use with Identity and Access Management](/mcp/control-mcp-use-iam) .

## What's next

  - Read the [Firestore MCP reference documentation](/firestore/docs/reference/mcp) .
  - Learn more about [Google Cloud MCP servers](/mcp/overview) .
  - Learn how to [use an AI prompt to draft security rules](https://firebase.google.com/docs/ai-assistance/prompt-catalog/write-security-rules)
