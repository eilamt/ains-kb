---
type: note
title: why modularity is important
tags: [mdd]
people: []
missions: [keynote]
status: developing
created: 2026-08-11
updated: 2026-08-11
---

why modularity is important and what is the state of the field and open questions.

## Elaboration

Empirical studies show a contradiction: increased developer productivity but reduced code quality in the long run. Based on multiple measures such as DORA. There are multiple reasons for this. One key reason is that AI context window is limited, it may make inconsistence changes in different parts of the code because it cant hold the big picture, another reason is that it prioritises expediency, a known issue is hallucination, from a human prespective, the code becomes complex they do not understand it, and they are trusting the AI too much.

## Tensions

the AI code which is generated is NOT modular, it increases in complexity. But what we need is modularity for multiple reasons: reduce context, control scope, have readable code, that is easier to continue to evolve and maintain. Modularity is more important, not less important because of AI.

## Connects to
- [[sources/meng-jackson-2025-legible-software]]
- [[sources/he-miller-2026-speed-cost-quality]]
- [[sources/cervantes-kazman-2026-llm-architecture-code-generation]]

## Provenance

provenance: raw/claude-exports/2026-08-26-keynote-scoping.md

*From candidate 1 — Certus as existence proof:*

> Certus is a hyper-specialized storage system for KV Cache. Small team of 4
> developed 69K SLOCs of Rust code in less than 5 months. Zero lines of code
> hand-written – Spec Driven Development. Focus on assurance and
> human-maintainability.

— `Certus_Review_Priya_JUL2026.pptx`, slide 3

> Component-based composition solves a practical problem in system synthesis:
> generating correct, efficient low-level code from high-level descriptions is
> hard. [...] This means that the coding agent's inferencing context can be
> limited to a system-wide view that abstracts over the details of internal
> component implementations.

— `waddington-2026-certus-storage`, §5.2

> ery similar to approach in Certus but goes a step further with the
> synchronization service (but specification can be limiting)

— already in `sources/meng-jackson-2025-legible-software` (pre-dates this conversation; no export pointer)

> agreed. The Certus use case addresses many of the issues identified by
> literature. It is an exemplar of the emerging SDLC.

— Tamar, on review of triage `triage-2026-08-26-certus-modularity-sdlc-2.md`

*From candidate 4 — mechanism and evidence for modularity as a precondition for machine reasoning:*

> By generating compositions of proven components rather than raw code, Certus
> inherits the correctness and performance properties of the component library.

— `waddington-2026-certus-storage`, §5.2

> The key insight behind Prometheus is that complex programs can be made more
> amenable to AI-based automated reasoning by first transforming them into
> semantically equivalent, modular components.

— `wang-2025-prometheus-dissect-restore`

> indeed, and very important to note that modularity is important for multiple
> reasons.. and human readability is only one reason

— Tamar, on review of triage `triage-2026-08-26-certus-modularity-sdlc-2.md`
