---
description: Weekly health report on the knowledge base
---

Read-only. Write the report to `inbox/review-<date>.md`. Change nothing else.

Report on:
- **Inbox** — items unfiled for more than 14 days.
- **Orphans** — notes with no inbound wikilinks.
- **Stale seeds** — `status: seed` not updated in 60 days.
- **Missing "why it matters"** — sources with that section empty.
- **Singleton tags** — tags used by exactly one file, with merge suggestions.
- **Broken links** — wikilinks pointing at files that don't exist.
- **Unverified** — count in `sources/_unverified/`, oldest first.
- **Collected but unused** — sources with no inbound links from any note.
- **Schema drift** — files whose frontmatter fields don't match their template.

Keep it under one screen. Rank by what's worth 20 minutes. Propose deletions;
never perform them.
