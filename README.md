# FinBridge — Korean DART filings in English, with US, Japan and Europe for comparison. One MCP.

**Official Korean company data for AI clients.** FinBridge collects DART filings and financial statements every night (the filings feed every 5 minutes), adds plain-language English summaries of material disclosures, and serves them to ChatGPT, Claude, Cursor or any MCP client, and over a REST API. US (SEC EDGAR), Japan (EDINET), Taiwan and Europe (ESEF) statements are there as comparison counterparts.

- **MCP endpoint (Streamable HTTP):** `https://mcp.gronox.kr/mcp`
- **REST API:** `https://mcp.gronox.kr/api/v1` · OpenAPI 3.1: `https://mcp.gronox.kr/api/v1/openapi.json`
- **Free plan, no card:** 10 calls a day across the web and your AI, every tool, the last 4 fiscal years. Paid plans buy volume and history depth. Current plans: https://www.gronox.kr/pricing

Official sources only, and only sources we may redistribute: OpenDART, SEC EDGAR, EDINET, TWSE/TPEx OpenAPI, ESEF filings and data.go.kr (Financial Services Commission). Every answer names its source and as-of date, and every company carries a `page_url` to a public page with the filing behind each number.

## Coverage

| Market | Source | Statements & filings | Segments |
|---|---|---|---|
| Korea (KRX) | OpenDART · data.go.kr | ✅ K-IFRS, normalised, revisions kept, English summaries of material filings | ✅ |
| United States | SEC EDGAR | ✅ US-GAAP, as-filed (point-in-time) history | ✅ (SEC DERA) |
| Japan | EDINET | ✅ J-GAAP / IFRS | ✅ |
| Taiwan | TWSE / TPEx OpenAPI | ✅ TW-IFRS | — |
| Europe | ESEF / IFRS | ✅ statements | — |

Korean and US stock price delivery is paused; prices are not part of what FinBridge sells today.

Public pages for every listed operating company: `https://www.gronox.kr/companies/{kr|us|jp|tw}/{symbol}` (e.g. [Samsung Electronics](https://www.gronox.kr/companies/kr/005930)).

## What you get

| Area | Tools |
|---|---|
| Korean filings | DART filings, major-event reports, the disclosure feed with plain-language English summaries, filing bodies by section and table (`get_dart_document`), company search |
| Statements | DART and EDGAR financial statements with revision history, and a Korea–US comparison (`compare_financials_kr_us`) |
| Insiders & holders | DART executive and major-shareholder trades, SEC Form 4, Taiwan insider transfers, 13F institutional holdings |
| Comparison references | `get_peers` across KR / US / TW / JP / EU from sourced business themes and reported segments |
| Account | Watchlist, portfolio import and history, read-only SQL over the filings database |

Korean and US stock prices, technicals, valuation and screens are paused: those tools answer with a notice. Nothing here is investment advice.

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
curl -H "Authorization: Bearer smcp_..." "https://mcp.gronox.kr/api/v1/companies/eu/NL0010273215/peers?limit=5"   # Europe by ISIN: statements-based peers, no prices (EU groups all IT/electronics together, so treat the list as a starting point)
```
Endpoints: `/companies/{market}/{symbol}` (profile) · `/financials` · `/peers`. `/valuation` and `/prices` answer with the pause notice. Same key, same quota, same depth as MCP.

## Built-in prompts

FinBridge registers three MCP prompts, so you can start without typing a question. In Claude.ai or Claude Desktop, turn FinBridge on in the chat (**+ → FinBridge**), then open **+ → FinBridge** again and pick a prompt; in Claude Code type the slash command. Clients that don't list prompts (Cursor, ChatGPT developer mode): paste the one-liner.

| Prompt | What it does | Claude Code | Paste instead |
|---|---|---|---|
| This week's filings | This week's material filings for the companies you follow (or one market's if you follow none), grouped by company with each filing's figures and link | `/mcp__finbridge__weekly_watchlist kr` | "Show this week's FinBridge filings for the companies I follow, grouped by company, facts only." |
| Company check-up | One company, facts only: four annual statements, comparison references, recent filings and insider trades, every number dated | `/mcp__finbridge__company_checkup 005930` | "Give me a FinBridge check-up of Samsung Electronics (005930) with data_as_of dates." |
| First three questions | A one-minute tour: a company's recent filings, this month's treasury-share announcements, a Korea–US financials comparison | `/mcp__finbridge__first_questions` | "I just connected FinBridge — answer its three starter questions and show which tool you used." |

## Good first questions

1. "What did Samsung Electronics disclose in the last 30 days? Summarize the material filings in English."
2. "Which Korean listed companies announced treasury-share purchases this month?"
3. "Compare SK hynix and Micron on revenue and operating margin over the last three years."

## Links

- Product, keys and pricing: https://www.gronox.kr · https://www.gronox.kr/pricing
- Connect guide: https://www.gronox.kr/connect
- Where to get each market's data for free (guides): https://www.gronox.kr/guides
- Data sources and licences: https://www.gronox.kr/sources
- Status: https://mcp.gronox.kr/status
- Registry: `kr.gronox/finbridge` in the official MCP Registry · Smithery `red0920/finbridge` · mcp.so
- 한국어: https://www.gronox.kr/ko · 日本語: https://www.gronox.kr/ja

## Notes

- Statements are a nightly snapshot (the filings feed refreshes every 5 minutes).
- Statements follow the local accounting standard (K-IFRS, US-GAAP, J-GAAP/IFRS, TW-IFRS), so cross-market ratios are approximations.
- Information only, not investment advice: no ratings, target prices or buy/sell views.
- This repository is the public listing (registry manifest `server.json`) for the hosted service; the server itself is not open source.

Contact: 4y.changemaker@gmail.com

## License

The contents of this repository (listing metadata and documentation) are released under the [MIT License](./LICENSE). The hosted FinBridge service and its source code are not part of this repository and are provided under the [FinBridge Terms of Service](https://www.gronox.kr/terms).
