---
type: thread
title: Self-evolving systems — llm-d
question: can AI be the primary agent in constructing and evolving systems, and what is the opportunity space that opens? can a deployed system observe its own behaviour, hypothesize improvements, validate them, and ship them without a human in the loop for each one?
tags:
  - use-case
  - ains-concept
  - harness
  - validation
people: []
missions:
  - keynote
status: open
created: 2026-08-26
updated: 2026-08-26
---

## The question

The horizontal half of the talk. Certus produces a system that does not yet exist;
this thread evolves one that does — brownfield, telemetry-driven, changes going upstream.

## Where I stand now
<!-- TODO: your position, in your words. Date each rewrite. -->

## Moves in the argument

1. **The human-mediated loop is the bottleneck, and it biases toward reactive change.**
   When nothing appears broken, latent inefficiency persists because no alert fired.
   → [[sources/eilam-2026-ai-native-systems-autonomous-evolution]] §1

2. **Closing the loop needs cheap validation, or it cannot run.**
   A 30-minute GPU evaluation becomes seconds on CPU. The load-bearing claim is that
   simulation fidelity matters less than simulation *speed* — the simulator need not
   predict absolute latency, only rank algorithms correctly.
   → [[sources/guhathakurta-2026-why-simulate-before-scale]],
     [[sources/guhathakurta-2026-blis-inference-simulation]]

3. **And that ranking claim is independently evidenced.**
   Fit once on H100, 6.7% median end-to-end error on six models across three GPU types
   it never saw, ~200× faster than running them.
   → [[sources/guhathakurta-2026-modeling-llm-latency]]

4. **Structure, not capability, is what makes the agent an investigator.**
   Multi-arm hypothesis bundles, prediction-error taxonomy, principles that constrain
   the next iteration, and — the central bet — compliance verified externally by schema
   validation rather than self-reported. This is the direct answer to move 4 of
   [[ai-failure-modes]].
   → [[sources/anon-2027-nous-scientific-experimentation]], [[enforcement-over-self-reporting]]

5. **It produced upstream contributions, twice.**
   Probabilistic admitter: 37–98% P90 TTFT reduction for critical requests, validated on
   a real H100 cluster, merged into llm-d. Soft-reflective ceiling: proportional gating,
   no free parameters, merged.
   → [[sources/chen-2026-simulation-production-admission-controller]],
     [[sources/kalantar-2026-simulation-production-flow-control]]

6. **The gains are not just a better model, and not just more compute.**
   L0 43.1 → L1 55.0 → L2 68.5 → NOUS 92.8 on a 110-point rubric, independently judged.
   Cost parity with L2 ($28.96 vs $29.82). Re-run on a stronger model every baseline
   improves and NOUS still leads every campaign by +8.3.
   → [[sources/anon-2027-nous-scientific-experimentation]] RQ3

7. **Refutations are outputs, not failures.**
   Throttling SSD transfers added 83.8 ms for all tenants — preventing an incorrect
   production recommendation. A fairness principle refuted with a direction error when
   arrivals turn bursty.
   → [[sources/anon-2027-nous-scientific-experimentation]] campaigns 12–13

8. **Someone still has to say where to look.**
   Every execution-layer tool, Nous included, requires a human to point. Spotlights is
   the selection layer.
   → [[sources/anon-2026-spotlights-overview]]

## Open problems

- **The honest negative.** Campaign 16: −54% critical TTFT under saturation, but
  +66–132% harm in a near-saturation band invisible to the simulator. The blog reports
  the same regression at +18/+31%. Reconcile before quoting either.
- **Autonomy level.** Gates are optional with an automated-approval mode. Be precise
  about which mode produced which result.
- **Which principles survive.** The paper describes update-and-prune, not append-only.
  Decide what is claimed on stage.
- **Terminology.** Hassan's SE 3.0 already owns "AI-Native SE."
  → [[sources/hassan-2025-ai-native-se-30]]
- **Where the loop's limits are.** Requires a programmatic interface and quantitative
  outcomes; correctness and security properties fall outside the current schema.

## Reading
- [[sources/eilam-2026-ai-native-systems-autonomous-evolution]]
- [[sources/anon-2026-ai-native-systems-six-months]]
- [[sources/anon-2027-nous-scientific-experimentation]]
- [[sources/chen-2026-simulation-production-admission-controller]]
- [[sources/kalantar-2026-simulation-production-flow-control]]
- [[sources/anon-2026-spotlights-overview]]
- [[sources/anon-2026-residency-memory-llm-serving]]
