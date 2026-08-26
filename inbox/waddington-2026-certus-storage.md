---
type: source
title: "Certus: The End of One-Size-Fits-All Storage"
citekey: waddington-2026-certus-storage
authors: [Daniel Waddington, Michael Factor, Nara Batsoyol]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/06/17/certus-the-end-of-one-size-fits-all-storage/
lang:

verified: true
holdings: [link, pdf]
file: Certus__Blog_June_2026.pdf

people: []
tags: [use-case, sdlc]
missions: [keynote]

status: unread
added: 2026-08-13
---

## Why it matters to me
storage use case.

## Notes

Claude: The hyper-specialization thesis made concrete, and the most methodologically dense of the blog posts. The wager is stated explicitly: "if you can *generate* a specialized storage system rather than build one by hand, the economics of specialization change entirely." Historically specialization worked but was unaffordable; the forcing function toward generality is the cost of building storage engines at all.

**Why KV-cache is the chosen target.** The workload profile is hostile to general-purpose storage in six specific ways, and each one is an axis of specialization: 64-bit fixed-length keys (no need for string naming or hierarchical directories); write-once then read-many (4–5 MiB tensor blobs written in one burst at end of pre-fill, never modified); relaxed durability (lost entries are recomputable, so long as loss is *detected* — this opens design space closed to general stores); latency-sensitive reads (a miss stalls inference); fixed, predictable object sizes known at *system generation time*; and highly skewed access from shared prompt prefixes, making prefetch viable.

**Four interlocking techniques.**
1. *Spec-driven development* using Spec Kit. Specifications are the primary artifact, not scaffolding, and can be back-filled when code changes outside the flow. The structural claim, which matters more than the productivity claim: program synthesis **decouples the cost of building a system from the cost of specializing it**. Once the generator exists, a new variant costs about as much as modifying a specification.
2. *Component-based composition.* Each component exposes a typed **interface** plus one or more **receptacles** — required interfaces other components must satisfy. Generating compositions of proven components rather than raw code inherits their correctness and performance properties, and — the point that connects directly to the modularity argument — it **limits the coding agent's inference context to a system-wide view that abstracts over internal component implementations**. On evaluation failure, synthesis is re-invoked with the failure report plus the original spec.
3. *Synthesized formal verification.* Verification artifacts are generated alongside the implementation by a dedicated verification agent working from the same specification. Three tools form a **pipeline, not alternatives**: Spin (concurrency and protocol — no deadlock or livelock across interleavings), Kani (bit-precise model checking of the synthesized Rust against low-level safety properties), Creusot (deductive verification of core algorithms against their functional specs). The claim this licenses is the sharpest inversion in the whole corpus: a generated system carrying certificates at all three levels is *more* trustworthy than a hand-written system with none. That answers the opacity objection head-on rather than deflecting it.
4. *Evolutionary optimization* over the performance-critical code inside established interface contracts — buffer management, I/O scheduling, concurrency patterns, memory hierarchy — where the optimum depends on hardware topology and workload and cannot be derived analytically. Two guardrails prune infeasible candidates before evaluation: **API surface extraction** (scan target files for exact `use` paths and `pub fn` signatures so generated code cannot reference hallucinated symbols) and **hardware profiling** (inject measured NVMe bandwidth, PCIe topology, memory budgets so candidates exceeding physical limits are rejected).

**Results.** Block-device component selection: SPDK back-ends dominate cold reads at 10.9 GB/s vs 5.6 GB/s for a single kernel device, while writes and hot lookups are comparable — component selection differentiates only where the workload stresses that path. End-to-end against XFS on software RAID-0: writes **18.3x throughput (10.3 vs 0.56 GB/s) at 9x lower tail latency**, hot lookups 1.9x, cold reads 2.6x, each at roughly half the p99. The write gap is explained mechanically — the filesystem path pays per-object inode metadata, extra memory copies, WAL journaling, and fine-grained allocation that Certus bypasses via zero-copy DMA from GPU VRAM to NVMe.

**Hardware adaptability as the strategic argument.** Conventional adaptation to new hardware means identifying embedded performance assumptions, understanding how new hardware invalidates them, redesigning, re-implementing, re-testing, and validating no regression — years for a mature system, which is why new hardware capability goes unadopted. In Certus, an agent extracts hardware characteristics, the spec is updated, and the evolutionary layer re-optimizes. "A new specialized system emerges in days, not years."

Open questions the authors flag themselves: how far the component vocabulary scales, how generated systems should be versioned as workloads shift, and which workloads are too dynamic for a static spec.

<!-- TE: -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
