# Installing the Code4 MCP server

Code4 is a hosted remote MCP server. There is nothing to download, build or run locally.

- Server URL: `https://mcp.code4.space/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth 2.1 with the user's Code4 account. The client registers itself automatically (Dynamic Client Registration) and signs in with authorization code and PKCE. No API key or token is needed in the configuration.
- Recommended server name: `c4`

## Cline

Add this entry to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "c4": {
      "type": "streamableHttp",
      "url": "https://mcp.code4.space/mcp"
    }
  }
}
```

The `type` must be exactly `streamableHttp`. Without it, Cline falls back to SSE and the server answers 405.

After saving, Cline shows the server as needing authentication. Start the sign-in, and the user signs in to Code4 in the browser and approves access.

## Other clients

Most clients that support remote MCP servers with OAuth accept:

```json
{
  "mcpServers": {
    "c4": {
      "type": "http",
      "url": "https://mcp.code4.space/mcp"
    }
  }
}
```

## Requirements

- The user needs a Code4 account and membership in at least one organization: https://code4.space/signup
- A personal access token in an `Authorization` header does not work with this server. Only OAuth sign-in is accepted.

Support: support@code4.space
