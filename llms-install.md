# Installing the Worthbase MCP server

Worthbase is a hosted remote MCP server. There is nothing to install or run locally and no API
key: the person signs in to their own Worthbase account in the browser the first time a tool is
used. A Worthbase trial or subscription is needed to use the tools.

- Endpoint: `https://worthbase.app/mcp` (Streamable HTTP)
- Auth: OAuth 2.1 with PKCE, client ID metadata documents or dynamic client registration,
  discovered from the 401 the endpoint returns (`/.well-known/oauth-protected-resource/mcp`)

For clients that only run local (stdio) servers, bridge with `mcp-remote`:

```json
{
  "mcpServers": {
    "worthbase": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://worthbase.app/mcp"]
    }
  }
}
```

For clients that support remote servers directly:

```json
{
  "mcpServers": {
    "worthbase": { "url": "https://worthbase.app/mcp" }
  }
}
```

To check it works, ask: "What's my net worth?" The client should open a Worthbase sign-in page,
then answer from the `get_net_worth` tool.
