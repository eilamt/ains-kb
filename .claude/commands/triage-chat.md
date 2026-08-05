---
description: Mine one exported Claude conversation into reviewable proposals
---

Read `$ARGUMENTS` (a file under `raw/claude-exports/`). If no argument, list
untriaged exports and ask which one.

Produce ONE file: `inbox/triage-<export-basename>.md`, containing:

1. **Summary** — 3 sentences on what the conversation was about.
2. **Candidate sources** — every work referenced. For each: author, year,
   title, and whether it was named by the human or by the assistant.
   Also write a stub into `sources/_unverified/` using `templates/source.md`
   with `verified: false`.
3. **Candidate notes** — ideas that could become atomic notes. Do NOT write
   these into `notes/`. Format each one exactly like this, so `/promote` can
   read her decisions back:

   ```
   ### <n>. <proposed-filename>.md
   decision:
   one-line: <the idea in one sentence — a draft for her to replace>
   tags: [...]
   people: [...]
   attach-to: [[x]], [[y]]

   > verbatim passage from the conversation
   ```

   Leave `decision:` empty. She fills it with `promote`, `drop`,
   `merge -> <note>`, or `later`.
4. **Attachments to existing material** — for each candidate, which existing
   note, thread, or person file it should link to. Grep to check.
5. **Questions for her** — anything ambiguous.

Rules:
- Assistant-generated claims and human-generated claims are marked separately.
  Never present something the assistant said as something she thinks.
- Quote verbatim and briefly; do not paraphrase her into blandness.
- Do not touch `notes/`, `people/`, or `missions/`.
- Commit with message `triage-chat: <basename>`.
