---
name: publish-wiki-pr
description: Publishes durable knowledge from recent user sessions as a personal wiki pull request
---

1. Use `session-search-strategies` to gather user-scoped evidence from the
   previous 24 hours.
2. Read the existing `wiki/` directory before writing. Reuse existing topic
   pages and preserve useful structure.
3. Keep `wiki/index.md` as a concise map of topic pages. Store detailed content
   in `wiki/topics/SLUG.md`.
4. Organize by topic, system, workflow, or decision rather than by session.
   Include dates only where they help establish currency or decision history.
5. Add only durable, evidence-supported knowledge. Remove transient status,
   duplicated explanations, private session text, and generated-looking prose.
6. Prefer a small update to an existing page. Create a new page only when no
   existing topic fits.
7. Limit the pull request to the wiki update. Summarize the knowledge added
   without exposing session content.
8. If there is no durable new knowledge, make no changes.
