# Cloudinary MCP Servers

Model Context Protocol (MCP) is a new, standardized protocol for managing context between large language models (LLMs) and external systems. This repository provides comprehensive MCP servers for Cloudinary's media management platform, enabling you to use natural language to upload, transform, analyze, and organize your media assets directly from AI applications like Cursor and Claude.

With these MCP servers, you can seamlessly manage your entire media workflow through conversational AI - from uploading and transforming images and videos, to configuring automated processing pipelines, analyzing content with AI-powered tools, and organizing assets with structured metadata. Whether you're building media-rich applications, managing large asset libraries, or automating content workflows, these servers provide direct access to Cloudinary's full suite of media optimization and management capabilities.

The following MCP servers are available for Cloudinary:

| Server Name | Description | Remote MCP Server |
|-------------|-------------|-------------------|
| [**Asset Management**](https://github.com/cloudinary/asset-management-mcp) | Upload, manage, and transform your media assets with advanced search and organization capabilities | [asset-management](https://asset-management.mcp.cloudinary.com/sse) |
| [**Environment Config**](https://github.com/cloudinary/environment-config-mcp) | Configure and manage your Cloudinary environment settings, upload presets, and transformations | [environment-config](https://environment-config.mcp.cloudinary.com/sse) |
| [**Structured Metadata**](https://github.com/cloudinary/structured-metadata-mcp) | Create, manage, and query structured metadata fields for enhanced asset organization and searchability | [structured-metadata](https://structured-metadata.mcp.cloudinary.com/sse) |
| [**Analysis**](https://github.com/cloudinary/analysis-js) | Leverage AI-powered content analysis, moderation, and auto-tagging capabilities for your media assets | [analysis](https://analysis.mcp.cloudinary.com/sse) |
| [**MediaFlows**](https://cloudinary.com/documentation/mediaflows_mcp) | Build and manage low-code workflow automations for images and videos with AI-powered assistance | [mediaflows](https://mediaflows.mcp.cloudinary.com/v2/mcp) |

## Table of Contents

- [Documentation](#documentation)
- [Installation](#installation)
  - [Remote MCP Servers (Recommended)](#remote-mcp-servers-recommended)
  - [Local MCP Servers](#local-mcp-servers)
  - [Docker Images](#docker-images)
- [Configuration Examples](#configuration-examples)
  - [Advanced Local Server Configuration](#advanced-local-server-configuration)
- [Authentication](#authentication)
- [Features by Server](#features-by-server)
- [Need access to more Cloudinary tools?](#need-access-to-more-cloudinary-tools)
- [Troubleshooting](#troubleshooting)
- [Paid Features](#paid-features)
- [License](#license)

## Documentation

For detailed guides, tutorials, and comprehensive documentation on using Cloudinary's MCP servers:

- **[Cloudinary MCP and LLM Tool Documentation](https://cloudinary.com/documentation/cloudinary_llm_mcp)** - Complete guide to integrating Cloudinary with AI/LLM applications
- **[MediaFlows MCP Documentation](https://cloudinary.com/documentation/mediaflows_mcp)** - Setup instructions and guidelines for using the MediaFlows (MCP) server

## Installation

### Remote MCP Servers (Recommended)

Remote MCP servers are hosted by Cloudinary and ready to use immediately. No local installation required.

### Local MCP Servers

Local MCP servers run on your machine using npm packages. Choose this option if you need more control or customization.

**Note**: You'll need to configure your environment variables (`CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`) with your actual credentials after installation.

### Docker Images

Official Docker images for Cloudinary MCP servers are available on Docker Hub, providing a containerized deployment option for running MCP servers locally or in cloud environments.

**Available on Docker Hub:** [Cloudinary MCP Docker Images](https://hub.docker.com/u/cloudinary?page=1&search=MCP)

Docker images offer several benefits:
- **Isolated environments** - Run MCP servers in containers without affecting your system dependencies
- **Easy deployment** - Quick setup with minimal configuration required
- **Consistent runtime** - Ensures the same environment across different machines and platforms
- **Scalability** - Easily deploy multiple instances or integrate into container orchestration systems

To use Docker images, ensure you have Docker installed on your system and pass your Cloudinary credentials as environment variables when running the containers. See the individual Docker image documentation on Docker Hub for specific usage instructions.

## Configuration Examples

### Remote MCP Servers Configuration

Remote servers are hosted by Cloudinary and accessed via URL:

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt-remote": {
      "url": "https://asset-management.mcp.cloudinary.com/sse"
    },
    "cloudinary-env-config-remote": {
      "url": "https://environment-config.mcp.cloudinary.com/sse"
    },
    "cloudinary-smd-remote": {
      "url": "https://structured-metadata.mcp.cloudinary.com/sse"
    },
    "cloudinary-analysis-remote": {
      "url": "https://analysis.mcp.cloudinary.com/sse"
    },
    "mediaflows": {
      "url": "https://mediaflows.mcp.cloudinary.com/v2/mcp"
    }
  }
}
```

### Remote MCP Servers with Authentication

Remote MCP servers hosted by Cloudinary use OAuth2 by default for authentication. You can also authenticate using API keys via headers:

#### Using CLOUDINARY_URL (Simplest)
```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt-remote": {
      "url": "https://asset-management.mcp.cloudinary.com/sse",
      "headers": {
        "cloudinary-url": "cloudinary://api_key:api_secret@cloud_name"
      }
    }
  }
}
```

#### Using Individual Headers
```json
{
  "mcpServers": {
    "cloudinary-env-config-remote": {
      "url": "https://environment-config.mcp.cloudinary.com/sse",
      "headers": {
        "cloudinary-cloud-name": "your_cloud_name",
        "cloudinary-api-key": "your_api_key",
        "cloudinary-api-secret": "your_api_secret"
      }
    }
  }
}
```

#### With Custom Configuration
```json
{
  "mcpServers": {
    "cloudinary-smd-remote": {
      "url": "https://structured-metadata.mcp.cloudinary.com/sse",
      "headers": {
        "cloudinary-url": "cloudinary://api_key:api_secret@cloud_name",
        "cloudinary-region": "api-eu",
        "cloudinary-tools": "list-metadata-fields,get-metadata-field,create-metadata-field"
      }
    }
  }
}
```

### Local MCP Servers Configuration

Local servers run on your machine using npm packages:

#### Option 1: Using CLOUDINARY_URL environment variable (Recommended)

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/asset-management-mcp", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    },
    "cloudinary-env-config": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/environment-config-mcp", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    },
    "cloudinary-smd": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/structured-metadata-mcp", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    },
    "cloudinary-analysis": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/analysis", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    }
  }
}
```

#### Option 2: Using individual environment variables

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/asset-management-mcp", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_CLOUD_NAME": "cloud_name",
        "CLOUDINARY_API_KEY": "api_key",
        "CLOUDINARY_API_SECRET": "api_secret"
      }
    }
  }
}
```
#### Option 3: Using command line arguments

```json
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": [
        "-y", "--package", "@cloudinary/asset-management-mcp",
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

#### MediaFlows MCP Server Configuration

For MediaFlows, use the following configuration:

```json
{
  "mcpServers": {
    "mediaflows": {
      "url": "https://mediaflows.mcp.cloudinary.com/v2/mcp",
      "headers": {
        "cld-cloud-name": "cloud_name",
        "cld-api-key": "api_key",
        "cld-secret": "api_secret"
      }
    }
  }
}
```

### Advanced Local Server Configuration

Each npm package supports additional configuration options beyond the basic setup examples above.

#### Running as SSE Server

To run a local MCP server using Server-Sent Events (SSE) transport instead of stdio:

```bash
npx -y --package @cloudinary/asset-management-mcp -- mcp start --transport sse
```

You can specify a custom port (default is 2718):

```bash
npx -y --package @cloudinary/asset-management-mcp -- mcp start --transport sse --port 3000
```

#### Available Configuration Options

To see all available configuration options for any package:

```bash
npx -y --package @cloudinary/asset-management-mcp -- mcp start --help
```

**Complete list of available flags:**

```
USAGE
  mcp start [--transport stdio|sse] [--port value] [--tool value]...
            [--scope admin|builder|librarian] [--api-key value]
            [--api-secret value] [--oauth2 value] [--cloud-name value]
            [--server-url value] [--server-index value]
            [--region api|api-eu|api-ap] [--api-host value]
            [--log-level debug|warning|info|error] [--env value]...

FLAGS
  --transport       The transport to use for communicating with the server
                    [stdio|sse, default = stdio]
  --port            The port to use when the SSE transport is enabled
                    [default = 2718]
  --tool...         Specify tools to mount on the server (repeatable)
  --scope           Mount tools/resources that match given scope
                    [admin|builder|librarian]
  --api-key         Sets the apiKey auth field for the API
  --api-secret      Sets the apiSecret auth field for the API
  --oauth2          Sets the oauth2 auth field for the API
  --cloud-name      Allows setting the cloudName parameter for all operations
  --server-url      Overrides the default server URL used by the SDK
  --server-index    Selects a predefined server used by the SDK
  --region          Sets the region variable for url substitution
                    [api|api-eu|api-ap]
  --api-host        Sets the host variable for url substitution
  --log-level       The log level to use for the server
                    [debug|warning|info|error, default = info]
  --env...          Environment variables made available to the server
  -h, --help        Print help information and exit
```

#### Debugging

For detailed network payload debugging, use the `CLOUDINARY_DEBUG` environment variable:

```bash
CLOUDINARY_DEBUG=true npx -y --package @cloudinary/asset-management-mcp -- mcp start
```

You can combine debug mode with other options for comprehensive troubleshooting:

```bash
CLOUDINARY_DEBUG=true npx -y --package @cloudinary/asset-management-mcp -- mcp start --transport sse --log-level debug
```

**Note:** These configuration options apply to all local MCP packages:
- `@cloudinary/asset-management-mcp`
- `@cloudinary/environment-config-mcp`
- `@cloudinary/structured-metadata-mcp`
- `@cloudinary/analysis`

## Authentication

When running MCP servers locally, authentication can be configured in several ways:

### Option 1: Individual environment variables (Recommended)
```bash
export CLOUDINARY_CLOUD_NAME="cloud_name"
export CLOUDINARY_API_KEY="api_key"
export CLOUDINARY_API_SECRET="api_secret"
```

### Option 2: CLOUDINARY_URL environment variable
```bash
export CLOUDINARY_URL="cloudinary://api_key:api_secret@cloud_name"
```

### Option 3: Command line arguments
Pass credentials directly as arguments (see configuration examples above)

You can find your Cloudinary credentials in your [Cloudinary Console Dashboard](https://console.cloudinary.com/) under Settings > Security.

## Features by Server

### Asset Management Server
- Upload and manage media assets (images, videos, raw files)
- Search and organize assets with advanced filtering capabilities
- Handle asset operations and transformations
- Manage folders, tags, and asset relationships
- Generate archives and download links

### Environment Config Server
- Configure upload presets and transformation settings
- Manage streaming profiles and webhook notifications
- Set up upload mappings

### Structured Metadata Server
- Create and manage structured metadata fields
- Configure conditional metadata rules and validation
- Organize and search metadata configurations
- Handle metadata field relationships and ordering

### Analysis Server
- AI-powered content analysis including tagging, moderation, and captioning
- Object detection and recognition with multiple AI models
- Image quality analysis and watermark detection
- Content moderation and safety analysis
- Fashion, text, and anatomy detection capabilities

### MediaFlows Server
- Build and manage workflow automations using natural language
- Query existing PowerFlow automations in your environment
- Create conditional logic based on metadata, tags, and asset properties
- Automate asset moderation, approval, and notification workflows
- Debug and understand existing automation configurations

## Need access to more Cloudinary tools?

We're continuing to add more functionality to these MCP servers. If you'd like to leave feedback, file a bug or provide a feature request, please open an issue on this repository.

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
- Advanced transformation capabilities

## License

Licensed under the MIT License. See LICENSE file for details.
