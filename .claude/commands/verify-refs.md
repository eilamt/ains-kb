---
description: Verify extracted references and promote the real ones
---

For each file in `sources/_unverified/`:

1. Search for the work. Confirm author, title, year, and publisher/container
   against a real record.
2. If confirmed: fill in the frontmatter, set `verified: true`, move to
   `sources/`, filename `author-year-shorttitle.md`.
3. If not found or details conflict: leave it in place, set
   `verified: false`, and add a `## Verification` section stating exactly what
   you searched and what you found. Do not guess.
4. If it appears to be fabricated (no trace of the work exists), move it to
   `sources/_unverified/suspect/` and list it prominently in your report.

Report: promoted / unresolved / suspect, with counts. Commit as
`verify-refs: N promoted, M suspect`.

Never fill a bibliographic field from memory. If you did not read it in a
search result, it stays empty.
