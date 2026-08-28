---
type: source
title: "Discovery Is Easy, Composition Is Hard"
citekey: batsoyol-2026-discovery-easy-composition-hard
authors: [Nara Batsoyol, Daniel Waddington, Michael Factor, Tamar Eilam, Fabio A. Oliveira]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/08/04/discovery-is-easy-composition-is-hard/
lang:
origin:      own
project:     certus
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [use-case]
missions: [keynote]

status: unread
added: 2026-08-13
---

## Why it matters to me
storage use case optimization.

## Notes

Claude: A controlled bake-off, and the most intellectually honest artifact in the corpus — it is the one place where our own framework does not win. Handle deliberately rather than by omission.

**Setup.** Seven LLM-driven optimizers given the same task: speed up the Certus cold-read path (peer-to-peer NVMe-to-GPU transfer on four drives, bypassing host DRAM). Baseline 8.86 GB/s against a 21.1 GB/s hardware ceiling — only 42% of achievable. Shared budget of $20 and a 5-hour wall clock. Every mutation built, benchmarked, and integrity-checked. All frameworks used Claude Sonnet 4-6 for code generation; Nous additionally used Opus 4-6 for hypothesis design.

The seven fall into three families: mutation-driven populations (OpenEvolve, AdaEvolve, EvoX), reflection-driven search (GEPA, K-Search), and repository-level agents (Nous, and an unstructured Coding Agent).

**The finding.** Six of seven improved on baseline, but five plateaued between 10.5–11.6 GB/s. Only the Coding Agent broke through, reaching **16.5 GB/s (+86%)**. The gap is named the **composition barrier**: useful changes look ineffective or harmful until the rest of the combination is present. The winning compound required fewer but deeper queues (L1+L3), a larger staging ring (L2), and batching to keep them fed (L5). On the baseline configuration, batching alone *reduces* throughput by 9.5%, and queue changes without batching yield only modest gains — so **no incremental ordering delivers continuous progress**. Exploration was not the hard part; every framework found pieces of the answer.

**Why each got stuck** is diagnosed per-framework: population tools deprioritized regressing candidates as parents before they could be combined; GEPA's diversity-weighted Pareto selection pulled mutations away from the single best-scoring candidate; K-Search found the correct structure (kept batching and the larger ring) but reverted L1 and L3 to seed values, never combining them. The Coding Agent's tree is sparse — 26 mutations — and reaches the highest point.

**Recoverability is identified as the differentiator.** The Coding Agent reverts only after *consecutive* regressions, letting one worse result persist long enough for a complementary change to pay off, then returning to the best-known state if the branch still fails. Retaining the best candidate in a pool is explicitly not enough — the search must reliably *resume* from it.

**Where Nous lands, stated precisely.** Under the $20 budget Nous completed only three experiments and did not reach the compound. In a separate **$65** run it reached the same compound independently at 16.3 GB/s, by an entirely different route: controlled experiments that reset each time, carrying forward extracted principles rather than a retained code state. The authors' reading is that the limitation in this setting was **budget rather than method**. Nous also produces an artifact the Coding Agent does not — an explicit set of learned principles accumulable into a reusable knowledge base.

Three design factors concluded: recoverability enables composition; composition comes from either volume (many cheap iterations) or targeting (few expensive experiments with upfront design deciding what each tests); guardrails make autonomous optimization safe (data-integrity checks catch silent corruption such as buffer reuse before an async transfer completes, and a hardware ceiling rejects impossible results).

Caveated by the authors as a single case study that cannot establish general conclusions. 22% of the hardware ceiling remains unclaimed and whether software can close it is left open. Versions pinned by commit, which is good practice worth mentioning if anyone asks about reproducibility.

<!-- TE: -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
