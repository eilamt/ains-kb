---
description: Execute the decisions marked in a reviewed triage file
---

Argument: a triage file in `inbox/`. If none given, list triage files that
contain at least one `decision:` line and ask which.

## Before doing anything

Refuse to run if any candidate in the file has an empty or missing
`decision:` line. Report which ones and stop. Partial promotion silently
loses candidates.

Valid decisions: `promote`, `drop`, `merge -> <existing-note>`, `later`.

## For each candidate

**promote**
- Create `notes/<proposed-filename>` from `templates/note.md`.
- Fill frontmatter: `title`, `tags`, `people`, `missions`, `status: seed`,
  `created`, `updated`. Tags must come from `sources/_tags.md`; if the
  proposal used a tag not in the vocabulary, leave it out and list it under
  "Needs her attention".
- Body: write `<!-- TODO: state this idea in one sentence, your words -->`
  as the first line. **Do not write that sentence yourself.**
- Under `## Provenance`, paste the verbatim passage in a blockquote and add
  the `provenance:` frontmatter pointer to the file in `raw/`.
- Create the wikilinks named in the proposal. If a link target does not
  exist, leave the link and list it under "Dangling links" — do not create
  stub files.
- Add a backlink line in each existing target file under its
  `## Connects to` or `## Threads they bear on` section. This is the one
  case where you may edit `notes/` and `people/` directly.

**merge -> X**
- Append the passage and provenance pointer to `X` under `## Provenance`.
- Do not rewrite or reorganize X's existing prose.

**drop** — do nothing. Count it.

**later** — leave in place; the triage file will not be archived.

## Sources

Source stubs referenced by promoted candidates stay in
`sources/_unverified/`. Promotion of a note never promotes a source.
Only `/verify-refs` does that.

## Finishing

- If every candidate was resolved (no `later`), move the triage file to
  `inbox/_archive/`. Otherwise leave it.
- Report: promoted / merged / dropped / deferred, plus "Needs her attention"
  (rejected tags, dangling links) and the list of notes carrying a TODO line.
- Commit: `promote: N notes from <basename>`.

## Never
- Write the one-sentence statement of an idea. That is hers.
- Rewrite existing prose in `notes/`, `people/`, `missions/`.
- Create stub files for missing link targets.
