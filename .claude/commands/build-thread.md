---
description: Assess the state of one thread across the whole repository
---

Argument: a thread name, e.g. `ai-native-infrastructure`. Read
`missions/*/threads/<name>.md` first — its `question:` field defines relevance.

**This command is read-only apart from the memo it writes.** It must not
modify the thread file. That file holds her position; you report on the
evidence.

Gather everything related: notes, sources, people files, and archived triage
files matching by tag, `people:`, explicit wikilink, or clear topical bearing.
State your inclusion criteria in the memo so she can tell what you missed.

Write to `inbox/thread-<name>-<date>.md`:

## 1. Inventory
Counts and a table: notes (by status), sources (by read status and
verification), people, conversations touched. Note anything tagged for the
thread that has never been linked from it.

## 2. Proposed argument structure
An ordering of the moves the material currently supports. Each move: one
line, plus the notes/sources backing it. This is a proposal about *her*
material, not your own argument — build it only from what exists in the repo.

## 3. Gaps
- Moves in the structure with no supporting note
- Claims resting entirely on `verified: false` sources
- Claims resting entirely on assistant-originated material from a chat
  export rather than on a real source. Flag these hardest.

## 4. Tensions
Notes that appear to conflict, with the conflicting lines quoted. Do not
resolve them. These are usually the most valuable part of the memo.

## 5. Reading not yet done
Sources tagged for this thread with `status: unread`, ranked by how many
gaps in §3 each would close. Include `holdings:` so she knows what she can
reach today.

## 6. Verdict
Two or three sentences: is this thread converging on an argument, or
accumulating material without shape? Say so plainly. "Accumulating" is a
useful and common answer.

Commit: `build-thread: <name>`.
