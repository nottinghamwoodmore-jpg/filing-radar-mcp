# Filing Radar MCP

Live SEC filings for AI agents. Connect Claude, Cursor or any MCP client to parsed insider trades, 8-Ks, 5% stakes, IPO filings and red flags from [thefilingradar.com](https://thefilingradar.com), refreshed every 90 seconds, with plain-English summaries that are checked against the filing text.

**Endpoint:** `https://thefilingradar.com/mcp` (remote, Streamable HTTP)
**Auth:** `Authorization: Bearer fr_live_...` (free 14-day trial key, no card: https://thefilingradar.com/developers)

## Connect

Claude Code:

```bash
claude mcp add --transport http filing-radar https://thefilingradar.com/mcp \
  --header "Authorization: Bearer fr_live_YOUR_KEY"
```

Claude Desktop, Cursor and other clients:

```json
{
  "mcpServers": {
    "filing-radar": {
      "type": "http",
      "url": "https://thefilingradar.com/mcp",
      "headers": { "Authorization": "Bearer fr_live_YOUR_KEY" }
    }
  }
}
```

## Tools

| Tool | What it does |
| --- | --- |
| `get_insider_trades` | Form 4 insider buys and sells. Filters: `buys_only`, `cluster_only` (2+ insiders buying the same company), `exclude_planned` (skip 10b5-1 plan trades), `min_value`, `ticker`, `day`. `from_date` / `to_date` search history back to 2020 (open-market buys and sells). |
| `get_transactions` | Business plan. Every Form 4/5 transaction line back to 2006: all codes (buy, sale, grant, option exercise, tax withholding, gift), derivatives included. |
| `get_filings` | Latest parsed filings: 8-K, insider, stake, IPO, red flag. |
| `get_company_filings` | A company's name, industry, exchanges and latest filings. |
| `get_summaries` | Newest verified plain-English summaries, optionally per ticker. |
| `get_summary` | One summary by SEC accession number. |
| `get_usage` | Your plan, calls today and limits. |

Listing the tools needs no key. Calling them does.

## Try asking

- "Which insiders made open-market buys over $250,000 today? Skip anything under a 10b5-1 plan."
- "Any cluster buys in the last two weeks? Group them by company."
- "Summarize the latest filings for NVDA and flag anything unusual."
- "Show open-market insider buys over $1M in 2022."

## Plans

Free 14-day trial (100 calls a day, history 90 days back). Developer $29/month (5,000 calls a day, full history). Business $99/month (50,000 calls a day, webhooks, and full Form 4/5 history back to 2006). Same key for the REST API and MCP. Docs: https://thefilingradar.com/developers

Data is public-domain SEC EDGAR data. Summaries are AI-written, checked against the filing and labeled Verified, Partly verified or Unverified. Informational only, not investment advice.
