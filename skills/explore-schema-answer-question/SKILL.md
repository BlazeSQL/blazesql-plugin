---
name: explore-schema-answer-question
description: Explore a BlazeSQL database schema, identify the right tables and columns, and answer a user question with a read-only SQL query. Use when the user needs new analysis instead of an existing saved query or dashboard.
---

# Explore Schema And Answer A Question

## When to use

- The user wants a fresh answer from a connected SQL database.
- The user asks a data question but has not named a saved query, graph, or dashboard.
- You need to discover the schema before writing SQL.

## Instructions

1. Start with `list_schemas`.
   - If the database has a single visible schema or BlazeSQL already inlines small-schema metadata, use that extra detail.
   - Otherwise continue progressively instead of guessing table names.

2. Narrow the search with `list_tables`.
   - Pass one or more schema names from `list_schemas`.
   - Prefer the smallest relevant scope first.

3. Inspect the exact tables you need with `describe_tables`.
   - Use exact `schema.table` names from prior results.
   - Pay attention to column descriptions, knowledge notes, and permissions hints.

4. Run the analysis with `execute_sql`.
   - Keep the SQL read-only.
   - Explain the result in plain language after inspecting the returned rows.
   - Use the schema-discovery tools as the primary way to understand the database. Do not default to saved-query or dashboard tools for ordinary questions.

5. If the user also wants the SQL, share it from the `execute_sql` result.

6. If `execute_sql` indicates reusable context would help future requests, do not immediately write it.
   - Summarize the proposed lesson first.
   - Ask the user to confirm before calling `suggest_schema_context_update`, because that tool writes a context suggestion for admin review.

## Good defaults

- Start broad, then narrow.
- Prefer exact schema and table names over assumptions.
- Keep the final answer grounded in the returned rows, not just the SQL text.
