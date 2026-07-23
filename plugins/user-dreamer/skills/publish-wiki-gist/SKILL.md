---
name: publish-wiki-gist
description: Publishes durable knowledge from recent user sessions as a private personal wiki gist
---

1. Use `session-search-strategies` to gather user-scoped evidence from the
   previous 24 hours.
2. Synthesize durable workflows, architecture, decisions, troubleshooting, and
   conventions into a concise Markdown wiki. Organize by topic rather than by
   session chronology.
3. Do not modify the repository. Write the result to a temporary `WIKI.md`.
4. Remove private session text, secrets, personal paths, transient status, and
   generated-looking narrative. State uncertainty where evidence is incomplete.
5. Require `GIST_TOKEN` as a cloud-agent secret with permission to create
   gists. Publish a secret gist with:

   `GH_TOKEN="$GIST_TOKEN" gh gist create WIKI.md --desc "Personal engineering wiki update"`

6. Return the gist URL in the task response.
7. If there is no durable new knowledge, create no gist.
