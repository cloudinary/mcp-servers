# Cloudinary MCP Servers

Model Context Protocol (MCP) is a new, standardized protocol for managing context between large language models (LLMs) and external systems. This repository provides comprehensive MCP servers for Cloudinary's media management platform, enabling you to use natural language to upload, transform, analyze, and organize your media assets directly from AI applications like Cursor and Claude.

With these MCP servers, you can seamlessly manage your entire media workflow through conversational AI - from uploading and transforming images and videos, to configuring automated processing pipelines, analyzing content with AI-powered tools, and organizing assets with structured metadata. Whether you're building media-rich applications, managing large asset libraries, or automating content workflows, these servers provide direct access to Cloudinary's full suite of media optimization and management capabilities.

The following servers are included in this repository:

| Server Name | Description | Server URL |
|-------------|-------------|------------|
| [**Asset Management**](https://github.com/cloudinary/asset-management-js) | Upload, manage, and transform your media assets with advanced search and organization capabilities | https://asset-management.mcp.cloudinary.com/sse |
| [**Environment Config**](https://github.com/cloudinary/environment-config-js) | Configure and manage your Cloudinary environment settings, upload presets, and transformations | https://environment-config.mcp.cloudinary.com/sse |
| [**Structured Metadata**](https://github.com/cloudinary/structured-metadata-js) | Create, manage, and query structured metadata fields for enhanced asset organization and searchability | https://structured-metadata.mcp.cloudinary.com/sse |
| **Mediaflows** | Build and manage automated media processing workflows with triggers, conditions, and transformations | https://mediaflows.mcp.cloudinary.com/sse |
| [**Analysis**](https://github.com/cloudinary/analysis-js) | Leverage AI-powered content analysis, moderation, and auto-tagging capabilities for your media assets | https://analysis.mcp.cloudinary.com/sse |

## Access the MCP servers from any MCP client

### Remote Servers (Recommended)

If your MCP client has first class support for remote MCP servers, the client will provide a way to accept the server URL directly within its interface (e.g. Cloudinary AI Playground).

If your client does not yet support remote MCP servers, you will need to set up its respective configuration file using mcp-remote (https://www.npmjs.com/package/mcp-remote) to specify which servers your client can access.

```json
{
	"mcpServers": {
		"cloudinary-asset-mgmt": {
			"command": "npx",
			"args": ["mcp-remote", "https://asset-management.mcp.cloudinary.com/sse"]
		},
		"cloudinary-env-config": {
			"command": "npx",
			"args": ["mcp-remote", "https://environment-config.mcp.cloudinary.com/sse"]
		},
		"cloudinary-smd": {
			"command": "npx",
			"args": ["mcp-remote", "https://structured-metadata.mcp.cloudinary.com/sse"]
		},
		"cloudinary-mediaflows": {
			"command": "npx",
			"args": ["mcp-remote", "https://mediaflows.mcp.cloudinary.com/sse"]
		},
		"cloudinary-analysis": {
			"command": "npx",
			"args": ["mcp-remote", "https://analysis.mcp.cloudinary.com/sse"]
		}
	}
}
```

**Note**: Remote servers use OAuth authentication, so no additional credentials are required.

### Local Servers (Alternative)

You can also run the MCP servers locally using the individual npm packages. There are several ways to configure authentication:

#### Option 1: Using CLOUDINARY_URL environment variable

```json
{
	"mcpServers": {
		"cloudinary-asset-management": {
			"command": "npx",
			"args": ["-y", "--package", "@cloudinary/asset-management", "--", "mcp", "start"],
			"env": {
				"CLOUDINARY_URL": "cloudinary://api_key:api_secret@cloud_name"
			}
		}
	}
}
```

#### Option 2: Using command line arguments

```json
{
	"mcpServers": {
		"cloudinary-asset-management": {
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

#### Option 3: Using individual environment variables

```json
{
	"mcpServers": {
		"cloudinary-asset-management": {
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

Apply the same configuration pattern to all other servers by replacing `@cloudinary/asset-management` with the respective package names:
- `@cloudinary/environment-config`
- `@cloudinary/structured-metadata`
- `@cloudinary/analysis`

## Using Cloudinary's MCP servers with OpenAI Responses API

To use one of Cloudinary's MCP servers with OpenAI's responses API:

- **Remote servers**: Use OAuth authentication (no credentials required)
- **Local servers**: Provide your Cloudinary URL in the format `cloudinary://api_key:api_secret@cloud_name`

## Authentication

### Remote Servers
Remote Cloudinary MCP servers use OAuth authentication, so no additional credentials are required. Simply connect through your MCP client.

### Local Servers
When running MCP servers locally, authentication can be configured in several ways:

1. **CLOUDINARY_URL environment variable**:
   ```bash
   export CLOUDINARY_URL="cloudinary://api_key:api_secret@cloud_name"
   ```

2. **Individual environment variables**:
   ```bash
   export CLOUDINARY_CLOUD_NAME="cloud_name"
   export CLOUDINARY_API_KEY="api_key" 
   export CLOUDINARY_API_SECRET="api_secret"
   ```

3. **Command line arguments**: Pass credentials directly as arguments (see configuration examples above)

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
