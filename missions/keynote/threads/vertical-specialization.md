---
type: thread
title: Vertical specialization — Certus
question: "An opportunity opens when code is cheap:  hyper-specialization. when do we hyper specializes why and how."
tags:
  - use-case
  - sdd
  - verification
people: []
missions:
  - keynote
status: open
created: 2026-08-26
updated: 2026-08-26
---

## The question

Certus as exemplar of the new SDLC — composition and verification, not optimization
search. The deep-dive that makes the lifecycle argument concrete.

## Where I stand now

Certus examplar of two things: the concept and opportunity of domain specificity ie hyper specializations, but also how it is complex to implement a new complex system from scratch with AI as the primary agent, and how we needed to change the SDLC to address these issues. 

## Moves in the argument

1. **Specialization has always worked; it has never been affordable.**
   Twelve documented cases of software-only gains on identical hardware — WiscKey
   2.5–111×, SPDK 2–10× IOPS, ClickHouse 10–100×, LP solvers ~1000×. The barrier was
   rare combinations of domain, systems, and hardware expertise.
   → [[sources/waddington-2026-certus-storage]] Table 1 (PDF version only)

2. **Program synthesis decouples the cost of building from the cost of specializing.**
   Once the generator exists, a new variant costs about what modifying a specification
   costs. That is the structural claim; the productivity number is secondary.
   → [[sources/waddington-2026-certus-storage]] §5.1

3. **It was actually done.** 69K SLOC of Rust, four people, under five months, zero
   lines hand-written.
   → [[sources/anon-2026-certus-review]] slide 3

4. **Composition is what keeps it from degrading.**
   Typed interfaces and receptacles; generating compositions of proven components rather
   than raw code inherits their properties, and bounds the agent's context to a
   system-wide view.
   → [[why-modularity-is-important]], [[sources/waddington-2026-certus-storage]] §5.2

5. **Verification is generated alongside the code, from the same spec.**
   Four channels routed by property type: (A) functional correctness — abstract code for Creusot; (B) bounded model checking — instrumented harnesses for Kani and Loom; (C) concurrency — a Promela model for Spin; (D) targeted runtime tests where proof is out of reach.
   → [[sources/anon-2026-certus-review]] slides 20–23, [[sources/waddington-2026-holding-wild-elephant]] §3.5

6. **Which inverts the usual objection.** A generated system carrying certificates at
   three levels is more trustworthy than a hand-written system carrying none.
   → [[sources/waddington-2026-certus-storage]] §5.3

7. **But the chain is self-proving, and this must be said aloud.**
   → [[the-self-proving-problem]], [[sources/waddington-2026-holding-wild-elephant]] §3.5.1

<!-- SCOPE DECISION (2026-08-26): the optimization half of Certus — Optimization Agent,
     knowledge graph, pattern library, the seven-framework bake-off — is OUT. Certus is
     the composition-and-verification story. Do not reintroduce
     [[sources/batsoyol-2026-discovery-easy-composition-hard]] here. -->

## Open problems

- **The self-proving chain.** Spec, code, and proof from one source certifies agreement,
  not correctness. Adversarial cross-checking by a different agent (Codex) is now
  implemented and validated by systematic poisoning; it narrows the problem without
  dissolving it — the cross-checker is still a language model.
- **Two different headline numbers.** 18.3× writes is a component microbenchmark; 3× is
  end-to-end vLLM. They are not interchangeable. → [[sources/anon-2026-certus-review]]
- **LLM bias toward well-documented patterns** over niche-but-superior ones — a real
  limitation for a synthesis system.
- **Overfitting to the tests** that guide bug-fixing and refactoring.
- **How far does the component vocabulary scale**, and which workloads are too dynamic
  for a static spec?


## Reading
- [[sources/waddington-2026-holding-wild-elephant]]
- [[sources/waddington-2026-certus-storage]]
- [[sources/anon-2026-certus-review]]
- [[sources/meng-jackson-2025-legible-software]]
- [[sources/wang-2025-prometheus-dissect-restore]]
- [[sources/ye-2025-verina-verifiable-code-generation]]
- [[sources/bursuc-2025-vericoding-benchmark]]
- [[sources/dolcetti-iotti-2025-dual-perspective-llm-verification]]
