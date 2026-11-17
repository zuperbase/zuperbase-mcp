# Connect Cursor, VS Code and other MCP apps

Any app that adds MCP servers over HTTP and supports OAuth sign-in works.

- **Type:** HTTP (streamable)
- **Address:** `https://mcp.zuperbase.co/mcp`
- **Sign-in:** the app discovers it from the address (OAuth 2.1 with dynamic client registration); no key to paste.

Example configuration, for apps that read an `mcp.json`:

```json
{
  "mcpServers": {
    "zuperbase": { "type": "http", "url": "https://mcp.zuperbase.co/mcp" }
  }
}
```

The first time the app calls Zuperbase it opens your browser to sign in and choose the access.
