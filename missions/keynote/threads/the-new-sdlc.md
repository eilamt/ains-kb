---
type: thread
title: The new SDLC
question: How do we need to reinvent the lifecycle to get to the vision of AINS is EFFECTIVE collaboration with AI, increase productivity for real over time, and get quality results
tags:
  - sdlc
  - sdd
  - mdd
people: []
missions:
  - keynote
status: open
created: 2026-08-26
updated: 2026-08-26
---

## The question

The lifecycle beat of the talk: intent → model → code → validation/verification →
production, with back-arrows and human-AI collaboration marked. This thread establishes
why the arrows point that way and what governs the back-arrows.

## Where I stand now

The issues identified (productivity pradox, ai failure modes) is not an argument to abandon the mission, rather it requires us to think deeper about how we collaborate with AI, what new techniques need to be invented (such as validation / verification) and transform the SDLC accordingly. 

## Moves in the argument

1. **Automating code production does not automate software engineering.**
   Naur's theory-building: the durable asset is the shared mental model, not the source
   text, and it decays when the people leave. Brooks on essential vs accidental
   complexity underwrites the same point.
   → [[sources/alenezi-2026-human-ai-collaboration-se]]

2. **So the specification has to become the authoritative artifact.**
   → [[specification-as-the-durable-artifact]] — and your position that this is not a
   process preference but the only way the theory survives machine-speed churn.

3. **Greenfield and brownfield differ only in what comes first.**
   Your own resolution: code and spec co-evolve and must always be kept in sync; the
   question is epistemological. In brownfield the code came first and the spec is
   reverse-engineered as a bootstrap. Cito and Bork argue exactly that direction —
   models as post-hoc artifacts recovered by reverse engineering.
   → [[specification-as-the-durable-artifact]], [[sources/cito-bork-2025-lost-in-code-generation]]

4. **Modularity is the precondition, not a style preference.**
   Bounded modules are how the agent's context is bounded. This is the same move in two
   directions — build modular so the agent can reason, or refactor into modular so the
   verifier can, then restore.
   → [[why-modularity-is-important]], [[sources/meng-jackson-2025-legible-software]],
     [[sources/wang-2025-prometheus-dissect-restore]]

5. **The lifecycle does not end at release.**
   The AINS claim that separates it from SDD/TDD as practised: the process operates
   alongside the running artifact, evolving spec and tests from observation.
   → [[sources/eilam-2026-ai-native-systems-autonomous-evolution]] §3.1

6. **Nobody has patterns for this yet.**
   Context engineering in OSS is a Cambrian explosion — everyone inventing their own,
   no established patterns. Curated context files improve efficiency on focused work;
   generated ones reduce resolve rates, with agents following instructions literally
   even when counterproductive.
   → [[sources/mohsenimofidi-2026-context-engineering-oss]],
     [[sources/lulla-2026-impact-agents-md-efficiency]],
     [[sources/gloaguen-2026-evaluating-agents-md]]

<!-- POSITIONING RISK: "AI-Native SE" is Hassan et al.'s label for SE 3.0, and their
     agentic-SE roadmap is the framing this audience will already know. This thread has
     to differentiate explicitly rather than assume the term.
     → [[sources/hassan-2025-ai-native-se-30]] -->

## Open problems

- **Generating spec from code is unsolved.** Your own caveat on the brownfield
  bootstrap. Move 3 depends on it.
- **How is intent represented?** Free natural language to formal, or a mix. The vision
  post poses this and does not answer it.
- **Does machine-generated code need to stay human-comprehensible?** The compiler-assembly
  analogy — opaque yet trustworthy through abstraction and tooling — or not.
- **How do humans collaborate with each other when AI is the connecting fabric?**
  Underexplored everywhere, not just here.
- **Is completeness of a spec checkable?** → [[sources/huang-2026-specrl-completeness-rewards]]

## Reading
- [[sources/alenezi-2026-human-ai-collaboration-se]]
- [[sources/cito-bork-2025-lost-in-code-generation]]
- [[sources/hassan-2025-ai-native-se-30]]
- [[sources/rosa-2026-specification-driven-code-generation]]
- [[sources/mohsenimofidi-2026-context-engineering-oss]]
- [[sources/minsky-1965-matter-mind-models]]
