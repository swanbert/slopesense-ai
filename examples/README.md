# Client config examples

All clients use the same endpoint: `https://www.slopesense.ca/mcp` (Streamable
HTTP, OAuth 2.1 with PKCE; the client registers itself dynamically).

## Claude Code

```bash
claude mcp add --transport http slopesense https://www.slopesense.ca/mcp
# then inside Claude Code:
/mcp            # pick slopesense → Authenticate → approve in the browser
```

## Gemini CLI (`~/.gemini/settings.json`)

```json
{
  "mcpServers": {
    "slopesense": { "httpUrl": "https://www.slopesense.ca/mcp" }
  }
}
```

Then `/mcp auth slopesense`.

## Generic MCP client (`mcp.json` style)

```json
{
  "mcpServers": {
    "slopesense": {
      "type": "http",
      "url": "https://www.slopesense.ca/mcp"
    }
  }
}
```

## Discovery

- `GET https://www.slopesense.ca/.well-known/oauth-authorization-server`
- `GET https://www.slopesense.ca/.well-known/oauth-protected-resource`
- `POST https://www.slopesense.ca/oauth/register` — dynamic client registration
- `GET https://www.slopesense.ca/oauth/authorize` — consent (browser)
- `POST https://www.slopesense.ca/oauth/token` — code (PKCE) / refresh
