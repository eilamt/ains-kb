---
type: source
title: "A benchmark for vericoding: formally verified program synthesis"
citekey: bursuc-2025-vericoding-benchmark
authors: [Sergiu Bursuc, Theodore Ehrenborg, Shaowei Lin, Lacramioara Astefanoaei, Ionel Emilian Chiosa, Jure Kukovec, Alok Singh, Oliver Butterley, Adem Bizid, Quinn Dougherty, Miranda Zhao, Max Tan, Max Tegmark]
year: 2025
kind: paper
container: arXiv
publisher:
doi: https://doi.org/10.48550/arXiv.2509.22908
url: https://arxiv.org/abs/2509.22908
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

Claude: Explicitly contrasts vericoding — generating formally verified code from formal specifications — with vibe coding, on the grounds that test analysis demonstrates the presence but not absence of bugs. Largest benchmark to date: 12,504 formal specifications (3,029 Dafny, 2,334 Verus/Rust, 7,141 Lean), 6,174 unseen. Off-the-shelf LLM success rates: 82% Dafny, 44% Verus/Rust, 27% Lean. Critically — adding natural-language descriptions does not significantly improve performance. The same work reports pure verification capability on existing benchmarks rising from 68% to 96% within a year.

TE: VERICODING is coined (against vibe-coding).

## Quotes
<!-- Always blockquoted, always with a locator. -->

> Fortunately, rigorous correctness guarantees can be created via formal verification, by generating a machine-checkable proof that code meets its human-written specifications. Unfortunately, despite a venerable history dating back to Turing (1950), formal verification remains niche, applied to only a tiny fraction of all software because it requires much more human labor than programming does.

(p. ?)

> This makes it timely to test whether AI can help, either by verifying existing code or by writing new formally verifiable code from scratch based on its specification, which we term vericoding. The premise of this paper is that AI will soon be able to greatly facilitate both, dramatically reducing the cost of creating bug-free software. It is easy to imagine formal verification being simply a built-in final step of future compilers, which discover code problems and attempt to fix them automatically. One can also imagine a future where humans do not need to write programs, only specs.

(p. ?)

> We are primarily interested in constructing a benchmark for two kinds of provers: automated theorem provers (ATPs) such as Dafny and Verus, which use SMT solvers to automatically discharge verification conditions, and interactive theorem provers (ITPs) such as Lean, which use tactics to build proofs.

(p. ?)
