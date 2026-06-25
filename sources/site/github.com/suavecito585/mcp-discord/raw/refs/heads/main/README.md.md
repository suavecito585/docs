# Source: https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/README.md

\# MCP-Discord
\[!\[smithery badge\](https://smithery.ai/badge/@barryyip0625/mcp-discord)\](https://smithery.ai/server/@barryyip0625/mcp-discord) !\[\](https://badge.mcpx.dev?type=server 'MCP Server') \[!\[Docker Hub\](https://img.shields.io/docker/v/barryy625/mcp-discord?logo=docker&label=Docker%20Hub)\](https://hub.docker.com/r/barryy625/mcp-discord)

A Discord MCP (Model Context Protocol) server that enables AI assistants to interact with the Discord platform.

<a href="https://glama.ai/mcp/servers/@barryyip0625/mcp-discord">
 <img width="380" height="200" src="https://glama.ai/mcp/servers/@barryyip0625/mcp-discord/badge" alt="MCP-Discord MCP server" />
</a>

## Overview

MCP-Discord provides the following Discord-related functionalities:

- Login to Discord bot
- List servers the bot is a member of
- Get server information
- List members and inspect member details
- List, create, edit, delete, assign, and remove roles
- Search messages in a server
- Read, edit, and delete channel messages
- Send messages to specified channels
- Retrieve forum channel lists
- Create, update, delete, and reply to forum posts
- List forum threads and manage forum tags
- Create, edit, and delete text, forum, voice channels, and categories
- Set and remove channel permission overrides
- Add/remove message reactions
- Create/edit/delete/use webhooks

## Table of Contents

- \[Prerequisites\](#prerequisites)
- \[Installation\](#installation)
- \[Configuration\](#configuration)
- \[Tools Documentation\](#tools-documentation)
 - \[Basic Functions\](#basic-functions)
 - \[Channel Management\](#channel-management)
 - \[Forum Functions\](#forum-functions)
 - \[Messages and Reactions\](#messages-and-reactions)
 - \[Webhook Management\](#webhook-management)
 - \[Role Management\](#role-management)
 - \[Member Management\](#member-management)
- \[Development\](#development)
- \[License\](#license)

## Prerequisites

- Node.js (v18.0.0 or higher)
- npm (v7.0.0 or higher)
- A Discord bot with appropriate permissions
 - Bot token (obtainable from the \[Discord Developer Portal\](https://discord.com/developers/applications))
 - Message Content Intent enabled
 - Server Members Intent enabled
 - Presence Intent enabled
- Permissions required in your Discord server:

 #### Easiest Setup
 - Administrator (Recommended for quick setup and full functionality)

 #### Or, select only the required permissions:
 - Send Messages
 - Create Public Threads
 - Send Messages in Threads
 - Manage Messages
 - Manage Threads
 - Manage Channels
 - Manage Webhooks
 - Manage Roles
 - Add Reactions
 - View Channel

- Add your Discord bot to your server
 - To add your Discord bot to your server, use one of the following invite links (replace \`INSERT\_CLIENT\_ID\_HERE\` with your bot's client ID):
 - \*\*Administrator (full access):\*\*
 https://discord.com/oauth2/authorize?client\_id=INSERT\_CLIENT\_ID\_HERE&scope=bot&permissions=8
 - \*\*Custom permissions (minimum required):\*\*
 https://discord.com/oauth2/authorize?client\_id=INSERT\_CLIENT\_ID\_HERE&scope=bot&permissions=52076489808

> \*\*Note:\*\* 
> According to Discord's security model, a bot can only access information from servers it has been explicitly added to. 
> If you want to use this MCP server to access a specific Discord server, you must add the bot to that server first. 
> Use the invite link below to add the bot to your target server.

## Installation

### Installing via NPM

You can use it with the following command:
\`\`\`bash
npx mcp-discord --config ${DISCORD\_TOKEN}
\`\`\`

For more details, you can check out the \[NPM Package\](https://www.npmjs.com/package/mcp-discord).

### Installing via Smithery

To install mcp-discord automatically via \[Smithery\](https://smithery.ai/server/@barryyip0625/mcp-discord)

### Installing via Docker

You can run mcp-discord using Docker. The Docker images are automatically built and published to Docker Hub.

\*\*Docker Hub Repository\*\*: \[barryy625/mcp-discord\](https://hub.docker.com/r/barryy625/mcp-discord)

Docker uses the streamable HTTP server by default via \`build/app.js\`.

\`\`\`bash
# Pull the latest image
docker pull barryy625/mcp-discord:latest

# Run HTTP server on port 8080
docker run -e DISCORD\_TOKEN=your\_discord\_bot\_token -p 8080:8080 barryy625/mcp-discord:latest

# Override the listening port if needed
docker run -e DISCORD\_TOKEN=your\_discord\_bot\_token -p 3000:3000 barryy625/mcp-discord:latest --transport http --port 3000
\`\`\`

\*\*Available Tags:\*\*
- \`latest\` - Latest stable version from main branch
- \`v1.3.8\`, etc. - Specific version releases

### Manual Installation
\`\`\`bash
# Clone the repository
git clone https://github.com/barryyip0625/mcp-discord.git
cd mcp-discord

# Install dependencies
npm install

# Compile TypeScript
npm run build
\`\`\`

## Configuration

A Discord bot token is required for proper operation. The server supports two transport methods: stdio and streamable HTTP.

### Transport Methods

1. \*\*stdio\*\* (Default)
 - Traditional stdio transport for basic usage
 - Suitable for simple integrations

2. \*\*streamable HTTP\*\*
 - HTTP-based transport for more advanced scenarios
 - Supports stateless operation
 - Configurable port number

### Configuration Options

You can provide configuration in two ways:

1. Environment variables:
\`\`\`bash
DISCORD\_TOKEN=your\_discord\_bot\_token
\`\`\`

2. Using command line arguments:
\`\`\`bash
# For stdio transport (default)
node build/index.js --config "your\_discord\_bot\_token"

# For streamable HTTP transport
node build/app.js --transport http --port 3000 --config "your\_discord\_bot\_token"
\`\`\`

## Usage with Claude/Cursor

### 1. Use Stdio Transport with Claude/Cursor

Use \`build/index.js\` when your MCP client expects a command-based stdio server.

#### Claude Desktop / Claude Code

\`\`\`json
{
    "mcpServers": {
        "discord": {
            "command": "node",
            "args": \[
                "path/to/mcp-discord/build/index.js"
            \],
            "env": {
                "DISCORD\_TOKEN": "your\_discord\_bot\_token"
            }
        }
    }
}
\`\`\`

#### Cursor

\`\`\`json
{
    "mcpServers": {
        "discord": {
            "command": "node",
            "args": \[
                "path/to/mcp-discord/build/index.js"
            \],
            "env": {
                "DISCORD\_TOKEN": "your\_discord\_bot\_token"
            }
        }
    }
}
\`\`\`

This is the recommended setup for local command-based MCP clients.

### 2. Self-Host the Streamable HTTP Server

Use \`build/app.js\` when you want to run mcp-discord as an HTTP MCP server.

#### Run with Node.js

\`\`\`bash
DISCORD\_TOKEN=your\_discord\_bot\_token node build/app.js --transport http --port 3000
\`\`\`

On Windows PowerShell:

\`\`\`powershell
$env:DISCORD\_TOKEN="your\_discord\_bot\_token"
node build/app.js --transport http --port 3000
\`\`\`

#### Run with Docker

\`\`\`bash
docker run -e DISCORD\_TOKEN=your\_discord\_bot\_token -p 3000:3000 barryy625/mcp-discord:latest --transport http --port 3000
\`\`\`

Once started, the MCP HTTP endpoint is:

\`\`\`text
http://localhost:3000/mcp
\`\`\`

### 3. Connect to a Hosted HTTP MCP Server

If you already host mcp-discord elsewhere, point your MCP client at the server's \`/mcp\` endpoint instead of launching \`build/app.js\` as a command.

Example endpoint:

\`\`\`text
https://your-server.example.com/mcp
\`\`\`

Important notes:

- \`build/app.js\` starts an HTTP server. It does not speak stdio.
- \`build/index.js\` is the correct entrypoint for command-based stdio MCP clients.
- For hosted HTTP usage, configure your MCP client to connect to the HTTP endpoint URL provided by your deployment.
- The exact HTTP-client configuration format depends on the MCP client you use.

## Tools Documentation

### Basic Functions

- \`discord\_login\`: Login to Discord using the configured token
- \`discord\_list\_servers\`: List all Discord servers the bot is a member of
- \`discord\_send\`: Send a message to a specified channel
- \`discord\_get\_server\_info\`: Get Discord server information

### Channel Management

- \`discord\_create\_text\_channel\`: Create a text channel
- \`discord\_create\_forum\_channel\`: Create a forum channel
- \`discord\_create\_voice\_channel\`: Create a voice channel
- \`discord\_edit\_channel\`: Edit a channel name, topic, parent category, or position
- \`discord\_delete\_channel\`: Delete a channel
- \`discord\_create\_category\`: Create a channel category
- \`discord\_edit\_category\`: Edit a channel category
- \`discord\_delete\_category\`: Delete a channel category
- \`discord\_set\_channel\_permissions\`: Set permission overrides for a role or user on a channel/category
- \`discord\_remove\_channel\_permissions\`: Remove permission overrides from a channel/category

### Forum Functions

- \`discord\_get\_forum\_channels\`: Get a list of forum channels
- \`discord\_create\_forum\_post\`: Create a forum post
- \`discord\_get\_forum\_post\`: Get a forum post
- \`discord\_list\_forum\_threads\`: List active and archived threads in a forum channel
- \`discord\_reply\_to\_forum\`: Reply to a forum post
- \`discord\_get\_forum\_tags\`: Get all available tags for a forum channel
- \`discord\_set\_forum\_tags\`: Replace the available tags for a forum channel
- \`discord\_update\_forum\_post\`: Update a forum post's title, tags, archived state, or locked state
- \`discord\_delete\_forum\_post\`: Delete a forum post

### Messages and Reactions

- \`discord\_search\_messages\`: Search messages in a server
- \`discord\_read\_messages\`: Read channel messages (supports \`before\`, \`after\`, \`around\` params — accepts snowflake IDs or ISO 8601 dates like \`"2025-03-01T00:00:00Z"\`)
- \`discord\_edit\_message\`: Edit a bot-authored message
- \`discord\_add\_reaction\`: Add a reaction to a message
- \`discord\_add\_multiple\_reactions\`: Add multiple reactions to a message
- \`discord\_remove\_reaction\`: Remove a reaction from a message
- \`discord\_delete\_message\`: Delete a specific message from a channel

### Webhook Management

- \`discord\_create\_webhook\`: Creates a new webhook for a Discord channel
- \`discord\_send\_webhook\_message\`: Sends a message to a Discord channel using a webhook
- \`discord\_edit\_webhook\`: Edits an existing webhook for a Discord channel
- \`discord\_delete\_webhook\`: Deletes an existing webhook for a Discord channel

### Role Management

- \`discord\_list\_roles\`: List all roles in a server
- \`discord\_create\_role\`: Create a role with color, hoist, mentionable, and permission options
- \`discord\_edit\_role\`: Edit an existing role
- \`discord\_delete\_role\`: Delete a role
- \`discord\_assign\_role\`: Assign a role to a member
- \`discord\_remove\_role\`: Remove a role from a member

### Member Management

- \`discord\_list\_members\`: List members in a server with roles
- \`discord\_get\_member\`: Get detailed information about a specific member

## Development

\`\`\`bash
# Development mode
npm run dev
\`\`\`

## License

\[MIT License\](https://github.com/barryyip0625/mcp-discord?tab=MIT-1-ov-file)