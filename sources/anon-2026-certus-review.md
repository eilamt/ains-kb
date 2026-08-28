---
type: source
title: "Certus Review"
citekey: anon-2026-certus-review
authors: []
year: 2026
kind: talk
container: "Internal IBM review — marked IBM PROPRIETARY"
publisher:
doi:
url:
lang:
origin:      own
project:     certus
clearance:   internal

verified: true
holdings: [pdf]
file: Certus_Review_Priya_JUL2026.pptx

people: []
tags: [use-case, sdd, verification, harness]
missions: [keynote]

status: read
added: 2026-08-13
---

## Why it matters to me
certus.

## Notes

Claude: 39 slides, presented by Daniel Waddington and Nara Batsoyol, dated 7/31/26. **Every slide is marked IBM PROPRIETARY** — the productivity figures and the head-to-head framework comparison in particular are internal. Flagging so nothing lands on a public keynote slide by accident.

This deck carries substantially more than the Certus blog post, and in two places it contradicts it.

**The headline numbers, which are not in the blog.** A team of **4 people produced 69K SLOC of Rust in under 5 months with zero lines hand-written** — 100% spec-driven synthesis. Claimed ~10× productivity against comparable projects with similar teams, with the caveat on the slide that "gains could be higher since this data includes the learning process."

**Number to be careful with.** The deck's headline is **3× over a generalized solution end-to-end**; the blog's headline is 18.3× on writes, 1.9× hot lookups, 2.6× cold. These are different measurements, not different roundings. The blog figures are a component microbenchmark (4 MiB blocks, 672 objects, XFS on RAID-0). The deck's 3× is an end-to-end vLLM deployment: 450 conversations, 12 turns, ShareGPT replay, Llama-3-8B, single node, A100, PCIe 4.0, 64 GB DRAM limit. The deck also notes this is "manual-iterative optimization only" — the full workbench flow has not been applied yet. Quoting 18.3× as an end-to-end system result would be wrong.

**System Workbench** is the bigger idea here and it is absent from the blog entirely. Eight agents across the lifecycle — Inspection (profiles hardware and workload), Design (chooses architecture, drafts spec), Specialization (synthesize + compose), Optimization, Assurance (proves invariants), Deployment, Knowledge (mines outside literature in, writes confirmed results back), Security (scans everything emitted for unsafe code, secrets, vulnerabilities, and gates what ships) — plus a Meta-Agent outer loop that "evolves the agents themselves." The slides honestly mark which are built, partly built, and to-be-built. Three durable artifacts carry forward: the Spec (constitution, requirements, success criteria), the Hardware Profile, and the Optimization Pattern Library. The framing line is good: "Certus is the first target; a system built this way carries its spec, proofs and measurements forward" — what transfers is not the code but the pattern library and workbench.

Note the spec vocabulary: **constitution, user stories, functional requirements, success criteria, assumptions, research.** The constitution slide is a concrete instance of the governed-autonomy concept from the vision post — an actual artifact, not a metaphor.

**The Optimization Agent is a distinct system from Nous** and this deck is its main documentation. Footnote on slide 10: "Compared to Nous, the Optimization agent is specialized for system code." Its argument for why systems-code optimization is different: the search space is large and highly coupled; good optimizations look like regressions in isolation; changes interact so you cannot tune independently; layers mask each other. Its answer is **search-space narrowing before generation** — "Existing tools: generate first, evaluate later. Our agent: understand first, then generate."

