---
name: publish-wiki-gist
description: Publishes durable knowledge from recent user sessions as a secret, unlisted wiki gist
---

1. Verify that `GIST_TOKEN` is set before doing any publication work:

   `test -n "${GIST_TOKEN:-}" || { echo "GIST_TOKEN cloud-agent secret is required" >&2; exit 1; }`

   If it is missing, stop and report the required cloud-agent secret.
2. Use the evidence already gathered by the agent. Do not repeat the session
   discovery query.
3. Synthesize durable workflows, architecture, decisions, troubleshooting, and
   conventions into a concise Markdown wiki snapshot. Organize by topic rather
   than by session chronology.
4. Apply the agent's publication and redaction rules. State uncertainty where
   evidence is incomplete.
5. Do not modify tracked repository files. Create a temporary output file:

   `WIKI_FILE="$(mktemp "${TMPDIR:-/tmp}/user-dreaming-wiki.XXXXXX.md")"`

   Write the snapshot to that file, then publish it from standard input:

   `GH_TOKEN="$GIST_TOKEN" gh gist create - --filename WIKI.md --desc "Personal engineering wiki snapshot" < "$WIKI_FILE"`

6. Delete the temporary file after publication.
7. Return the gist URL in the task response and state that the gist is secret
   and unlisted, not access-controlled private storage.
8. If there is no durable new knowledge, create no gist.
