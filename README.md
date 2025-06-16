# Cloudinary MCP Servers

Model Context Protocol (MCP) is a new, standardized protocol for managing context between large language models (LLMs) and external systems. This repository provides comprehensive MCP servers for Cloudinary's media management platform, enabling you to use natural language to upload, transform, analyze, and organize your media assets directly from AI applications like Cursor and Claude.

With these MCP servers, you can seamlessly manage your entire media workflow through conversational AI - from uploading and transforming images and videos, to configuring automated processing pipelines, analyzing content with AI-powered tools, and organizing assets with structured metadata. Whether you're building media-rich applications, managing large asset libraries, or automating content workflows, these servers provide direct access to Cloudinary's full suite of media optimization and management capabilities.

The following MCP servers are available for Cloudinary:

| Server Name | Description | Server URL | Install |
|-------------|-------------|------------|---------|
| [**Asset Management**](https://github.com/cloudinary/asset-management-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Upload, manage, and transform your media assets with advanced search and organization capabilities | https://asset-management.mcp.cloudinary.com/sse | [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-asset-mgmt&config=eyJ0eXBlIjoic3NlIiwidXJsIjoiaHR0cHM6Ly9hc3NldC1tYW5hZ2VtZW50Lm1jcC5jbG91ZGluYXJ5LmNvbS9zc2UifQ%3D%3D) |
| [**Environment Config**](https://github.com/cloudinary/environment-config-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Configure and manage your Cloudinary environment settings, upload presets, and transformations | https://environment-config.mcp.cloudinary.com/sse | [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-env-config&config=eyJ0eXBlIjoic3NlIiwidXJsIjoiaHR0cHM6Ly9lbnZpcm9ubWVudC1jb25maWcubWNwLmNsb3VkaW5hcnkuY29tL3NzZSJ9) |
| [**Structured Metadata**](https://github.com/cloudinary/structured-metadata-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Create, manage, and query structured metadata fields for enhanced asset organization and searchability | https://structured-metadata.mcp.cloudinary.com/sse | [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-smd&config=eyJ0eXBlIjoic3NlIiwidXJsIjoiaHR0cHM6Ly9zdHJ1Y3R1cmVkLW1ldGFkYXRhLm1jcC5jbG91ZGluYXJ5LmNvbS9zc2UifQ%3D%3D) |
| **Mediaflows** | Build and manage automated media processing workflows with triggers, conditions, and transformations | https://mediaflows.mcp.cloudinary.com/sse | [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-mediaflows&config=eyJ0eXBlIjoic3NlIiwidXJsIjoiaHR0cHM6Ly9tZWRpYWZsb3dzLm1jcC5jbG91ZGluYXJ5LmNvbS9zc2UifQ%3D%3D) |
| [**Analysis**](https://github.com/cloudinary/analysis-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Leverage AI-powered content analysis, moderation, and auto-tagging capabilities for your media assets | https://analysis.mcp.cloudinary.com/sse | [![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-analysis&config=eyJ0eXBlIjoic3NlIiwidXJsIjoiaHR0cHM6Ly9hbmFseXNpcy5tY3AuY2xvdWRpbmFyeS5jb20vc3NlIn0%3D) |

## Table of Contents

- [Access the MCP servers from any MCP client](#access-the-mcp-servers-from-any-mcp-client)
  - [Remote Servers (Recommended)](#remote-servers-recommended)
  - [Local Servers (Alternative)](#local-servers-alternative)
- [Using Cloudinary's MCP servers with OpenAI Responses API](#using-cloudinarys-mcp-servers-with-openai-responses-api)
- [Authentication](#authentication)
- [Features by Server](#features-by-server)
- [Troubleshooting](#troubleshooting)
- [Paid Features](#paid-features)

## Access the MCP servers from any MCP client

### Remote Servers (Recommended)

If your MCP client has first class support for remote MCP servers, the client will provide a way to accept the server URL directly within its interface.

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "url": "https://asset-management.mcp.cloudinary.com/sse"
    },
    "cloudinary-env-config": {
      "url": "https://environment-config.mcp.cloudinary.com/sse"
    },
    "cloudinary-smd": {
      "url": "https://structured-metadata.mcp.cloudinary.com/sse"
    },
    "cloudinary-mediaflows": {
      "url": "https://mediaflows.mcp.cloudinary.com/sse"
    },
    "cloudinary-analysis": {
      "url": "https://analysis.mcp.cloudinary.com/sse"
    }
  }
}
```

**Note**: Remote servers use OAuth authentication, so no additional credentials are required.

### Local Servers (Alternative)

#### Quick Install with Cursor Deeplinks

For Cursor users, you can install local MCP servers with one click using [Cursor deeplinks](https://docs.cursor.com/deeplinks):

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-asset-mgmt&config=eyJjb21tYW5kIjoibnB4IC15IC0tcGFja2FnZSBAY2xvdWRpbmFyeS9hc3NldC1tYW5hZ2VtZW50IC0tIG1jcCBzdGFydCIsImVudiI6eyJDTE9VRElOQVJZX0NMT1VEX05BTUUiOiJjbG91ZF9uYW1lIiwiQ0xPVURJTkFSWV9BUElfS0VZIjoiYXBpX2tleSIsIkNMT1VESU5BUllfQVBJX1NFQ1JFVCI6ImFwaV9zZWNyZXQifX0%3D) **Asset Management**

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-env-config&config=eyJjb21tYW5kIjoibnB4IC15IC0tcGFja2FnZSBAY2xvdWRpbmFyeS9lbnZpcm9ubWVudC1jb25maWcgLS0gbWNwIHN0YXJ0IiwiZW52Ijp7IkNMT1VESU5BUllfQ0xPVURfTkFNRSI6ImNsb3VkX25hbWUiLCJDTE9VRElOQVJZX0FQSV9LRVkiOiJhcGlfa2V5IiwiQ0xPVURJTkFSWV9BUElfU0VDUkVUIjoiYXBpX3NlY3JldCJ9fQ%3D%3D) **Environment Config**

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-smd&config=eyJjb21tYW5kIjoibnB4IC15IC0tcGFja2FnZSBAY2xvdWRpbmFyeS9zdHJ1Y3R1cmVkLW1ldGFkYXRhIC0tIG1jcCBzdGFydCIsImVudiI6eyJDTE9VRElOQVJZX0NMT1VEX05BTUUiOiJjbG91ZF9uYW1lIiwiQ0xPVURJTkFSWV9BUElfS0VZIjoiYXBpX2tleSIsIkNMT1VESU5BUllfQVBJX1NFQ1JFVCI6ImFwaV9zZWNyZXQifX0%3D) **Structured Metadata**

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=cloudinary-analysis&config=eyJjb21tYW5kIjoibnB4IC15IC0tcGFja2FnZSBAY2xvdWRpbmFyeS9hbmFseXNpcyAtLSBtY3Agc3RhcnQiLCJlbnYiOnsiQ0xPVURJTkFSWV9DTE9VRF9OQU1FIjoiY2xvdWRfbmFtZSIsIkNMT1VESU5BUllfQVBJX0tFWSI6ImFwaV9rZXkiLCJDTE9VRElOQVJZX0FQSV9TRUNSRVQiOiJhcGlfc2VjcmV0In19) **Analysis**

**Note**: For local servers, you'll need to update the environment variables (`CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`) with your actual credentials after installation.

#### Manual Configuration

You can also run the MCP servers locally using the individual npm packages. There are several ways to configure authentication:

#### Option 1: Using individual environment variables

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/asset-management", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_CLOUD_NAME": "cloud_name",
        "CLOUDINARY_API_KEY": "api_key",
        "CLOUDINARY_API_SECRET": "api_secret"
      }
    }
  }
}
```

#### Option 2: Using command line arguments

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": [
        "-y", "--package", "@cloudinary/asset-management",
        "--",
        "mcp", "start",
        "--cloud-name", "cloud_name",
        "--api-key", "api_key",
        "--api-secret", "api_secret"
      ]
    }
  }
}
```

#### Option 3: Using CLOUDINARY_URL environment variable

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/asset-management", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    }
  }
}
```

Apply the same configuration pattern to all other servers by replacing `@cloudinary/asset-management` with the respective package names:
- `@cloudinary/environment-config`
- `@cloudinary/structured-metadata`
- `@cloudinary/analysis`

## Using Cloudinary's MCP servers with OpenAI Responses API

OpenAI's [Responses API](https://platform.openai.com/docs/guides/responses) allows you to integrate MCP servers directly into your OpenAI API calls, enabling AI models to access Cloudinary's media management capabilities in real-time.

### Setup Overview

1. **Choose your server type**: Remote (recommended) or Local
2. **Configure authentication**: OAuth for remote, credentials for local
3. **Add server to your OpenAI API request**: Include MCP server configuration in your API call
4. **Use Cloudinary tools**: The AI model can now call Cloudinary functions during the conversation

### Remote Server Configuration (Recommended)

For remote servers, use OAuth authentication with no additional credentials required:

```javascript
const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      role: "user", 
      content: "Upload this image and optimize it for web delivery"
    }
  ],
  tools: [
    {
      type: "mcp_server",
      mcp_server: {
        name: "cloudinary-asset-mgmt",
        url: "https://asset-management.mcp.cloudinary.com/sse"
      }
    }
  ]
});
```

### Local Server Configuration

For local servers, provide your Cloudinary credentials:

```javascript
const response = await openai.chat.completions.create({
  model: "gpt-4o", 
  messages: [
    {
      role: "user",
      content: "Analyze the content of my uploaded images"
    }
  ],
  tools: [
    {
      type: "mcp_server",
      mcp_server: {
        name: "cloudinary-analysis",
        command: "npx",
        args: ["-y", "--package", "@cloudinary/analysis", "--", "mcp", "start"],
        env: {
          "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
        }
      }
    }
  ]
});
```

### Multiple Server Configuration

You can use multiple Cloudinary MCP servers in a single API call:

```javascript
const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      role: "user",
      content: "Upload these images, analyze their content, and create structured metadata"
    }
  ],
  tools: [
    {
      type: "mcp_server",
      mcp_server: {
        name: "cloudinary-asset-mgmt",
        url: "https://asset-management.mcp.cloudinary.com/sse"
      }
    },
    {
      type: "mcp_server", 
      mcp_server: {
        name: "cloudinary-analysis",
        url: "https://analysis.mcp.cloudinary.com/sse"
      }
    },
    {
      type: "mcp_server",
      mcp_server: {
        name: "cloudinary-smd", 
        url: "https://structured-metadata.mcp.cloudinary.com/sse"
      }
    }
  ]
});
```

### Authentication Summary

- **Remote servers**: Use OAuth authentication (no credentials required)
- **Local servers**: Provide your Cloudinary URL in the format `cloudinary://api_key:api_secret@cloud_name`

### Available Server URLs

| Server | Remote URL | Package Name |
|--------|------------|--------------|
| Asset Management | `https://asset-management.mcp.cloudinary.com/sse` | `@cloudinary/asset-management` |
| Environment Config | `https://environment-config.mcp.cloudinary.com/sse` | `@cloudinary/environment-config` |
| Structured Metadata | `https://structured-metadata.mcp.cloudinary.com/sse` | `@cloudinary/structured-metadata` |
| Mediaflows | `https://mediaflows.mcp.cloudinary.com/sse` | N/A (remote only) |
| Analysis | `https://analysis.mcp.cloudinary.com/sse` | `@cloudinary/analysis` |

## Authentication

### Remote Servers
Remote Cloudinary MCP servers use OAuth authentication, so no additional credentials are required. Simply connect through your MCP client.

### Local Servers
When running MCP servers locally, authentication can be configured in several ways:

1. **Individual environment variables**:
   ```bash
   export CLOUDINARY_CLOUD_NAME="cloud_name"
   export CLOUDINARY_API_KEY="api_key" 
   export CLOUDINARY_API_SECRET="api_secret"
   ```

2. **Command line arguments**: Pass credentials directly as arguments (see configuration examples above)

3. **CLOUDINARY_URL environment variable**:
   ```bash
   export CLOUDINARY_URL="cloudinary://api_key:api_secret@cloud_name"
   ```

You can find your Cloudinary credentials in your [Cloudinary Console Dashboard](https://console.cloudinary.com/) under Settings > Security.

## Features by Server

### Asset Management Server
- Upload and manage images, videos, and raw files
- Advanced search and filtering capabilities
- Bulk operations on assets
- Asset transformation and optimization
- Folder and tag management

### Environment Config Server
- Manage upload presets and transformation settings
- Configure webhooks and notifications
- Set up auto-moderation and tagging rules
- Manage user access and permissions

### Structured Metadata Server
- Define custom metadata fields for assets
- Create searchable metadata schemas
- Bulk metadata operations
- Advanced querying capabilities

### Analysis Server
- AI-powered content analysis and tagging
- Content moderation and safety checks
- Object detection and recognition
- Color analysis and dominant color extraction
- Quality assessment and optimization suggestions

## Need access to more Cloudinary tools?

We're continuing to add more functionality to this remote MCP server repository. If you'd like to leave feedback, file a bug or provide a feature request, please open an issue on this repository.

## Troubleshooting

**"Claude's response was interrupted..."**

If you see this message, Claude likely hit its context-length limit and stopped mid-reply. This happens most often on servers that trigger many chained tool calls such as the asset management server with large asset listings.

To reduce the chance of running into this issue:

* Try to be specific, keep your queries concise.
* If a single request calls multiple tools, try to break it into several smaller tool calls to keep the responses short.
* Use filtering parameters to limit the scope of asset searches and listings.

**Authentication Issues**

Ensure your Cloudinary credentials are correctly configured and have the necessary permissions for the operations you're trying to perform.

## Paid Features

Some features may require a paid Cloudinary plan. Ensure your Cloudinary account has the necessary subscription level for the features you intend to use, such as:

- Advanced AI analysis features
- High-volume API usage
- Custom metadata fields
- Advanced transformation capabilities

## License

Licensed under the MIT License. See LICENSE file for details.

## Quick Start

**For Cursor users**: Click any install button in the table above
**For other MCP clients**: Use the remote server URLs (no setup required)
**For OpenAI API**: See the [OpenAI Integration section](#using-cloudinarys-mcp-servers-with-openai-responses-api)
