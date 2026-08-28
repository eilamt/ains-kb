---
type: source
title: "The Scientific Method on Code: How a Hypothesis-Driven AI Learned What Evolution Couldn't"
citekey: eilam-2026-scientific-method-on-code
authors: [Tamar Eilam]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/06/24/the-scientific-method-on-code-how-a-hypothesis-driven-ai-learned-what-evolution-couldnt/
lang:
origin:      own
project:     nous
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
<!-- One or two sentences, your words. Written for you-in-six-months.
     If you can't write this, it's not catalogued yet. -->

## Notes

Graph coloring use case. Compares OpenEvolve (evolutionary, plateaued at DSatur 1979) vs Nous (hypothesis-driven, scientific method). Nous progressed from DSatur -> RLF -> TabuCol, improving benchmark score from 0.8934 to 0.9690 over four iterations.

Claude: Fuller detail from the published text, for keynote use.

Benchmark: 22 DIMACS graphs with known chromatic numbers — seven queen, four Mycielski, four "book" graphs from character co-occurrence in novels, two US-city distance graphs, one college-football schedule, three register-allocation graphs from real compilers, one large Leighton graph. Score is a weighted combination of coloring quality (distance from chi) and speed. Campaign ran four iterations in May 2026, Opus 4.5 for design and Sonnet for execution, **total spend $17.21 across ten model calls** ($11.85 on six Opus design calls, $5.37 on four Sonnet execute-analyze calls). That number is unusually persuasive to a systems audience and is worth a slide on its own.

Score progression: 0.8934 naive greedy -> 0.9384 DSatur -> 0.9556 (multi-start RLF, found by the *robustness arm*, not h-main) -> 0.9615 -> 0.9690 (RLF + TabuCol, tenure=11).

**The two strongest talking points are both about the AI initiating, not executing.** At Iteration 2 the Planner proposed the shift from vertex-level to color-class-level construction (RLF) on its own; at Iteration 4 it proposed abandoning construction heuristics entirely for conflict-repair local search (TabuCol) after reading its own accumulated principles and concluding construction was exhausted. Neither was suggested by a human — the human role at the design gate was approve/reject only. The Planner also did its own literature search and named Brelaz 1979, Leighton 1979, and Hertz & de Werra 1987 itself.

Mechanism findings that show the arms doing real work:
- Iter 1 ablation (Largest-First, +0.0171) vs h-main (DSatur, +0.0450) isolated *dynamic saturation tracking*, not merely informed ordering, as the mechanism. The negative control (random ordering, +0.0166) revealed the DIMACS natural order is itself adversarial — quantified as ~37% of DSatur's gain coming from simply not using the original order, ~63% from the saturation signal.
- Iter 2 ablation removed block-counting from RLF and scored *below* DSatur (0.9249 vs 0.9384) — block-counting is the entire mechanism, not an optimization. Super-additivity arm showed a DSatur+RLF ensemble identical to RLF alone on all 22 graphs; RLF uniformly dominated, so DSatur was retired.
- Iter 3 robustness arm produced a **refutation**: uniform K=4 captured *none* of the multi-start gain (0.9556, identical to baseline). The gain is discontinuous with a K=6 threshold for small graphs — a sharp threshold the post argues would be invisible to a mutation-based approach.
- Iter 4 robustness arm beat its own h-main: tenure=11 (0.9690) against the classical Hertz & de Werra recommendation of 7 (0.9659).

RP-13 is the best single illustration of the principle schema's `applicability-bounds` field. Kempe-chain post-processing yielded zero improvement on all 22 graphs, but the recorded principle is scoped to the *restricted* variant actually run (smallest color class only, skipped if that class held more than n/4 of vertices, required a single absorbing color, stopped at first failed pass) and explicitly does not rule out Kempe on DSatur output, iterated Kempe on class pairs, or TabuCol/annealing.

**The confound is stated openly and should be stated openly on stage too:** Nous ran on Opus 4.5 + Sonnet; OpenEvolve ran on Gemini 2.0 Flash (free tier) with Sonnet 4.5 optional. No Opus drove OpenEvolve. The argument for the framework effect surviving the confound is structural rather than statistical — a stronger model produces better individual proposals but does not create a mechanism for ruling out dead ends or for pivoting mechanism class after three iterations. "No equivalent of RP-13 is possible in a mutation-based system, because there's nowhere to store 'we checked this; it doesn't help here.'"

Honest limitation, stated in the post: le450_15c went 30 -> 23 -> 22 against chi=15, while specialized solvers reach 15-16 without enormous effort. And the campaign did not produce new algorithms — all three were known. What it produced was the experimental determination of *which mechanisms matter on this workload and how to tune them*.

<!-- TE: -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
