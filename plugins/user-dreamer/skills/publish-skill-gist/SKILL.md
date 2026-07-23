---
name: publish-skill-gist
description: Publishes a strongly supported skill proposal as a private gist
---

1. Query the user-scoped session store for sessions updated during the previous
   24 hours. Select only the fields needed to identify repeated workflows.
2. Read the most relevant session turns and tool activity. Prefer workflows
   demonstrated successfully in at least two independent sessions.
3. Search `.github/skills`, `.github/agents`, and repository instructions for
   an existing equivalent. Do not publish a duplicate.
4. Reject candidates that depend on secrets, personal paths, transient
   incidents, one-off fixes, or context that cannot be safely generalized.
5. If one candidate remains, write a concise `SKILL.md` to a temporary
   directory. Do not modify the repository.
6. Require `GIST_TOKEN` to be available as a cloud-agent secret with permission
   to create gists. Publish a secret gist with:

   `GH_TOKEN="$GIST_TOKEN" gh gist create SKILL.md --desc "Copilot skill proposal"`

7. Return the gist URL in the task response without quoting private session
   content.
8. If no candidate is sufficiently supported, create no gist.
