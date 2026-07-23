---
name: publish-wiki-pr
description: Publishes durable knowledge from recent user sessions as a personal wiki pull request
---

1. Read the existing `wiki/` directory before writing. If it does not exist,
   create `wiki/index.md` and `wiki/topics/`.
2. Reuse existing topic pages and preserve useful structure. Keep
   `wiki/index.md` as a concise map of topic pages and store detailed content in
   lower-case, kebab-case `wiki/topics/SLUG.md` files.
3. Organize by topic, system, workflow, or decision rather than by session.
   Include dates only where they help establish currency or decision history.
4. Limit the pull request to the wiki update and summarize the knowledge added
   without exposing session content.
