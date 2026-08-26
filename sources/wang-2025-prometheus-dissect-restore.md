---
type: source
title: "Dissect-and-Restore: AI-based Code Verification with Transient Refactoring"
citekey: wang-2025-prometheus-dissect-restore
authors: [Changjie Wang, Mariano Scazzariello, Anoud Alshnakat, Roberto Guanciale, Dejan Kostić, Marco Chiesa]
year: 2025
kind: paper
container: arXiv
publisher:
doi: https://doi.org/10.48550/arXiv.2510.25406
url: https://arxiv.org/abs/2510.25406
lang:

verified: true
holdings: [link]
file:

people: []
tags: [verification]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

TE: decomposition and recomposition to help formal verification - in conjunction with modular SWE techniques.

See [[notes/the-self-proving-problem]], [[notes/why-modularity-is-important]].

## Quotes
<!-- Always blockquoted, always with a locator. -->

> Given a formal specification, the model can produce assertions, invariants, and auxiliary lemmas to construct a formal proof. LLMs significantly reduce the manual burden of formal verification, making them powerful tools for both improving the reliability of AI-generated code and lowering the overall cost of applying formal methods.

(p. ?)

> In this work, we introduce Prometheus, a system that facilitates AI-based code verification by leveraging fundamental software engineering principles. The key insight behind Prometheus is that complex programs can be made more amenable to AI-based automated reasoning by first transforming them into semantically equivalent, modular components. These transformations, e.g., function extraction or control flow simplification, decompose the original code into smaller, more manageable units that are easier for AI systems to verify. Once these components are individually verified, Prometheus systematically translates them back to the original code structure.

(p. ?)

> Formal verification is increasingly recognized as a critical foundation for building reliable software systems. However, the need for specialized expertise to write precise specifications, navigate complex proof obligations, and learn annotations, often makes verification order of magnitude more expensive than implementation.

(p. ?)

> Verifying that MaxSubImpl guarantees the IsMaxSubSum specification is non-trivial. The Dafny verifier cannot independently establish correctness, as formal verification often involves reasoning over an exponential number of implicit logical steps, a fundamentally complex task. To make verification feasible, users must assist the verifier by providing intermediate assertions, loop invariants, and supporting lemmas, which guide the verifier in generating more manageable subgoals within the verification process. We now discuss multiple challenges in generating such verification proofs and relate these challenges to AI-based systems.

(p. ?)
