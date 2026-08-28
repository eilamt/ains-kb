---
type: source
title: "Understanding Specification-Driven Code Generation with LLMs: An Empirical Study Design"
citekey: rosa-2026-specification-driven-code-generation
authors: [Giovanni Rosa, David Moreno-Lumbreras, Gregorio Robles, Jesús M. González-Barahona]
year: 2026
kind: paper
container: "Proceedings of the IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER 2026)"
publisher: IEEE
doi: https://doi.org/10.1109/SANER66133.2026.11576668
url: https://ieeexplore.ieee.org/abstract/document/11576668
lang:
origin:      external
project:
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [sdlc]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

Claude: SANER 2026 accepted a Stage 1 Registered Report on how developers express intent through a TDD-style specification workflow, implemented as a VS Code plugin (Currante) with three phases — structured NL specification, LLM-guided test suite generation and refinement, then fully delegated code generation verified against the suite.

TE: interesting approach to guide LLMs to test and fix problems itteratively. The claim is that failed test does not provide enough info, so they use static analysis to identify the suspicious areas of the code to focus on.

## Quotes
<!-- Always blockquoted, always with a locator. -->

> Large language models (LLMs) have advanced the field of code generation, yet the code they produce often contains errors. Although incorporating Test-Driven Development (TDD) can enhance the reliability of code generation, existing TDD-based approaches for LLMs often lack fine-grained error localization capability, which limits their effectiveness in error repair. To resolve this issue, we propose an enhanced TDD framework that integrates structured program analysis with LLMs. It adopts an automated four-stage feedback mechanism to progressively adapt guidance to task complexity. Moreover, the framework leverages block-level decomposition and a multi-dimensional suspiciousness score strategy to deliver fine-grained, targeted repair signals.

(p. ?)

> LLMs often produce grammatically correct yet semantically incorrect programs [7]–[9]. Providing external feedback to help LLMs improve the correctness of code generation is a widely validated and effective approach.

(p. ?)
