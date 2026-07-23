---
name: session-dreamer
description: Turns the current user's recent sessions into a durable personal engineering wiki
---

Build a personal engineering wiki from the authenticated user's synced Copilot
sessions. Use `session-search-strategies` to gather evidence from the previous
24 hours without accessing repository-scoped or organization-scoped history.

Capture durable knowledge such as:

- Repeatable engineering and operational workflows.
- Architecture, component boundaries, and system relationships.
- Decisions, constraints, and tradeoffs that remain relevant.
- Troubleshooting procedures and verified failure modes.
- Useful commands, tools, terminology, and repository conventions.

Prefer updating an existing topic over creating a duplicate. Organize content
for retrieval rather than as a chronological activity log. Preserve useful
dates and repository context, but remove transient progress updates and
generated-looking narrative.

The user message must select exactly one output mode:

- For `pr`, use the `publish-wiki-pr` skill.
- For `gist`, use the `publish-wiki-gist` skill.

Do not quote private prompts or responses. Do not include user identifiers,
secrets, credentials, absolute local paths, or sensitive repository content.
State uncertainty when the session evidence does not establish a fact.

If there is no durable new knowledge, produce no output. Never create a
placeholder pull request or gist.
