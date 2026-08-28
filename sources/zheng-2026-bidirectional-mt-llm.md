---
type: source
title: "Bidirectional Empowerment of Metamorphic Testing and Large Language Models: A Systematic Survey"
citekey: zheng-2026-bidirectional-mt-llm
authors: [Zheng Zheng, Zenghui Zhou, Yinwang Xu, Daixu Ren, Tsong Yueh Chen]
year: 2026
kind: paper
container: arXiv
publisher:
doi: https://doi.org/10.48550/arXiv.2605.13898
url: https://arxiv.org/abs/2605.13898
lang:
origin:      external
project:
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [mt]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

Claude: covers the bidirectional relationship — MT gives an oracle-alleviating framework for testing LLMs, while LLMs automate the historically manual work of discovering metamorphic relations from requirements, documentation, and source, synthesizing input transformations, and running agentic test workflows that iterate generation, execution, checking, and refinement. Also: Valentin, Madadi, Sapia & Böhme, Incoherence as Oracle-less Measure of Error in LLM-Based Code Generation (arXiv 2507.00057) — a measure of error estimated without oracles, which is conceptually close to your prediction-error taxonomy.

Wikipedia: metamorphic relations (MRs) are necessary properties of the intended functionality of the software, and must involve multiple executions of the software. Consider, for example, a program that implements sin x correct to 100 significant figures; a metamorphic relation for sine functions is "sin (π − x) = sin x". Thus, even though the expected value of sin x1 for the source test case x1 = 1.234 correct to the required accuracy is not known, a follow-up test case x2 = π − 1.234 can be constructed. We can verify whether the actual outputs produced by the program under test from the source test case and the follow-up test case are consistent with the MR in question. Any inconsistency (after taking rounding errors into consideration) indicates a failure of the program, caused by a fault in the implementation.

## Quotes
<!-- Always blockquoted, always with a locator. -->

> For many tasks, such as question answering, code synthesis, dialogue, and agent planning, there may be multiple acceptable outputs rather than a single ground truth. This makes the classical oracle problem [6] particularly severe in the LLM setting. Moreover, LLMs exhibit failure modes that are difficult to capture with static benchmarks or exact-match assertions, including hallucination [42], demographic and social bias [85], adversarial vulnerability [118], and non-deterministic behavior. Practitioner-oriented discussions have further emphasized that manually labeled ground-truth evaluation does not scale to the volume and diversity of inputs required for LLM-powered software [96]. These characteristics create an urgent need for testing and evaluation methods that can reason about behavioral relations rather than relying exclusively on exact expected outputs. Metamorphic testing (MT) [11, 15, 16, 84] provides a natural response to this challenge. MT was originally proposed as a technique for generating follow-up test cases and has since become a prominent oracle-alleviating testing paradigm for systems whose exact outputs are difficult or impossible to determine. Instead of checking whether a single output is correct, MT checks whether a necessary relation, known as a metamorphic relation (MR), holds among the outputs of multiple related inputs.

(p. ?)
