# BlazeSQL

BlazeSQL lets you query connected SQL databases with plain English, inspect
schema metadata, reuse saved analyses, and turn query results into charts.
It is designed for analytics workflows where you want grounded answers, the
generated SQL, and structured results in one place.

BlazeSQL supports PostgreSQL, MySQL, SQL Server, BigQuery, Snowflake, and
other SQL databases connected through BlazeSQL.

## What this plugin includes

- A remote MCP connection to `https://mcp.blazesql.com/mcp`
- OAuth sign-in to BlazeSQL
- Skills for schema exploration, saved-analysis lookup, and charting workflows
- No embedded API keys, headers, or local setup scripts

## Requirements

- A BlazeSQL account
- At least one database already connected in BlazeSQL, or permission to connect
  one during setup

## How to connect

1. Install the plugin in Cursor or another compatible plugin host.
2. On first use, sign in with BlazeSQL through the OAuth flow.
3. Pick the BlazeSQL database you want the MCP connection to use.
4. Ask a question, inspect a saved analysis, or request a chart.

This plugin uses BlazeSQL's hosted MCP server and OAuth flow. It does not ask
you to paste API keys into the plugin configuration.

## Tool list

### Schema discovery and SQL execution

- `list_schemas` - List visible schemas, with descriptions and table counts.
- `list_tables` - List tables for one or more schema names.
- `describe_tables` - Return detailed metadata for specific `schema.table`
  references, including columns and knowledge notes.
- `execute_sql` - Run one read-only SQL statement or rerun a saved query by
  `query_id`, then return structured rows and query metadata.

### Saved queries and dashboards

- `list_saved_queries` - List saved queries and saved graphs for the selected
  BlazeSQL database.
- `search_saved_queries` - Search saved query names, descriptions, and SQL.
- `read_saved_query` - Read one saved query or saved graph in detail.
- `list_dashboards` - List accessible dashboards for the selected database.
- `search_dashboards` - Search dashboards, dashboard text, and linked query
  content.
- `read_dashboard` - Read one dashboard, including ordered content tiles.

### Visualization and memory updates

- `graph_sql_result` - Build a BlazeSQL-compatible chart from an executed query
  result or saved query.
- `add_graph_to_dashboard` - Save a graph and add it as a dashboard tile.
  This writes data in BlazeSQL and should only be used after user confirmation.
- `suggest_schema_context_update` - Submit reusable database context for admin
  review. This writes a suggestion record and should only be used after user
  confirmation.

### Compatibility and interactive-query helpers

- `blazesql_query` - Natural-language BlazeSQL query tool kept for
  compatibility with earlier BlazeSQL MCP clients.
- `check_query_status` - Poll the status of an in-flight BlazeSQL query.
- `blazesql_query_progress` - Internal progress helper used by BlazeSQL's
  interactive query UI.

## Recommended usage

- For a new question, start with schema discovery:
  `list_schemas` -> `list_tables` -> `describe_tables` -> `execute_sql`
- For an existing report or graph, use saved-query or dashboard tools first.
- For a chart, use `execute_sql` before `graph_sql_result` so the chart is
  based on the exact result you inspected.
- Confirm with the user before using write tools:
  `add_graph_to_dashboard` and `suggest_schema_context_update`

## Privacy, terms, and support

- Privacy: https://www.blazesql.com/privacy
- Terms: https://www.blazesql.com/terms
- Support: https://help.blazesql.com/en/
