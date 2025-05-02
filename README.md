# Linear MCP Server

A Model Context Protocol (MCP) server for interacting with Linear's API. This server provides a set of tools for managing Linear issues, projects, and teams through AI assistants.

## Overview

The Linear MCP Server enables AI assistants to perform operations in Linear without needing direct API access. It serves as a bridge between AI tools and Linear's API, handling authentication, request formatting, and response parsing.

## Features

- **Authentication**: Secure API key and OAuth-based authentication
- **Issue Management**: Create, update, delete, and search issues
- **Project Management**: Create projects and associate issues
- **Team Management**: Access team information, states, and workflows
- **Batch Operations**: Support for bulk issue creation and deletion

## Setup Guide

### Prerequisites

- Node.js 18 or later
- npm 7 or later
- A Linear account with API access

### Installation

#### Option 1: Local Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

#### Option 2: Docker (Recommended)

1. Pull the latest image:
   ```bash
   docker pull ghcr.io/0xbigboss/linear-mcp:latest
   ```

2. Run with your Linear API key:
   ```bash
   docker run -e LINEAR_API_KEY=your_api_key ghcr.io/0xbigboss/linear-mcp
   ```

For OAuth authentication, mount a volume with your environment variables:
```bash
docker run -v /path/to/.env:/app/.env ghcr.io/0xbigboss/linear-mcp
```

### Authentication Configuration

The client supports two authentication methods:

#### API Key (Recommended)

1. Go to Linear Settings
2. Navigate to the "Security & access" section
3. Find the "Personal API keys" section
4. Click "New API key"
5. Give the key a descriptive label (e.g. "MCP Server")
6. Copy the generated token immediately
7. Add the token to your `.env` file:
   ```
   LINEAR_API_KEY=your_api_key
   ```

#### OAuth Flow (Alternative) ***NOT IMPLEMENTED***

1. Create an OAuth application at https://linear.app/settings/api/applications
2. Configure OAuth environment variables in `.env`:
   ```
   LINEAR_CLIENT_ID=your_oauth_client_id
   LINEAR_CLIENT_SECRET=your_oauth_client_secret
   LINEAR_REDIRECT_URI=http://localhost:3000/callback
   ```

### Building and Running

#### Using npm

1. Build the client:
   ```bash
   npm run build
   ```
2. Start the client:
   ```bash
   npm start
   ```

#### Using Docker

Build the image locally:
```bash
docker build -t linear-mcp .
```

Run the container:
```bash
docker run -e LINEAR_API_KEY=your_api_key linear-mcp
```

## Diagnostics and Troubleshooting

### Verifying Installation

The MCP server should start without errors. Check console output for any startup issues.

### Testing Authentication

```bash
# Test API key authentication
npm run test:integration

# Test OAuth flow
npm run test:oauth
```

### Common Issues

- **Authentication failures**: Verify your API key or OAuth credentials
- **Connection errors**: Check network connectivity to Linear's API
- **Permission errors**: Ensure your Linear account has appropriate permissions

## Development

```bash
# Run in development mode with auto-reload
npm run dev

# Run tests
npm test

# Run integration tests
npm run test:integration

# Run with test tokens
npm run get-test-tokens
```

## Integration with AI Assistants

This MCP server is designed to be integrated with AI assistants. See documentation for specific assistant setup:

- [Cline Setup](./docs/cline-setup.md)
- [Claude Setup](./docs/claude-setup.md)

## Docker Image

The official Docker image is available on GitHub Container Registry:

```bash
docker pull ghcr.io/0xbigboss/linear-mcp:latest
```

This container image is automatically built and published via GitHub Actions. See the [Dockerfile](./Dockerfile) for details on the image configuration.
