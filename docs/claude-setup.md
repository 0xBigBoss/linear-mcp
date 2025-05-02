# Setting Up Claude with Linear MCP Server

This guide will help you configure Claude to use the Linear MCP server, allowing you to interact with Linear directly through Claude's interface.

## Prerequisites

- Linear MCP server installed and built
- Access to Claude (web interface or API)
- Linear account with API access

## Configuration Steps

### 1. Prepare the Linear MCP Server

You have multiple options to set up the Linear MCP server:

#### Option 1: Local Installation

```bash
# Install dependencies
npm install

# Build the server
npm run build
```

#### Option 2: Docker (Recommended)

Pull and run the official Docker image:

```bash
# Pull the latest image
docker pull ghcr.io/0xbigboss/linear-mcp:latest

# Run with your Linear API key
docker run -e LINEAR_API_KEY=your_api_key ghcr.io/0xbigboss/linear-mcp
```

### 2. Deploy the Linear MCP Server

The Linear MCP server needs to be running and accessible to Claude. You have several options:

#### Option 1: Run Locally with Port Forwarding

1. Start the Linear MCP server:
   ```bash
   # Using npm
   npm start
   
   # Or using Docker
   docker run -e LINEAR_API_KEY=your_api_key ghcr.io/0xbigboss/linear-mcp
   ```

2. Use a secure tunneling service to expose your local server:
   ```bash
   # Using ngrok (install from https://ngrok.com)
   ngrok http 3000
   ```

3. Note the forwarded URL (e.g., `https://a1b2c3d4.ngrok.io`)

#### Option 2: Deploy to a Cloud Provider

Deploy the Linear MCP server to a cloud hosting service like:
- Heroku
- Vercel
- Railway
- Digital Ocean App Platform
- Any container service that supports Docker (AWS ECS, Google Cloud Run, etc.)

Make sure to set up environment variables for your Linear API key in your hosting platform.

### 3. Configure API Access

Ensure your deployment has the necessary authentication:

1. For API Key authentication:
   - Set the `LINEAR_API_KEY` environment variable

2. For OAuth authentication:
   - Configure OAuth credentials and redirect URL
   - Set the required environment variables

### 4. Using with Claude

Once deployed, you can use Claude to interact with Linear by:

1. **Web Interface**: Ask Claude to make requests to your Linear MCP endpoint
   ```
   Can you make a POST request to https://your-mcp-url.com/linear_createIssue with the following JSON body:
   {
     "title": "Update user documentation",
     "description": "The installation guide needs updating for v2.0",
     "teamId": "TEAM_ID"
   }
   ```

2. **Claude API**: Integrate Claude with your application and pass Linear MCP requests programmatically

3. **Claude Code**: Use the WebFetch tool to communicate with your Linear MCP endpoint
   ```
   Can you create a new issue in Linear titled "Improve performance on dashboard page"?
   ```

## Example Commands for Claude

Here are some examples of how to ask Claude to interact with your Linear MCP client:

```
Create a new issue in Linear with the title "Refactor authentication logic" and assign it to the Backend team.
```

```
Search for all high-priority bugs in the current sprint and summarize them.
```

```
Create a new project called "Mobile App Redesign" with the following issues: [list issues].
```

## Security Best Practices

When using Claude with Linear MCP:

1. Use HTTPS for all communications
2. Consider implementing authentication for your MCP endpoint
3. Regularly rotate your Linear API keys
4. Set up appropriate rate limiting
5. Never share your API keys directly with Claude in the conversation

## Troubleshooting

If you encounter issues:

1. Check that your Linear MCP client is running and accessible
2. Verify network connectivity between Claude and your MCP endpoint
3. Examine server logs for detailed error information
4. Ensure your Linear API key has the necessary permissions

## Advanced Configuration

For advanced users, you can enhance the integration by:

1. Adding custom endpoints for specific Linear workflows
2. Implementing middleware for logging or rate limiting
3. Setting up authentication for your MCP endpoint
4. Adding response formatting for better Claude compatibility