---
type: thread
title: Two communities, opposite conclusions
question: <DRAFT — replace with your thesis in one line> Why do the systems/ML community and the software-engineering community reach opposite conclusions about AI writing code, and which of them is the audience in this room?
tags: [sdlc, harness, genai-failure]
people: []
missions: [keynote]
status: open
created: 2026-08-27
updated: 2026-08-27
---

## The question

The Outline's section 2 sets promising academic results against open gaps, and labels
the two camps. This thread is the argument behind that slide: two literatures, two
conclusions, almost no citation between them — and a systems audience that has read
only one of them.

## Where I stand now
<!-- TODO: your position, in your words. Date each rewrite.
     Note the Outline already contains a stance — "maybe too optimistic?" — which is
     a claim you would be making about the room you are standing in. Decide how far
     to press it. -->

## Moves in the argument

1. **One literature says AI is upending systems research.**
   The title is the thesis. ADRS framing; the Berkeley Sky Lab cluster builds on it.
   → [[sources/cheng-2025-barbarians-at-the-gate]]

2. **It has real results behind it.**
   AlphaEvolve for algorithmic discovery; Glia and Engram for systems design and
   optimization; SkyDiscover, AdaEvolve, EvoX as a framework family.
   → [[sources/novikov-2025-alphaevolve]], [[sources/hamadanian-2026-glia]],
     [[sources/karimi-2026-engram]], [[sources/liu-2026-skydiscover]]

3. **The other literature measures the same technology and finds degradation.**
   Complexity up 41.6% and persistent; code smells compounding at volume; comprehension
   debt invisible to tooling; failure modes with no human analogue.
   → [[the-productivity-paradox]], [[genai-failures]]

4. **They are not arguing with each other — they are measuring different things.**
   The optimistic literature evaluates *discovery*: can a search loop find a better
   artifact than the human baseline, scored against a fixed benchmark. The pessimistic
   literature evaluates *maintenance*: what happens to a codebase and a team over
   months of assisted authorship. Both can be right.

5. **The unit of analysis is the actual disagreement.**
   Per-task and per-benchmark against per-codebase and per-team over time. Neither
   community's instrument can see the other's finding.

6. **Which is why the AINS position is not a compromise between them.**
   If degradation is a property of the human-mediated loop — code produced faster than
   it can be understood, reviewed without a confidence signal — then making AI the
   primary agent is not more of the thing that caused the problem. That claim is
   load-bearing and is argued in [[the-new-sdlc]].

<!-- POSITIONING: this thread decides how the talk treats its own audience. A systems
     conference is the optimistic community. Presenting the SE evidence as a
     corrective is the whole value of the beat — and also the thing most likely to
     land badly if it reads as a rebuke. -->

## Open problems

- **Our own bake-off is evidence against the optimistic framing, and it tests this
  group's tools by name.** AdaEvolve, EvoX, GEPA, K-Search reached only +19–31% and
  plateaued on the Certus cold-read path. That is a genuine receipt, and it puts a
  Berkeley-vs-IBM frame on stage. Decide whether to use it.
  → [[sources/batsoyol-2026-discovery-easy-composition-hard]]
- **Engram is subsumed by the L2 baseline** in the NOUS evaluation, so the L2 → NOUS
  delta is effectively our measured margin over it. If that characterisation is
  contested, RQ3 is at stake. → [[sources/karimi-2026-engram]]
- **Glia is cited but not compared against.** The obvious question from this audience.
- **All five sources above are unverified stubs.** Nothing has been read from the
  works themselves. This thread cannot be presented until they are.
- **The Haifa validation work** named in the Outline ("check with Paula") is not
  catalogued at all.

## Reading
- [[sources/cheng-2025-barbarians-at-the-gate]]
- [[sources/karimi-2026-engram]]
- [[sources/hamadanian-2026-glia]]
- [[sources/novikov-2025-alphaevolve]]
- [[sources/liu-2026-skydiscover]]
- [[sources/hassan-2025-ai-native-se-30]]
- [[sources/batsoyol-2026-discovery-easy-composition-hard]]
