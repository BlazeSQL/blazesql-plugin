---
name: find-saved-analysis
description: Find, inspect, and optionally rerun BlazeSQL saved queries, graphs, and dashboards. Use when the user asks for an existing report, dashboard, tile, saved graph, or saved query rather than a brand-new analysis.
---

# Find And Use Saved Analysis

## When to use

- The user asks for an existing saved query, saved graph, dashboard, report, or dashboard tile.
- The user names a dashboard or report and wants to know what is in it.
- The user wants to rerun a saved query with BlazeSQL's `query_id` execution flow.

## Instructions

1. Identify the asset type the user wants.
   - Use `list_saved_queries` or `search_saved_queries` for saved queries and saved graphs.
   - Use `list_dashboards` or `search_dashboards` for dashboards and reports.
   - Use search tools only to find the requested saved asset, not for ordinary database discovery.

2. Inspect the exact asset with the read tool.
   - Use `read_saved_query` for a saved query or graph.
   - Use `read_dashboard` for a dashboard.

3. If the user wants fresh results from a saved query, run `execute_sql` with `query_id`.
   - If the saved query has variables, gather any required `query_variable_values` first.
   - Prefer `query_id` only when the user explicitly wants that saved query or a dashboard-linked query tile. For new analysis, use schema discovery plus raw SQL instead.

4. Summarize the saved asset clearly.
   - For saved queries, mention the name, description, SQL purpose, variables, graph configuration, and BlazeSQL URL when relevant.
   - For dashboards, mention the tile mix, linked query tiles for the selected database, text tiles, refresh settings, and BlazeSQL URL when relevant.

## Guardrails

- `list_saved_queries`, `search_saved_queries`, `read_saved_query`, `list_dashboards`, `search_dashboards`, and `read_dashboard` are read-only.
- Do not use `add_graph_to_dashboard` unless the user explicitly asks to save or pin a graph.
- If a follow-up suggests reusable database context, ask before calling `suggest_schema_context_update` because it writes a suggestion for admin review.
