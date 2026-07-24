---
name: publish-wiki-gist
description: Publishes durable knowledge from recent user sessions as a secret, unlisted wiki gist
---

1. Verify that `GIST_TOKEN` is set before doing any publication work:

   `test -n "${GIST_TOKEN:-}" || { echo "GIST_TOKEN cloud-agent secret is required" >&2; exit 1; }`

2. Synthesize durable workflows, architecture, decisions, troubleshooting, and
   conventions into a concise Markdown wiki snapshot. Organize by topic rather
   than by session chronology.
3. Do not modify tracked repository files. Create a temporary directory and
   write the snapshot to `WIKI.md` inside it:

   `WIKI_DIR="$(mktemp -d "${TMPDIR:-/tmp}/user-dreaming-wiki.XXXXXX")"`

4. If `DREAM_GIST_ID` is set, replace `WIKI.md` in that gist:

   `(cd "$WIKI_DIR" && GH_TOKEN="$GIST_TOKEN" gh gist edit "$DREAM_GIST_ID" WIKI.md)`

   Otherwise, create a secret gist:

   `GH_TOKEN="$GIST_TOKEN" gh gist create "$WIKI_DIR/WIKI.md" --desc "Personal engineering wiki snapshot"`

5. Delete the temporary directory and return the gist URL.
