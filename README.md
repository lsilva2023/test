# Custom Azure DevOps MCP Server 🧩

An MCP (Model Context Protocol) server that connects to Azure DevOps and exposes Work Items and Test Cases from the TaxAct-Engineering project as resources and tools.

## Features ✨

- 🔐 **Personal Access Token Authentication**: Secure authentication using Azure DevOps Personal Access Token (PAT)
- 🛠️ **Test Case tool**: Provides a tool to retrieve test case details by ID
- 🛠️ **Work Item tool**: Provides a tool to retrieve Work Item (US, Enablers, bugs, etc) details by ID
- 🛠️ **Related Test Cases tool**: Provides a tool to retrieve Test Cases associated to a Work Item

## Prerequisites 📋

- 💻 Node.js 18.x or higher
- 🔑 Azure DevOps Personal Access Token with Work Item and Test Management read permissions
- 📦 Azure DevOps Personal Access Token with Package read permissions (only if you want to build the package)
- 🏢 Access to the TaxAct-Engineering project in the Taxwell organization

## Installation 📦
Follow the next steps to install the ado-mcp server:

1. 📥 Get a copy of the package `taxwell-ado-mcp-server-1.0.0.tgz` from `\\mhvfs01\Testing\LuisSilva\QAAutomationTools\tax-ado-mcp`

2. 🌐 Install the package globally
    ```bash
    npm install -g taxwell-ado-mcp-server-1.0.0
    ```
To review the code or create your own package:

1. Get a copy of the source code from `\\mhvfs01\Testing\LuisSilva\QAAutomationTools\tax-ado-mcp\tax-ado-mcp`
2. 📝 Rename npmrc_example to .npmrc
3. 🔗 Folow the steps in <https://dev.azure.com/Taxwell/TaxAct-Engineering/_artifacts/feed/TaxwellNodePackageFeed/connect> to set the values in .npmrc 
4. ⬇️ Install dependencies:
    ```bash
    npm install
    ```
5. 📦 Create the npm package
    ```bash
    npm run package
    ```
    This will generate the package named taxwell-ado-mcp-server-1.0.0.tgz

## Setup the MCP Server ⚙️

### 1. Configure in VSCode 🖥️

Follow the next steps to configure the MCP Server in VSCode:

1. ⌨️ Press `Ctrl + Shift + P` to open the VSCode command prompt

2. 🛠️ Type `MCP: Open User Configuration` and press enter

3. 📋 Add the `azure-devops` entry in  `servers` as the following:
    ```json
    {
      "servers": {
        "azure-devops": {
          "command": "ado-mcp.cmd",
          "args": [],
          "env": {
            "AZURE_DEVOPS_PAT": "",
            "AZURE_DEVOPS_ORG": "Taxwell",
            "AZURE_DEVOPS_PROJECT": "TaxAct-Engineering"
          }
        }
      }
    }
    ```
4. 🔐 Set the `AZURE_DEVOPS_PAT` using your Personal Access Token with `Work Item` and `Test Management` read permissions.
5. 💾 Save the file.
6. ▶️ Click the `Start` link that will appear above `azure-devops` new entry.
7. ✅ Test your configuration. Open a copilot chat and type the following prompt `Get User Story [replace this with your US ID]` (⚠️ Make sure you are using Taxwell Copilot account)
 
### 2. Configure in Visual Studio 🖥️
1. ⚠️ Make sure you have Visual Studio 17.14.9 or higher

2. 📄 Create a file in `%USERPROFILE%` named `.mcp.json`

3. 📝 Open that file using Visual Studio

4. 📋 Paste into that file the following JSON:
    ```json
    {
      "servers": {
        "azure-devops": {
          "command": "ado-mcp.cmd",
          "args": [],
          "env": {
            "AZURE_DEVOPS_PAT": "",
            "AZURE_DEVOPS_ORG": "Taxwell",
            "AZURE_DEVOPS_PROJECT": "TaxAct-Engineering"
          }
        }
      }
    }
    ```
5. 🔐 Set the `AZURE_DEVOPS_PAT` using your Personal Access Token with `Work Item` and `Test Management` read permissions

6. 💾 Save the file.

7. ▶️ Click the `Start` link that will appear above `azure-devops` new entry.

8. 💬 Open a copilot chat (⚠️ Make sure you are using Taxwell Copilot account)

9. 🔄 Select `Agent` mode instead of `Ask` (drop down below the prompt input text)

10. 🔧 Click the `Select tools` icon and check:
    - `get-test-case`
    - `get-test-cases-for-work-item`
    - `get-work-item`
11. ✅ Test your configuration. Type the following prompt `Get User Story [replace this with your US ID]`