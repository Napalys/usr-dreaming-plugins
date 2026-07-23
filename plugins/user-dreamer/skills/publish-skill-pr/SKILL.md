---
name: publish-skill-pr
description: Publishes a strongly supported skill proposal as a pull request
---

1. Query the user-scoped session store for sessions updated during the previous
   24 hours. Select only the fields needed to identify repeated workflows.
2. Read the most relevant session turns and tool activity. Prefer workflows
   demonstrated successfully in at least two independent sessions.
3. Search `.github/skills`, `.github/agents`, and repository instructions for
   an existing equivalent. Reuse or improve existing guidance instead of
   duplicating it.
4. Reject candidates that depend on secrets, personal paths, transient
   incidents, one-off fixes, or context that cannot be safely generalized.
5. If one candidate remains, create a concise `.github/skills/NAME/SKILL.md`
   containing actionable instructions and clear trigger conditions.
6. Limit the pull request to that single skill. Explain which recurring
   workflow motivated it without quoting private session content.
7. If no candidate is sufficiently supported, make no changes.
