# Use Firestore with MCP, Gemini CLI, and other agents

This page shows you how to connect your Firestore database to various developer tools.

For an integrated experience, we recommend using the dedicated Firestore extension for [Gemini CLI](/gemini/docs/codeassist/gemini-cli) . As Google Cloud's next-generation command-line interface, Gemini CLI bundles the underlying MCP server directly into the extension, which removes the need for a separate server setup. You can configure Gemini Code Assist to use the Gemini CLI, offering similar setup benefits in your IDE.

For other developer tools that support the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) , you can connect by manually configuring the [MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) . MCP Toolbox is an open-source MCP server that connects AI agents to your data by managing tasks such as authentication and connection pooling. This lets you interact with your data using natural language directly from your IDE. For these tools, this method provides core database interaction capabilities. This page describes how to use the [MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) to expose your developer assistance tools to a Firestore instance using the following IDEs:

  - [Gemini CLI](#configure-your-mcp-client)
  - [Gemini Code Assist](#configure-your-mcp-client)
  - [Cursor](#configure-your-mcp-client)
  - [Windsurf](#configure-your-mcp-client) (Codium)
  - [Visual Studio Code](#configure-your-mcp-client) (Copilot)
  - [Cline](#configure-your-mcp-client) (VS Code extension)
  - [Claude desktop](#configure-your-mcp-client)
  - [Claude code](#configure-your-mcp-client)

## About Gemini CLI and extensions

Gemini CLI is an open-source AI agent designed to assist with development workflows by assisting with coding, debugging, data exploration, and content creation. Its mission is to provide an agentic interface for interacting with Data Cloud services and popular open-source databases.

### How extensions work

Gemini CLI is highly extensible, allowing for the addition of new tools and capabilities through extensions. You can load the extensions from a GitHub URL, a local directory, or a configurable registry. They provide new tools, slash commands, and prompts to assist with your workflow.

## Use the Gemini CLI extension for Firestore

**Note:** The Firestore Gemini CLI extension is based on MCP Toolbox for Databases. MCP Toolbox for Databases is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

The integration with Gemini CLI is through a dedicated extension that offers additional capabilities compared to the standard MCP Toolbox connection. The extension offers a streamlined installation process and a set of tools. The open-source extension contains detailed information on installation, configuration, and usage examples. For more information, see the [Gemini CLI Extension - Firestore](https://github.com/gemini-cli-extensions/firestore-native) .

The `  firestore-native  ` extension includes tools for querying the database, updating documents, and managing Firestore security rules.

Category

Tools

Example natural language prompt

Document and data retrieval

`  get_documents  `

Show me the Firestore data for the test users qa\_user\_123 and qa\_user\_456 from the users-staging collection.

`  list_collections  `

List all subcollections under the users-staging collection.

`  query_collection  `

Find all users in the users-staging collection whose wishlist contains product-glasses.

Document updates and deletions

`  add_documents  `

Add document qa\_user\_789 to the users-staging collection with fields name: tester1 and location: USA.

`  delete_documents  `

Delete document qa\_user\_789 from the users-staging collection.

`  update_document  `

Update the document with ID order-987 in the orders collection to set the status to 'Shipped'.

For all 20 test users you just found, please remove product-glasses(inactive) from their wishlist.

Security rules management

`  get_rules  `

Show me the active Firestore security rules for this database.

`  validate_rules  `

new\_rules.txt is a new Firestore Security Rule I'm working on for staging. Can you validate it for me?

## Before you begin

To use the tools in the Gemini CLI extension for Firestore, you must have one of the following Identity and Access Management (IAM) roles, or a custom role with equivalent permissions:

<table>
<thead>
<tr class="header">
<th>Task</th>
<th>Role name</th>
<th>Required Identity and Access Management (IAM) role</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Read and write data in Firestore database</td>
<td><a href="/iam/docs/roles-permissions/firestore#datastore.user">Cloud Datastore User</a></td>
<td><code dir="ltr" translate="no">       roles/datastore.user      </code></td>
</tr>
<tr class="even">
<td>View and test security rules</td>
<td><a href="/iam/docs/roles-permissions/firebaserules#firebaserules.viewer">Firebase Rules Viewer</a></td>
<td><code dir="ltr" translate="no">       roles/firebaserules.viewer      </code></td>
</tr>
</tbody>
</table>

## Set up Firestore

1.  [Create a new Google Cloud project](/resource-manager/docs/creating-managing-projects) or [select an existing one](/resource-manager/docs/creating-managing-projects#identifying_projects) .

2.  [Enable the Firestore in Native Mode API](https://console.cloud.google.com/apis/library/firestore.googleapis.com) for your project.

3.  [Create a Firestore database](/firestore/docs/create-database-web-mobile-client-library) if you haven't already.

4.  Set up authentication for your local environment.
    
      - [Install gcloud CLI](/sdk/docs/install)
      - Run `  gcloud auth application-default login  ` to authenticate

## Configure the MCP client

This section describes how to configure various developer tools to connect to your Firestore instance using the [MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) . The toolbox acts as an open-source [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) server that sits between your IDE and your database, providing a secure and efficient control plane for your AI tools. Select the tab for one of the following tools to see the configuration instructions.

### Gemini CLI

1.  Install the [Gemini CLI](https://github.com/google-gemini/gemini-cli?tab=readme-ov-file#-installation) .

2.  Install the Firestore extension for Gemini CLI from the GitHub repository using the following command:
    
    ``` text
    gemini extensions install https://github.com/gemini-cli-extensions/firestore-native
    ```

3.  Set environment variables to connect to your Firestore database. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` :
    
    ``` text
    export FIRESTORE_PROJECT="PROJECT_ID"
    export FIRESTORE_DATABASE="DATABASE_NAME"
    ```
    
    The Gemini CLI extension for Firestore uses your application default credentials (ADC) for authentication.

4.  Start the Gemini CLI in interactive mode:
    
    ``` text
    gemini
    ```
    
    The CLI automatically loads the Firestore extension for Gemini CLI extension and its tools, which you can use to interact with your database.

### Gemini Code Assist

We recommend to configure Gemini Code Assist to use the Gemini CLI, this approach removes the need to manually configure an MCP server.

1.  Make sure you have installed and configured the [Gemini CLI](https://github.com/google-gemini/gemini-cli?tab=readme-ov-file#-installation) and the [`  firestore-native  ` extension](https://github.com/gemini-cli-extensions/firestore-native) .
2.  [Configure Gemini Code Assist to use the Gemini CLI](https://developers.google.com/gemini-code-assist/docs/set-up-gemini-standard-enterprise) .
3.  Start interacting with your Firestore database using natural language directly within the Gemini Code Assist chat.

### Claude code

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Install [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) .
2.  Create the `  .mcp.json  ` file in your project root, if it doesn't exist.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

  

``` text
 {
    "mcpServers": {
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```

4.  Restart Claude code to apply the new configuration.

### Claude desktop

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Open [Claude Desktop](https://claude.ai/download) and navigate to **Settings** .
2.  In the **Developer** tab, click **Edit Config** to open the configuration file.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

  

``` text
 {
    "mcpServers": {
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```

4.  Restart Claude Desktop.
5.  From the new chat screen, you should see a hammer (MCP) icon appear with the new MCP server available.

### Cline

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Open the [Cline](https://github.com/cline/cline) extension in VS Code and tap **MCP Servers** icon.
2.  Click **Configure MCP Servers** to open the configuration file.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

  

``` text
 {
    "mcpServers": {
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```

  
A green active status appears after the server connects successfully.  
  

### Cursor

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Create the `  .cursor  ` directory in your project root if it doesn't exist.
2.  Create the `  .cursor/mcp.json  ` file if it doesn't exist, and open it.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

<!-- end list -->

``` text
 {
    "mcpServers": {
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```

4.  Open [Cursor](https://www.cursor.com/) and navigate to **Settings \> Cursor Settings \> MCP** . A green active status appears when the server connects.

### Visual Studio Code (Copilot)

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Open [VS Code](https://code.visualstudio.com/docs/copilot/overview) and create `  .vscode  ` directory in your project root if it does not exist.
2.  Create the `  .vscode/mcp.json  ` file if it doesn't exist, and open it.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

<!-- end list -->

``` text
 {
    "servers":{
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```

### Windsurf

#### Install MCP Toolbox for Databases

1.  Download the latest version of Toolbox as a binary. Select the [binary](https://github.com/googleapis/genai-toolbox/releases) corresponding to your operating system (OS) and CPU architecture. You must use Toolbox version V0.15.0 or later.
    
    ### linux/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/linux/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/arm64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/arm64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### darwin/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/darwin/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .
    
    ### windows/amd64
    
    ``` text
    curl -O https://storage.googleapis.com/genai-toolbox/version/windows/amd64/toolbox
    ```
    
    Replace `  version  ` with the Toolbox version number, for example `  v0.15.0  ` .

2.  Make the binary executable.
    
    ``` text
    chmod +x toolbox
    ```

3.  Verify the installation.
    
    ``` text
    ./toolbox --version
    ```

#### Connect to the MCP server

1.  Open [Windsurf](https://docs.codeium.com/windsurf) and navigate to Cascade assistant.
2.  Click the MCP icon, then click **Configure** to open the configuration file.
3.  Add the following configuration, replace the environment variables with your values, and save. The `  FIRESTORE_DATABASE  ` variable is optional and defaults to `  (default)  ` .

<!-- end list -->

``` text
 {
    "mcpServers": {
      "firestore": {
        "command": "./PATH/TO/toolbox",
        "args": ["--prebuilt","firestore","--stdio"],
        "env": {
          "FIRESTORE_PROJECT": "PROJECT_ID",
          "FIRESTORE_DATABASE": "DATABASE_NAME"
        }
      }
    }
  }
```
