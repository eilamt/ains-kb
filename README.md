# ains

Private knowledge base on AI Native Systems. Markdown + git. Obsidian is the
editor; Claude Code is the agent. See `CLAUDE.md` for the working agreement
and `index.md` for the map.

## Layout
- `missions/` — what is being made
- `notes/` — atomic notes, one concept each
- `people/` — thinkers
- `sources/` — bibliographic catalog (metadata only)
- `library/` — PDFs and ebooks, **not in git**, synced separately
- `inbox/` — capture and agent proposals, triaged weekly
- `raw/` — verbatim exports, immutable
- `templates/` — copy these, don't improvise

## The loop
- `/triage-chat <export>` → proposals in `inbox/`
- you mark `decision:` on each candidate
- `/promote <triage-file>` → notes created, provenance wired, TODO lines left for you
- you write the one-sentence statements
- `/verify-refs` → sources checked and promoted out of quarantine
- `/build-thread <name>` → memo on where a thread actually stands (run rarely)

## Weekly ritual (20 min)
1. Empty `inbox/` — decide and promote.
2. Run `/verify-refs`.
3. Run `/review`, act on one or two items. Ignore the rest.
4. Commit.
