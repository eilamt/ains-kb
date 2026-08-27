---
type: note
title: when code is cheap, specialization becomes the default
tags: [use-case, sdd, sdlc]
people: []
missions: [keynote]
status: seed
created: 2026-08-27
updated: 2026-08-27
---
<!-- TODO: state this idea in one sentence, your words.
     Your own framing from the thread question is close already: "an opportunity opens
     when code is cheap: hyper-specialization." -->

## Elaboration
<!-- DRAFT — cut to house style. -->

Specialized systems have always outperformed general-purpose ones — the evidence spans
decades and orders of magnitude, from SSD-aware key-value separation to flash-optimized
filesystems to domain-specific compilers. The question was never whether specialization
works. It was whether anyone could afford it: building a production storage engine is
expensive, maintaining it across hardware generations more so, and re-specializing it
as the workload shifts more so again. That cost creates a forcing function toward
generality, and the result is a landscape where everyone runs a handful of
general-purpose systems regardless of fit.

What changes is not that generation is faster. It is that program synthesis decouples
the cost of *building* a system from the cost of *specializing* it. Once the generator
exists, a new variant costs about what modifying a specification costs. The economics
that made specialization a luxury stop holding.

## Tensions
<!-- What complicates this? What would a serious objector say? -->

**Fragmentation is the price.** A separate specialized variant per deployment is a
separate artifact to review, support, and reason about. The vision post names this and
does not resolve it: hyper-specialization becomes feasible precisely when human effort
stops being the constraint, which is also when the number of distinct artifacts stops
being bounded by anything.

**It requires a stable workload.** The clearer and more stable the profile, the more
aggressively the generator can specialize — so workloads that shift faster than the
spec can be regenerated fall outside. Which workloads those are is an open question.

**Versioning is unsolved.** How generated systems should be versioned as workloads
drift is named as an open question by the authors themselves.

**One data point.** Certus is a single case on a workload chosen for being both
important and analytically tractable.

## Connects to
- [[why-modularity-is-important]]
- [[specification-as-the-durable-artifact]]
- [[sources/waddington-2026-certus-storage]]
- [[sources/anon-2026-certus-review]]
- [[sources/eilam-2026-ai-native-systems-autonomous-evolution]]

## Provenance
<!-- Claude assembly from material already in the KB; no new source read. -->

> The central wager of Certus: if you can generate a specialized storage system rather
> than build one by hand, the economics of specialization change entirely.

— `Certus__Blog_June_2026.pdf` §2

> program synthesis decouples the cost of building a system from the cost of
> specializing it. Once the generator exists, producing a new specialized variant
> costs approximately as much as modifying a specification—not as much as writing its
> implementation.

— `Certus__Blog_June_2026.pdf` §5.1
