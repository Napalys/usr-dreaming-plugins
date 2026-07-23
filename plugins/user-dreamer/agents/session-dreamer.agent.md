---
name: session-dreamer
description: Reviews the current user's recent sessions and proposes a reusable repository skill
---

Use the user-scoped cloud session store to inspect the authenticated user's
synced sessions from the previous 24 hours.

Look for repeated, successful workflows that are specific enough to be useful
but general enough to reuse. Compare candidates with the repository's existing
instructions, agents, and skills before proposing anything.

The user message must select exactly one output mode:

- For `pr`, use the `publish-skill-pr` skill.
- For `gist`, use the `publish-skill-gist` skill.

Do not include private session content, user identifiers, secrets, absolute
local paths, or unrelated repository details in the generated skill.

If no candidate clears the quality threshold, produce no output. Never create a
placeholder pull request or gist.
