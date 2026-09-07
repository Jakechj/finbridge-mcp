# FinBridge — DART + SEC + FRED + prices + screeners. One MCP.

**The finance MCP for AI stock analysis.** FinBridge is a hosted data service that collects official financial data for **Korea, the United States, Japan and Taiwan** (plus European statements) every night, normalises it to one schema, and serves it to ChatGPT, Claude, Cursor or any MCP client — and to everything else over a REST API.

- **MCP endpoint (Streamable HTTP):** `https://mcp.gronox.kr/mcp`
- **REST API:** `https://mcp.gronox.kr/api/v1` · OpenAPI 3.1: `https://mcp.gronox.kr/api/v1/openapi.json`
- **Free plan, no card:** 200 calls/day, every tool, the last 4 fiscal years and 130 trading sessions. Paid plans buy history depth, not attempts.

Official sources only, and only sources we may redistribute: OpenDART, SEC EDGAR, EDINET, TWSE/TPEx OpenAPI, data.go.kr (Financial Services Commission), Databento (US daily prices), FRED public series, exchange public data via ccxt. Every answer names its source and as-of date, and every company carries a `page_url` to a public page with the filing behind each number.

## Coverage

| Market | Source | Statements & filings | Daily prices | Segments | Screeners / backtests |
|---|---|---|---|---|---|
| Korea (KRX) | OpenDART · data.go.kr | ✅ K-IFRS, normalised, revisions kept | ✅ corporate-action adjusted, 2020– | ✅ | ✅ |
| United States | SEC EDGAR · Databento | ✅ US-GAAP, as-filed (point-in-time) history | ✅ from 2023-03, split-adjusted | ✅ (SEC DERA) | ✅ |
| Taiwan | TWSE / TPEx OpenAPI | ✅ TW-IFRS | ✅ 2004– | — | ✅ |
| Japan | EDINET | ✅ J-GAAP / IFRS | — (no redistributable source) | ✅ | — |
| Europe | ESEF / IFRS | ✅ statements | — | — | — |

Public pages for every listed operating company: `https://www.gronox.kr/companies/{kr|us|jp|tw}/{symbol}` (e.g. [Samsung Electronics](https://www.gronox.kr/companies/kr/005930)).

## What you get (37 tools)

| Area | Tools |
|---|---|
| Statements & filings | DART / EDGAR financials (with the five nearest peers attached), filings, major events, insider trades (DART · Form 4), 13F institutional holdings, disclosure feed |
| Prices & technicals | Daily OHLCV (KR · US · TW), technical indicators, valuation snapshots with market percentiles |
| Screeners | Minervini trend template, CAN SLIM, Kell and Schwartz playbooks, technical screens, ETF screens — nightly over every listing |
| Peers & segments | `get_peers` by industry group and size, or by business-mix similarity from reported segments |
| Research | Portfolio backtests with trading costs (KR · US · TW), point-in-time factor studies, saved runs, read-only SQL over the database |
| Macro & crypto | FRED series and snapshots, crypto tickers / OHLCV / exchange premium |
| Account | Watchlist, portfolio import |

Tool reference (rendered from the live registry): https://www.gronox.kr/docs

## Quick start

### Claude (claude.ai / Desktop)
Settings → Connectors → Add custom connector → `https://mcp.gronox.kr/mcp` — sign in with Google, no key needed. Then, in each new chat, open **+ → FinBridge** to turn it on (connectors are off per conversation until you do) and ask.

### Claude Code
```bash
claude mcp add --transport http finbridge https://mcp.gronox.kr/mcp --header "Authorization: Bearer smcp_..."
```
Get a key at https://www.gronox.kr/login (Google sign-in, issued instantly).

### ChatGPT (developer mode)
Settings → Apps & Connectors → Advanced → Developer mode → Create connector with the URL above and your `smcp_` key as the access token.

### Any MCP client (Gemini CLI, Cursor, …)
```json
{"mcpServers": {"finbridge": {"httpUrl": "https://mcp.gronox.kr/mcp",
  "headers": {"Authorization": "Bearer smcp_..."}}}}
```

### REST (no MCP client)
```bash
curl -H "Authorization: Bearer smcp_..." https://mcp.gronox.kr/api/v1/companies/kr/005930/financials
curl -H "Authorization: Bearer smcp_..." "https://mcp.gronox.kr/api/v1/companies/us/AAPL/peers?limit=5"
curl -H "Authorization: Bearer smcp_..." "https://mcp.gronox.kr/api/v1/companies/eu/NL0010273215/peers?limit=5"   # Europe by ISIN (ASML): statements-based peers, no prices
```
Endpoints: `/companies/{market}/{symbol}` (profile) · `/financials` · `/valuation` · `/peers` · `/prices`. Same key, same quota, same depth as MCP.

## Built-in prompts

FinBridge registers three MCP prompts, so you can start without typing a question. In Claude.ai or Claude Desktop, turn FinBridge on in the chat (**+ → FinBridge**), then open **+ → FinBridge** again and pick a prompt; in Claude Code type the slash command. Clients that don't list prompts (Cursor, ChatGPT developer mode): paste the one-liner.

| Prompt | What it does | Claude Code | Paste instead |
|---|---|---|---|
| This week's watchlist | What passed the trend, CAN SLIM, VCP and RS screens this week (KR/US/TW), then a closer look at the strongest three | `/mcp__finbridge__weekly_watchlist kr` | "Run this week's FinBridge watchlist for Korea and check the strongest three with get_valuation and get_technicals." |
| Company check-up | One company end to end: four annual statements, valuation vs five peers, technicals, latest filings, every number dated | `/mcp__finbridge__company_checkup 005930` | "Give me a FinBridge check-up of Samsung Electronics (005930) with data_as_of dates." |
| First three questions | A one-minute tour: peers, a screen, four years of statements | `/mcp__finbridge__first_questions` | "I just connected FinBridge — answer its three starter questions and show which tool you used." |

## Good first questions

1. "Compare Samsung Electronics with its five nearest peers on P/E, ROE and revenue growth."
2. "Screen KOSDAQ for names above RS 90 that pass the trend template."
3. "Pull Apple's last four annual statements and summarise margin trends."

## Links

- Product, keys and pricing: https://www.gronox.kr · https://www.gronox.kr/pricing
- Connect guide: https://www.gronox.kr/connect
- Where to get each market's data for free (guides): https://www.gronox.kr/guides
- Data sources and licences: https://www.gronox.kr/sources
- Status: https://mcp.gronox.kr/status
- Registry: `kr.gronox/finbridge` in the official MCP Registry · Smithery `red0920/finbridge` · mcp.so
- 한국어: https://www.gronox.kr/ko · 日本語: https://www.gronox.kr/ja

## Notes

- Data is a nightly snapshot (the filings feed refreshes every 5 minutes); not real-time quotes.
- Statements follow the local accounting standard (K-IFRS, US-GAAP, J-GAAP/IFRS, TW-IFRS), so cross-market ratios are approximations.
- Information only, not investment advice. FinBridge is not affiliated with any trader whose published criteria it implements.
- This repository is the public listing (registry manifest `server.json`) for the hosted service; the server itself is not open source.

Contact: 4y.changemaker@gmail.com

## License

The contents of this repository (listing metadata and documentation) are released under the [MIT License](./LICENSE). The hosted FinBridge service and its source code are not part of this repository and are provided under the [FinBridge Terms of Service](https://www.gronox.kr/terms).
