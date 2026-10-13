# Installing the ResumeQuick MCP server

ResumeQuick is a hosted remote MCP server. There is nothing to download, build or run.

- Endpoint: `https://mcp.resumequick.app/mcp`
- Transport: streamable HTTP
- Auth: OAuth sign-in in the browser, or a personal API key sent as `Authorization: Bearer <key>`

## Cline

1. Ask the user for a personal API key. They create it at https://resumequick.app/en/profile/extension under API keys; it starts with `rq_live_`.
2. Add this entry to `cline_mcp_settings.json`, with the key in place of `<key>`:

```json
{
  "mcpServers": {
    "resumequick": {
      "type": "streamableHttp",
      "url": "https://mcp.resumequick.app/mcp",
      "headers": { "Authorization": "Bearer <key>" }
    }
  }
}
```

3. Call `get_next_step` to confirm the connection: it returns the one step the user's job search suggests now.

The key gives full access to the user's ResumeQuick account. Keep it in the settings file only, never in a chat or a repository. The user can revoke it on the same settings page.
