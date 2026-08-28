---
type: source
title: "Detecting and Correcting Hallucinations in LLM-Generated Code via Deterministic AST Analysis"
citekey: khati-2026-detecting-correcting-hallucinations-ast
authors: [Dipin Khati, Daniel Rodriguez-Cardenas, Paul Pantzer, Denys Poshyvanyk]
year: 2026
kind: paper
container: "Proceedings of the IEEE/ACM 3rd International Conference on AI Foundation Models and Software Engineering (FORGE '26)"
publisher: ACM
doi: https://doi.org/10.1145/3793655.3793725
url: https://dl.acm.org/doi/10.1145/3793655.3793725
lang:
origin:      external
project:
clearance:   public

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

Claude: KCHs are subtle semantic errors like non-existent API parameters that evade linters and fail at runtime; their deterministic AST framework validates against a knowledge base built by library introspection, achieving 100% precision, 87.6% recall, and auto-correcting 77% of cases. They note constrained decoding and LLM-in-the-loop repair are unreliable for this class.

TE: basically lightweight static analysis to address hallucination in code.

## Quotes
<!-- Always blockquoted, always with a locator. -->
