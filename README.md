# FinBridge MCP — Korean + US market data for AI agents

**Remote MCP server** (Streamable HTTP): `https://mcp.gronox.kr/mcp`

FinBridge gives your AI assistant (Claude, ChatGPT, Gemini CLI, Cursor — any MCP client) unified access to Korean and US market data on one normalized schema. It is the only place that serves the Korean market as a first-class citizen: DART filings, corporate-action-adjusted prices, 1,300+ Korean ETFs and named screeners — data that global providers either skip or gate behind $149/mo tiers.

**Licensing-clean by design**: FinBridge serves only data it may redistribute — OpenDART, SEC EDGAR, data.go.kr (Financial Services Commission), FRED public series, and exchange public data via ccxt. No scraped or license-encumbered feeds.

## What you get (33 tools)

| Area | Tools |
|---|---|
| Korean market | DART filings · financials (K-IFRS, normalized) · insider trades · major events · corporate-action-adjusted daily prices (2020–) · 1,354 ETFs · KOSPI/KOSPI200 |
| US market | SEC EDGAR filings · financials (US-GAAP, 18y) · Form 4 insider trades · 13F holdings · shares outstanding (US price feeds are not redistributed — licensing policy) |
| Screeners | Minervini Trend Template (+VCP) · CAN SLIM · RS leaders · technical screens — over every Korean listing, with national RS percentiles |
| Analysis | Technical indicators · valuation snapshots · KR/US financial comparison · portfolio backtests (KR stocks/ETFs) · disclosure news feed |
| Macro & crypto | FRED series (rates, FX) · economic snapshot · crypto quotes/OHLCV via ccxt |

## Quick start

**Free tier, no card**: 100 metered calls/day (basic lookups are unmetered), 130 trading sessions / 4 quarters of depth. Paid plans buy depth, not attempts.

### Claude (claude.ai / Desktop)
Settings → Connectors → Add custom connector → `https://mcp.gronox.kr/mcp` — sign in with Google, no key needed.

### Claude Code
```bash
claude mcp add --transport http finbridge https://mcp.gronox.kr/mcp --header "Authorization: Bearer smcp_..."
```
Get a key at [www.gronox.kr](https://www.gronox.kr) (Google sign-in, issued instantly).

### ChatGPT (developer mode)
Settings → Apps & Connectors → Advanced → Developer mode → Create connector with the URL above and your `smcp_` key as an access token.

### Gemini CLI
```json
{"mcpServers": {"finbridge": {"httpUrl": "https://mcp.gronox.kr/mcp",
  "headers": {"Authorization": "Bearer smcp_..."}}}}
```

## Links

- Product & API keys: https://www.gronox.kr
- Tool reference: https://www.gronox.kr/docs
- Live coverage/status: https://mcp.gronox.kr/status
- Screeners explained: https://www.gronox.kr/screeners
- 한국어: https://www.gronox.kr/ko

## Notes

- Data is a nightly snapshot (filings feed refreshes every 5 minutes); not real-time quotes.
- Output is information, not investment advice. FinBridge is not affiliated with any trader whose published criteria it implements.
- This repository is the public listing for the hosted service; the server itself is not open source.

Contact: 4y.changemaker@gmail.com

## License

The contents of this repository (listing metadata and documentation) are released under the [MIT License](./LICENSE). The hosted FinBridge service and its source code are not part of this repository and are provided under the [FinBridge Terms of Service](https://www.gronox.kr/terms).
