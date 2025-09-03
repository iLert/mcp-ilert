# ilert MCP server

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-light.svg)](https://cursor.com/en/install-mcp?name=ilert&config=eyJ0eXBlIjoic3RyZWFtYWJsZUh0dHAiLCJ1cmwiOiJodHRwczovL21jcC5pbGVydC5jb20vbWNwIiwiaGVhZGVycyI6eyJBdXRob3JpemF0aW9uIjoiQmVhcmVyIHtZT1VSLUlMRVJULUFQSS1LRVktSEVSRX0ifX0%3D)

The official [Model Context Protocol](https://modelcontextprotocol.io/introduction) (MCP) server for ilert.

Enables AI assistants to navigate your alerting and incident management resources on [ilert](https://www.ilert.com/).

The ilert MCP server is remote and uses the [Streamable HTTP transport](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports#streamable-http).

## Usage

See the [ilert docs](https://docs.ilert.com/developer-docs/mcp-server/overview) for instructions on how to connect with the most popular AI agents and coding assistants like Claude, Cline, Cursor and Windsurf.

For custom integrations or integrating with other MCP clients, follow the instructions below:

1. Log in to the [ilert app](https://app.ilert.com) and open your organization settings.

2. Click on `Profile` > `API Keys` and create a new api key for your user.

3. Add the following configuration to your AI assistant or MCP client (the configuration schema may differ depending on the implementation):
   ```json
   {
     "mcpServers": {
       "ilert": {
         "type": "streamableHttp",
         "url": "https://mcp.ilert.com/mcp",
         "headers": {
           "Authorization": "Bearer {{YOUR-API-KEY}}"
         }
       }
     }
   }
   ```
   For clients that don't support remote MCP servers or that haven't implemented the [Streamable HTTP transport](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports#streamable-http) yet, you can use a configuration like the following instead:
   ```json
   {
     "mcpServers": {
       "ilert": {
         "command": "npx",
         "args": [
           "-y",
           "mcp-remote",
           "https://mcp.ilert.com/mcp",
           "--header",
           "Authorization: Bearer ${ILERT_AUTH_TOKEN}"
         ],
         "env": {
           "ILERT_AUTH_TOKEN": "{{YOUR-API-KEY}}"
         }
       }
     }
   }
   ```
