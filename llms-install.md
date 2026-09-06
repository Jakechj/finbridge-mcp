# Installing FinBridge (remote MCP server)

FinBridge is a **hosted** MCP server. There is nothing to clone, build or run locally — add one server entry pointing at the public endpoint and authenticate.

- Endpoint: `https://mcp.gronox.kr/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth 2.1 with dynamic client registration (a Google sign-in window opens on first use), **or** an API key sent as a Bearer token. Free plan: 200 calls/day, no card. Keys are issued at https://www.gronox.kr/login after Google sign-in.

## Cline

Add to Cline's MCP settings (`cline_mcp_settings.json`) — OAuth flow:

```json
{
  "mcpServers": {
    "finbridge": {
      "type": "streamableHttp",
      "url": "https://mcp.gronox.kr/mcp"
    }
  }
}
```

Or with an API key instead of OAuth:

```json
{
  "mcpServers": {
    "finbridge": {
      "type": "streamableHttp",
      "url": "https://mcp.gronox.kr/mcp",
      "headers": { "Authorization": "Bearer smcp_..." }
    }
  }
}
```

## Other clients

- Claude.ai / Claude Desktop: Settings → Connectors → Add custom connector → `https://mcp.gronox.kr/mcp`
- Claude Code: `claude mcp add --transport http finbridge https://mcp.gronox.kr/mcp --header "Authorization: Bearer smcp_..."`
- Cursor / Gemini CLI / any Streamable HTTP client: `{"httpUrl": "https://mcp.gronox.kr/mcp", "headers": {"Authorization": "Bearer smcp_..."}}`

## Verify

Ask: "Compare Samsung Electronics with its five nearest peers on P/E and ROE." A working install returns a table with `data_as_of` and a `page_url` per company. Tool reference: https://www.gronox.kr/docs · Prompt library: https://www.gronox.kr/prompts

No environment variables, no dependencies, no local process. Information only, not investment advice.
