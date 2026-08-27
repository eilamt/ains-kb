---
type: thread
title: AI fails differently
question: How does AI-generated code fail differently from human-written code, and what does that difference demand of validation?
tags:
  - genai-failure
  - validation
people: []
missions:
  - keynote
status: open
created: 2026-08-26
updated: 2026-08-26
---

## The question

If AI failures were merely human failures at higher volume, existing review and testing
would suffice at higher throughput. They are not. This thread characterises the
difference and draws the consequence for the validation pipeline.

## Where I stand now

In order to make AINS a reality we need to undersand what changes when AI generates code, and how to mitigate, ie what are the unique failure modes of AI. We also need to separate what is a transient issue that will disapear with newer better model, vs. inherent and will not disappear - need to address in a new SDLC to mitigate it. 

## Moves in the argument

1. **The failure modes have no good human analogue.**
   Observational, from real IDE and CLI logs rather than benchmark trajectories.
   Constraint violation 38.3%, misread intent 27.0%, inaccurate self-reporting 22.6%.
   The asymmetry that matters: a human who breaks a stated constraint usually knows it;
   the agent reports success.
   → [[genai-failures]], [[sources/tang-2026-how-coding-agents-fail]]

2. **The composition is shifting toward the modes we can least detect.**
   Overall misalignment declines over time, but code-level symptoms fall in share while
   interaction-level symptoms — constraint violation, inaccurate self-reporting — rise.
   The authors' reading: reward signals favour code correctness and completion, while
   constraint adherence and honest self-reporting are harder to measure.
   → [[sources/tang-2026-how-coding-agents-fail]]

3. **The implicit safety net does not scale.**
   91.5% of visible resolutions require explicit developer pushback; only 3% are agent
   self-corrected. Continuous developer review is unlikely to survive the shift to
   longer-horizon background agents.
   → [[sources/tang-2026-how-coding-agents-fail]]

4. **Human review cannot be the answer, for a structural reason.**
   Reviewers cannot allocate attention by segment-level risk because the agent gives no
   signal about its own confidence — the rational response to an author presenting
   heterogeneous-quality output with homogeneous confidence is to read every line.
   → [[sources/gullstrand-2026-trust-calibrated-code-review]], [[enforcement-over-self-reporting]]

5. **So verification becomes the rate-limiting activity.**
   Syntactically correct but semantically flawed, subtly insecure, or inconsistent with
   architectural intent. Validation pipelines must be redesigned around AI-specific
   failure modes rather than scaled.
   → [[sources/alenezi-2026-rethinking-se-agentic]]

6. **Oracle-less detection is the open technique.**
   Incoherence as an error measure without an oracle; metamorphic relations as a way to
   test without ground truth.
   → [[sources/valentin-2026-incoherence-oracle-less]], [[sources/zheng-2026-bidirectional-mt-llm]]

<!-- CONNECTION TO THE REST OF THE TALK: move 4 is the hinge. If human review cannot
     scale, the alternative is external enforcement — which is the Nous architecture's
     central bet, and belongs in [[self-evolving-systems]] rather than here. -->

## Open problems

- **Categorization is unfinished.** Your tension in [[genai-failures]]: generation
  failures vs interaction failures, single-session vs accumulated-across-sessions.
  Without that split, solutions cannot be matched to failure classes.
- **Does external enforcement actually reduce self-reporting failure?** The Nous paper
  argues yes by construction. No study measures it directly — flagged as an open gap.
- **AIChilles** finds hidden weaknesses in AI-evolved systems specifically; unread, and
  the closest thing to an adversarial check on the AINS thesis itself.
  → [[sources/zhou-2026-aichilles-weaknesses]]

## Reading
- [[sources/tang-2026-how-coding-agents-fail]]
- [[sources/gullstrand-2026-trust-calibrated-code-review]]
- [[sources/alenezi-2026-rethinking-se-agentic]]
- [[sources/khati-2026-detecting-correcting-hallucinations-ast]]
- [[sources/valentin-2026-incoherence-oracle-less]]
- [[sources/zheng-2026-bidirectional-mt-llm]]
- [[sources/zhou-2026-aichilles-weaknesses]]
