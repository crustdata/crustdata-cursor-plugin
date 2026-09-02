# Changelog

All notable changes to this plugin will be documented here.

## 1.0.0 (initial release)

- Added the `crustdata` MCP server backed by Crustdata's hosted MCP (`https://install.crustdata.com/mcp`).
- Auth uses OAuth via Crustdata sign-in. No API key to configure.
- Added `crustdata-tool-selection` rule: how to drive the Code Mode server (`list_tools` / `get_schema` / `execute`) and which tool to reach for, cheapest correct path first.
- Bundled Crustdata's public skills catalog (the skills published at crustdata/skills).
