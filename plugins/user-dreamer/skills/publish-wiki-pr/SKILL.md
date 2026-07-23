---
name: publish-wiki-pr
description: Publishes durable knowledge from recent user sessions as a personal wiki pull request
---

1. Use the evidence already gathered by the agent. Do not repeat the session
   discovery query.
2. Read the existing `wiki/` directory before writing. If it does not exist,
   create `wiki/index.md` and `wiki/topics/`.
3. Reuse existing topic pages and preserve useful structure. Keep
   `wiki/index.md` as a concise map of topic pages and store detailed content in
   lower-case, kebab-case `wiki/topics/SLUG.md` files.
4. Organize by topic, system, workflow, or decision rather than by session.
   Include dates only where they help establish currency or decision history.
5. Apply the agent's publication and redaction rules. Add only durable,
   evidence-supported knowledge and remove transient status, duplication, and
   generated-looking prose.
6. Prefer a small update to an existing page. Create a new page only when no
   existing topic fits.
7. Limit the pull request to the wiki update and summarize the knowledge added
   without exposing session content.
8. If there is no durable new knowledge, make no changes.
