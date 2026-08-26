---
type: source
title: "VERINA: Benchmarking Verifiable Code Generation"
citekey: ye-2025-verina-verifiable-code-generation
authors: [Zhe Ye, Zhengxu Yan, Jingxuan He, Timothe Kasriel, Kaiyu Yang, Dawn Song]
year: 2026
kind: paper
container: "Proceedings of the International Conference on Learning Representations (ICLR 2026)"
publisher:
doi:
url: https://proceedings.iclr.cc/paper_files/paper/2026/file/41b8c80f9113b9f8e2e129447221682a-Paper-Conference.pdf
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

Claude: proof generation is the major bottleneck for end-to-end verifiable code generation, and writing sound and complete postconditions is generally harder than preconditions. The spec-hackability caution is important and under-discussed. CLEVER's authors note that FVAPPS used an LLM to auto-create formal specifications for 4,715 problems, and that those specifications are often easily hackable, with verification correctness guarded by a layer of test cases. If the AI writes the spec and the AI writes the code, the verifier certifies agreement, not correctness.

See [[notes/the-self-proving-problem]].

## Quotes
<!-- Always blockquoted, always with a locator. -->

> Our extensive evaluation of state-of-the-art LLMs reveals significant challenges in verifiable code generation, especially in proof generation, underscoring the need for improving LLM-based theorem provers in verification domains.

(p. 1)
