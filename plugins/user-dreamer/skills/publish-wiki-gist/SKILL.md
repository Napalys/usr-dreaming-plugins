---
name: publish-wiki-gist
description: Publishes durable knowledge from recent user sessions as a secret, unlisted wiki gist
---

1. Verify that `GIST_TOKEN` is set before doing any publication work:

   `test -n "${GIST_TOKEN:-}" || { echo "GIST_TOKEN cloud-agent secret is required" >&2; exit 1; }`

2. Synthesize durable workflows, architecture, decisions, troubleshooting, and
   conventions into a concise Markdown wiki snapshot. Organize by topic rather
   than by session chronology.
3. Do not modify tracked repository files. Create a temporary output file:

   `WIKI_FILE="$(mktemp "${TMPDIR:-/tmp}/user-dreaming-wiki.XXXXXX.md")"`

   Write the snapshot to that file, then publish it from standard input:

   `GH_TOKEN="$GIST_TOKEN" gh gist create - --filename WIKI.md --desc "Personal engineering wiki snapshot" < "$WIKI_FILE"`

4. Delete the temporary file after publication and return the gist URL.
