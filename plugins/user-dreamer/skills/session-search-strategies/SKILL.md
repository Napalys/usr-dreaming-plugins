---
name: session-search-strategies
description: Provides bounded, user-scoped strategies for gathering relevant Copilot session history.
user-invocable: false
---

## Scope

Search only the authenticated user's synced session history. Never request
repository-scoped or organization-scoped access and never pass a `repo` or
`org` scope to `session_store_sql`.

The visible history may include the user's CLI, cloud agent, code review, IDE,
and Copilot app sessions. It does not include local-only sessions that were not
synced.

## Discovery

Prefer precise anchors before broad discovery. Extract exact session IDs,
quotes, repository names, paths, branches, tools, timestamps, PR or issue
numbers, and commit SHAs from the task before searching.

Run one user-scoped 24-hour discovery query:

```sql
SELECT id, summary, repository, branch, agent_name, updated_at
FROM sessions
WHERE updated_at > now() - INTERVAL '24 hours'
ORDER BY updated_at DESC
LIMIT 100
```

Do not widen beyond 24 hours unless the user explicitly requests it. If the
query times out, retry once with fewer columns and `LIMIT 50`. Stop after a
second timeout.

Group candidate sessions by topic and select at most ten session IDs for
detailed inspection. Prefer sessions with substantive summaries, successful
outcomes, repeated workflows, or matching repository and tool anchors.

## Detailed inspection

Do not scan `turns` or `events` without first selecting candidate session IDs.
Use `tool_requests` to find anchored work:

```sql
SELECT session_id, tool_call_id, name,
       substr(COALESCE(arguments_json, ''), 1, 600) AS args
FROM tool_requests
WHERE session_id IN ('<session-id-1>', '<session-id-2>')
  AND (
    COALESCE(arguments_json, '') ILIKE '%<anchor-1>%'
    OR COALESCE(arguments_json, '') ILIKE '%<anchor-2>%'
  )
LIMIT 50
```

Retrieve completion snippets only for matching call IDs:

```sql
SELECT session_id, timestamp, tool_complete_call_id,
       substr(COALESCE(tool_complete_result_content, ''), 1, 1200) AS result
FROM events
WHERE session_id IN ('<session-id-1>', '<session-id-2>')
  AND type = 'tool.execution_complete'
  AND tool_complete_call_id IN ('<tool-call-id-1>', '<tool-call-id-2>')
ORDER BY timestamp DESC
LIMIT 20
```

Use `turns` only for selected session IDs when tool evidence does not contain
enough context:

```sql
SELECT session_id, turn_index,
       substr(COALESCE(user_message, ''), 1, 500) AS user_msg,
       substr(COALESCE(assistant_response, ''), 1, 700) AS assistant_msg
FROM turns
WHERE session_id IN ('<session-id-1>', '<session-id-2>')
ORDER BY session_id, turn_index
LIMIT 50
```

If a query is noisy or slow, narrow by session ID, time, tool name, event type,
or an exact anchor. Select fewer columns and split complex queries rather than
repeating the same broad query.

## Evidence handling

Do not treat the current run, pasted transcripts, or discussions about the
search prompt as independent evidence. Prefer original source sessions.

A zero-row result means insufficient visible evidence, not that an event did
not happen. Distinguish zero rows from timeouts and state uncertainty rather
than inventing conclusions.

When `_query_source` provenance is returned, preserve it. Do not select or
invent provenance fields in SQL.
