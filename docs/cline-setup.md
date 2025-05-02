# Setting Up Cline with Linear MCP Server

This guide will help you configure Cline to use the Linear MCP server, allowing your AI assistant to interact with Linear directly through the VS Code extension.

## Prerequisites

- Linear MCP server installed and built
- VS Code with Cline extension installed
- Linear account with API access

## Configuration Steps

### 1. Set Up the Linear MCP Server

You have two options to set up the Linear MCP server:

#### Option 1: Local Installation

```bash
# Install dependencies
npm install

# Build the server
npm run build
```

This will create the executable in the `/build` directory.

#### Option 2: Docker (Recommended)

Pull the official Docker image:

```bash
docker pull ghcr.io/0xbigboss/linear-mcp:latest
```

For Docker-based setup, you'll need to configure Cline to use the Docker container instead of a local executable in the next step.

### 2. Add the Linear MCP to Cline's Configuration

1. Open your Cline MCP settings file:
   - macOS: `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`
   - Windows: `%APPDATA%/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`
   - Linux: `~/.config/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`

2. Add the Linear MCP server configuration to the `mcpServers` section:

#### For Local Installation

```json
{
  "mcpServers": {
    "linear": {
      "command": "node",
      "args": ["/absolute/path/to/linear-mcp/build/index.js"],
      "env": {
        "LINEAR_API_KEY": "your_linear_api_key"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

#### For Docker Installation

```json
{
  "mcpServers": {
    "linear": {
      "command": "docker",
      "args": ["run", "--rm", "-e", "LINEAR_API_KEY=your_linear_api_key", "ghcr.io/0xbigboss/linear-mcp"],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Make sure to replace:
- `/absolute/path/to/linear-mcp/build/index.js` with the absolute path to your built Linear MCP server
- `your_linear_api_key` with your actual Linear API key

### 3. Configure Permissions

In the Cline extension settings, you can configure which MCP operations require explicit approval:

1. Open VS Code Settings (Ctrl+,)
2. Search for "Cline MCP"
3. Click "Edit in settings.json" to customize auto-approve settings

You can add specific Linear MCP operations to the `autoApprove` array to allow them without prompting:

```json
"autoApprove": [
  "linear_searchIssues",
  "linear_getTeams"
]
```

### 4. Restart Cline

After saving your configuration:

1. Press `F1` to open the command palette
2. Search for and select "Cline: Restart Server"

## Using Linear with Cline

Once configured, you can interact with Linear through your AI assistant in Cline. Here are some example prompts:

```
Create a new Linear issue titled "Update user profile page" with high priority in the Web team.
```

```
Find all issues assigned to me with the bug label.
```

```
Create a new project named "Q3 Documentation Overhaul" and add issues for each section that needs updating.
```

## Tool Capabilities

The Linear MCP server provides tools that enable your AI assistant to:

- **Issues**: Create, update, search, and delete issues
- **Projects**: Create projects and associate issues
- **Teams**: Get team information, states, and workflows
- **Authentication**: Securely authenticate with Linear

## Security Considerations

Keep in mind that:

- Your Linear API key grants access to your Linear workspace
- All actions performed by the assistant will use your credentials
- You can review and approve/deny each operation before it executes
- Never share your API key in chat conversations

## Troubleshooting

If you encounter issues with the Linear integration:

1. Check the Cline output panel in VS Code for error messages
2. Verify your API key is valid and properly configured
3. Ensure paths in your configuration are absolute and correct
4. Try restarting VS Code completely

For more help, check the Cline extension documentation or report issues on the Linear MCP GitHub repository.