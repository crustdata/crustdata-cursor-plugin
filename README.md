# Crustdata

Cursor plugin that connects agents to [Crustdata](https://crustdata.com) through Crustdata's official hosted [Model Context Protocol](https://modelcontextprotocol.io/) server.

Search and enrich 800M+ people and 200M+ companies with live B2B data: people and company search, firmographic enrichment, contact data, job listings, and social posts, straight from the signed-in Crustdata account.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Crustdata**.
3. Click **Install**, then complete the Crustdata sign-in prompt.

Or run `/add-plugin crustdata` in chat.

## MCP

```json
{
  "mcpServers": {
    "crustdata": {
      "type": "http",
      "url": "https://install.crustdata.com/mcp"
    }
  }
}
```

Auth is OAuth against Crustdata. Cursor opens a Crustdata sign-in window the first time the plugin connects. There is no API key to configure.

## How it works

The server is Code Mode: it exposes three tools — `list_tools`, `get_schema`, and `execute` — and the agent reaches every data operation by writing a short JavaScript script for `execute` that calls `callTool('person_search', …)`, `callTool('company_enrich', …)`, and so on. `list_tools` carries the full annotated tool list with per-tool pricing; `get_schema` returns filterable columns and response shapes before any credits are spent.

## Before you connect

You need a Crustdata account with API credits. Most tools bill per result; company identification and the autocomplete tools are free. Agents can check the balance with the free `account_credits` tool, and every tool call's result reports the exact `credits_used`.

## What agents can do

| Category | Capabilities |
| --- | --- |
| People | Search 800M+ profiles by company, title, seniority, and region (`person_search`); enrich full profiles (`person_enrich`) |
| Companies | Identify by name or domain for free (`company_identify`), enrich firmographics, headcount, funding, and technographics (`company_enrich`) |
| Contacts | Emails and phone numbers via `person_contact_enrich`, billed per contact type returned |
| Jobs | Search job listings with filters and aggregations (`job_search`), or live-scrape a company's openings (`job_search_live`) |
| Social | Pull LinkedIn posts by person, company, or keyword (`social_post_list_live`, `social_post_search_live`) |
| Web | Live web/news search and page fetch (`web_search_live`, `web_enrich_live`) |
| Alerts | Watchers on people, companies, and jobs (`watch_create`, `watch_discovery_create`) |

The hosted runtime is the source of truth for tool names and schemas.

## Included

- `rules/crustdata-tool-selection.mdc`: how to drive the Code Mode server and which tool to reach for
- `skills/`: Crustdata's public skills catalog — the same skills published at [crustdata/skills](https://github.com/crustdata/skills) — covering prospecting, account research, outreach, meeting prep, candidate sourcing, and email enrichment

## Notes

- Tool calls run as the Crustdata user who authorizes the connection and draw from that account's credit balance.
- Indexed DB search tools bill cheaply per result (~0.03 credits); the bundled rule steers agents to them before the live variants (2 credits/result).

## Docs

- API docs: https://docs.crustdata.com
- Server URL: https://install.crustdata.com/mcp

## License

MIT
