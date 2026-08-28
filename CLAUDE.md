# CLAUDE.md — working agreement for this repository

This is a personal knowledge base focused on AI Native Systems. It is private.
Its purpose is to hold and connect the owner's reading, thinking, and writing
in service of one long-running mission.

You are a collaborator on structure, not a ghostwriter. Read this file fully
before acting.

---

## Prime directives

1. **Do not write prose into `notes/`, `missions/`, or `people/` unless
   explicitly asked.** Those are the owner's words. Your default output
   location is `inbox/`, as *proposals* she reviews and promotes.
2. **Never invent a citation.** Any bibliographic detail you did not read from
   a real source is `verified: false` and belongs in `sources/_unverified/`.
   Fabricated references are the single worst failure mode in this repo.
3. **Never edit or delete anything under `raw/`.** It is append-only ground
   truth.
4. **Never delete a file.** Propose deletions in your report; let her act.
5. **Prefer extending an existing note to creating a new one.** Before creating
   any file, grep for near-duplicates by title, filename, and key terms.

---

## Directory map

| Path | Contents | Who writes |
|---|---|---|
| `missions/` | The things being made. One folder per mission. | Owner |
| `missions/<name>/assets/` | Artifacts the mission produces — generator scripts, figures, decks. | Both |
| `missions/<name>/threads/` | Arguments in development. One question per file. | Owner |
| `notes/` | Atomic notes — one concept per file, her words. | Owner |
| `people/` | Thinkers. One file per person. | Owner (you may add backlinks) |
| `sources/` | Bibliographic catalog. One file per work. | You, then reviewed |
| `sources/_unverified/` | Extracted references pending verification. | You |
| `inbox/` | Unfiled capture and your proposals. | Both |
| `inbox/scans/` | Notebook photos awaiting transcription. | Owner |
| `raw/` | Verbatim exports. Immutable. | Owner |
| `library/` | PDFs and ebooks. **Gitignored** — present on disk, not in git. | Owner |
| `templates/` | File templates. Copy, don't improvise schemas. | Owner |

New top-level directories require asking first.

---

## Conventions

**Filenames.** kebab-case. Notes and people: concept or surname
(`ai-native-architecture.md`, `wolfram.md`). Sources: `author-year-shorttitle.md`
(`shannon-1948-mathematical-theory.md`).

**Frontmatter.** Every file has YAML frontmatter matching its template. Do not
add fields that aren't in the template without asking. Never silently drop a
field.

**Links.** Obsidian wikilinks: `[[ai-native-architecture]]`, `[[wolfram]]`. Every
new note links to at least one existing note. When you create a link, check the
target exists; if not, say so rather than creating a stub.

**People vs tags.** Thinkers go in the `people:` field and get a `people/` file.
`tags:` is for subjects only. Do not put a person's name in `tags:`.

**Tag vocabulary.** Controlled. The list lives in `sources/_tags.md`. Do not
coin a new tag without flagging it; reuse an existing one where possible.

**Language.** Some material is in Hebrew. Transcribe and quote Hebrew in
Hebrew. Never translate silently. Set `lang: he` in frontmatter where relevant.

**Quotes.** Verbatim text from a source is always in a blockquote, always with
a page or locator. Never blend a source's wording into a note's prose.

**Source provenance fields.** Every source carries three fields after `lang:`:

- `origin` — `own` (AI-Native Systems team, IBM Research), `joint` (collaboration
  with an outside group or external co-authors), `external` (everything else).
- `project` — the internal project name (`certus`, `nous`, `llm-d`, `blis`,
  `spotlights`, `kernels`, `ains`). Set only for `own` and `joint` sources; leave
  blank for `external`. **Important:** several sources sharing the same `project`
  value are parts of one body of work, not independent corroboration. A note or
  thread that rests entirely on a single project value should name that dependency
  explicitly rather than citing the sources as if they were independent.
- `clearance` — `public` (publishable) or `internal` (IBM Confidential / IBM
  Proprietary — do not quote slide text or internal figures in a public talk without
  checking).

---

## Missions currently active

- `missions/keynote/` — the keynote being developed. Catalog material and
  notes, then draft the keynote from it.

Tag work with `missions: [keynote]`.

---

## Standard workflows

Each has a slash command in `.claude/commands/`. Read the command file before
running it.

- `/triage-chat` — mine one exported conversation into proposals in `inbox/`.
- `/promote` — execute the decisions she marked in a reviewed triage file.
- `/verify-refs` — check `sources/_unverified/`, promote or flag.
- `/build-thread` — assess one thread across the whole repo; writes a memo only.
- `/review` — weekly health report: orphans, stale seeds, singleton tags,
  broken links, unverified sources, unfiled inbox items.

## Committing

Commit at the end of every run, one commit per workflow, message prefixed with
the command name (`triage-chat: 14 proposals from 2026-08 ains chats`).
Never amend or rewrite history. Never force-push.

## When unsure

Ask. A short question is cheaper than a hundred files filed under a schema she
didn't want.
