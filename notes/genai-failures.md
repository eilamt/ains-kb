---
type: note
title: Gen AI Failures
tags: [genai-failure]
people: []
missions: [keynote]
status: developing
created: 2026-08-11
updated: 2026-08-11
---

GenAI failures must be understood. They are different then developer failures.

## Elaboration

Claude: Relevance: the distinctively non-human failure modes cluster as inaccurate self-reporting, constraint violation despite explicit instruction, plausible-but-wrong concretization of underspecified intent, and confabulated dependencies. Note the asymmetry with human developers: a human who breaks a stated constraint usually knows they did; the agent reports success. That is the failure mode with no good human analogue, and it's the one growing in share.

TE: other reported issues are code complexity, code smells, copy+paste instead of referencing, the affect is that over time productivity in group/project level actually goes down (based on DORA measures). Validation (eg PR handling) is a huge bottleneck.

## Tensions

We need to be careful to distinguish between real inhernt issues in AI generating code, vs ones that are already solved in newer model generations ! It is also important to categorise these failures. Eg the generation of code, vs. the interaction with the developer etc. and the scope - single session vs multitude - ie accumulation, so that we can find solutions.

## Connects to
- [[sources/tang-2026-how-coding-agents-fail]]
- [[sources/he-miller-2026-speed-cost-quality]]
- [[sources/meng-jackson-2025-legible-software]]
- [[sources/cervantes-kazman-2026-llm-architecture-code-generation]]
- [[the-self-proving-problem]]
