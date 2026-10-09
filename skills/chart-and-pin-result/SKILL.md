---
name: chart-and-pin-result
description: Turn BlazeSQL query results into a chart and optionally save that chart to a dashboard. Use when the user wants a visualization, a saved graph, or a dashboard tile based on a BlazeSQL query result.
---

# Chart A Result And Pin It

## When to use

- The user wants a chart from query results.
- The user wants to save a graph in BlazeSQL.
- The user wants to pin a result to an existing dashboard.

## Instructions

1. Start from the data.
   - For fresh analysis, use schema discovery plus `execute_sql` first.
   - If the user explicitly wants an existing saved query or graph, you may use `query_id`-based flows instead.

2. Build the visualization with `graph_sql_result`.
   - Prefer `query_request_id` from `execute_sql` so the graph matches the exact result you inspected.
   - Choose a graph type and axes that fit the returned column names and row shape.
   - Keep any `dynamicChartCode` consistent with BlazeSQL's runtime assumptions: `data.rows` is an array of objects keyed by exact column name.

3. Show or summarize the chart result for the user before saving anything.

4. If the user wants the graph saved to a dashboard, confirm the write first.
   - Confirm the target dashboard.
   - Confirm the saved graph name and any description.
   - If the dashboard name is ambiguous, use `list_dashboards` or `search_dashboards` only to identify the intended dashboard ID.

5. After confirmation, call `add_graph_to_dashboard`.
   - This tool writes a saved BlazeSQL graph and adds a dashboard tile.
   - Treat it as non-idempotent and do not call it speculatively.

## Guardrails

- `graph_sql_result` is read-only.
- `add_graph_to_dashboard` writes data and must only run after user confirmation.
- If reusable business context emerges, ask before calling `suggest_schema_context_update`, because that tool also writes.
