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