Mechanism: a Bootstrap phase builds a **knowledge graph** — nodes are changeable things (parameters, hard-coded caps, sync points, algorithm choices, buffer ownership) plus *missing capabilities*; edges are `caps`, `couples`, `enables`, and couples-edges carry the formula rather than just an arrow. Four inputs shape every proposal: code that actually runs (traced benchmark → source), the pattern library, the system model (what's blocked), and this run's memory (what's been tried). A deterministic controller with **9 modes** decides whose hypothesis runs next, escalates on evidence, opens a bottleneck-discovery mode when it needs a new hypothesis, and stops at a validated ceiling. Outcomes are typed: confirmed / refuted / inconclusive / **quarantined**. An `Assess` step applies a "measurement contract" — data-origin, ceiling, plausibility, coldness invariants, plus a harness-untampered check.

**Internal inconsistency to resolve before quoting.** Slide 10 says the pattern library holds **122** patterns from literature; slides 15 and 19 say **118**. Slide 14 says they were distilled from **477 systems papers**. Pick one and check it.

**The bake-off backup slides (26–27) are materially different from the published blog, and more damaging.** The blog reports the Coding Agent hitting 16.5 GB/s under a $20 budget with a sparse 26-mutation tree, and Nous reaching 16.3 GB/s in a separate $65 run. The deck reports:

| Approach | Result | Cost | Repeatable? |
|---|---|---|---|
| Optimization Agent | +86% | $2.69 | Yes |
| Coding Agent (trial & error) | +86% | $12, 152 iterations | Depends on budget |
| Nous (scientific method) | +84% | $65, 10 iterations | Yes, but depends on budget |
| OpenEvolve / AdaEvolve / EvoX | +19–31% | $20 ea | Stuck |
| GEPA / K-Search | +23–25% | $20 ea | Stuck |

So the new Optimization Agent matches the Coding Agent's result at roughly a fifth the cost and a fraction of the iterations, and beats Nous on both cost and outcome on this task. The deck's own conclusion — "The model isn't the bottleneck — the structure around it is. All tools used the same AI" — is the right lesson, but note it is being used to argue for a *different* structure than Nous's. If the keynote presents Nous as the answer, this deck is the internal counter-evidence, and someone in the room may have seen it.

One detail from the speaker notes worth keeping: in the run that reached ~16 GB/s, **auto-revert fired 32 times.** That is the recoverability finding quantified.

**Slide 16, "Key Highlights of Our Experience," is the most valuable slide in the deck for a research keynote.** Five honest findings:
- It is easy to lose a mental model of the system and accumulate technical debt — countered by holistically generated specs and architectural artifacts coupled to a component-based architecture.
- **LLM bias**: trained on massive public code, so "popular, well-documented patterns are overrepresented relative to niche-but-superior ones." A real limitation for a discovery system and not one I have seen stated elsewhere in this corpus.
- Design exploration is very different from algorithm optimization — you must understand the system before optimizing it, and hardware-derived guardrails help.
- **Overfitting to the tests**: bug fixing and refactoring guided by unit, integration, and performance tests will happily overfit to those tests.
- **The self-proving problem**: using GenAI to apply formal verification has potential, but proving the chain-of-transformation correctness — spec → code properties → abstract code → proofs/test harness — is tricky, and "it's sort of self-proving." Their proposed mitigation is an adversarial alternative LLM (Codex) attacking the chain. This is the honest version of the blog's much bolder claim that generated code with three certificates is more trustworthy than hand-written code with none. Both are defensible; they should not be stated in the same talk without acknowledging the tension.

The speaker note under that slide states the discipline plainly: since they cannot validate against every deployment, each generated component and optimization is recorded with its preconditions and contraindications — "so it travels with its conditions rather than as a general claim."

Also here and not in the blog: Kani, Creusot, and Spin each get a worked example slide (the Kani one catches a real `base + offset` u32 overflow and proves the fix across all 2³² inputs), the current architecture's seven key features including lazy write-through and RDMA remote peers via Zyre discovery, an optimization landscape table keyed on lifetime / reusability / size / heterogeneity / failure sensitivity / access predictability, and next steps naming 8×H200 + 8×NVMe testing and comparison against 3FS and Mooncake.

See [[notes/the-self-proving-problem]], [[notes/why-modularity-is-important]].

## Quotes
<!-- Always blockquoted, always with a locator. -->
