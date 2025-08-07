# Cloudinary MCP Servers

Model Context Protocol (MCP) is a new, standardized protocol for managing context between large language models (LLMs) and external systems. This repository provides comprehensive MCP servers for Cloudinary's media management platform, enabling you to use natural language to upload, transform, analyze, and organize your media assets directly from AI applications like Cursor and Claude.

With these MCP servers, you can seamlessly manage your entire media workflow through conversational AI - from uploading and transforming images and videos, to configuring automated processing pipelines, analyzing content with AI-powered tools, and organizing assets with structured metadata. Whether you're building media-rich applications, managing large asset libraries, or automating content workflows, these servers provide direct access to Cloudinary's full suite of media optimization and management capabilities.

The following MCP servers are available for Cloudinary:

| Server Name | Description | GitHub Repository | Remote MCP Server |
|-------------|-------------|-------------------|-------------------|
| [**Asset Management**](https://github.com/cloudinary/asset-management-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Upload, manage, and transform your media assets with advanced search and organization capabilities | [@cloudinary/asset-management](https://github.com/cloudinary/asset-management-js) | ✅ `https://asset-management.mcp.cloudinary.com/sse` |
| [**Environment Config**](https://github.com/cloudinary/environment-config-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Configure and manage your Cloudinary environment settings, upload presets, and transformations | [@cloudinary/environment-config](https://github.com/cloudinary/environment-config-js) | ✅ `https://environment-config.mcp.cloudinary.com/sse` |
| [**Structured Metadata**](https://github.com/cloudinary/structured-metadata-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Create, manage, and query structured metadata fields for enhanced asset organization and searchability | [@cloudinary/structured-metadata](https://github.com/cloudinary/structured-metadata-js) | ✅ `https://structured-metadata.mcp.cloudinary.com/sse` |
| [**Analysis**](https://github.com/cloudinary/analysis-js?tab=readme-ov-file#model-context-protocol-mcp-server) | Leverage AI-powered content analysis, moderation, and auto-tagging capabilities for your media assets | [@cloudinary/analysis](https://github.com/cloudinary/analysis-js) | Local only |
| [**MediaFlows**](https://cloudinary.com/documentation/mediaflows_mcp) | Build and manage low-code workflow automations for images and videos with AI-powered assistance | MediaFlows MCP | ✅ `https://mediaflows.mcp.cloudinary.com/v2/mcp` |

## Table of Contents

- [Documentation](#documentation)
- [Installation](#installation)
  - [Remote MCP Servers (Recommended)](#remote-mcp-servers-recommended)
  - [Local MCP Servers](#local-mcp-servers)
- [Configuration Examples](#configuration-examples)
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
    "mediaflows": {
      "url": "https://mediaflows.mcp.cloudinary.com/v2/mcp"
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
      "args": ["-y", "--package", "@cloudinary/asset-management", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    },
    "cloudinary-env-config": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/environment-config", "--", "mcp", "start"],
      "env": {
        "CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
      }
    },
    "cloudinary-smd": {
      "command": "npx",
      "args": ["-y", "--package", "@cloudinary/structured-metadata", "--", "mcp", "start"],
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

#### Option 3: Using command line arguments

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
- Custom metadata fields
- Advanced transformation capabilities

## License

Licensed under the MIT License. See LICENSE file for details.
