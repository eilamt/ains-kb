---
type: note
title: the self-proving problem
tags: [verification, genai-failure]
people: []
missions: [keynote]
status: seed
created: 2026-08-26
updated: 2026-08-26
---
There is a potential issue if we use the same AI agent to create the specification and the proof. 


## Elaboration

The whole chain from spec through abstract code to proof harness is problematic, and this  holds even across different agents if they work from the same spec... 

## Tensions

The mitigation has moved from aspiration to practice. Certus employs a different coding agent (Codex) to independently cross-check translation source against target. That cross-checker was itself validated by a systematic method of poisoning code and specifications to create deliberate source/target mismatches, then confirming all poison items were identified. This narrows the problem without dissolving it — the cross-checker is still a language model, and the guarantee it provides is weaker than an independent human verification would be.

## Connects to
- [[genai-failures]]
- [[sources/anon-2026-certus-review]]
- [[sources/ye-2025-verina-verifiable-code-generation]]
- [[sources/bursuc-2025-vericoding-benchmark]]
- [[sources/wang-2025-prometheus-dissect-restore]]
- [[sources/waddington-2026-holding-wild-elephant]]

## Provenance

provenance: raw/claude-exports/2026-08-26-keynote-scoping.md

> Using Gen-AI to apply formal verification and reduce the burden has potential
> but proving the chain-of-transformation correctness (spec + code properties
> abstract code proofs/test harness) is tricky; its sort of self-proving – we
> are looking to applying adversarial alternative LLM (e.g., Codex) to attack
> this issue

— `Certus_Review_Priya_JUL2026.pptx`, slide 16

> CLEVER's authors note that FVAPPS used an LLM to auto-create formal
> specifications for 4,715 problems, and that those specifications are often
> easily hackable, with verification correctness guarded by a layer of test
> cases.

— assistant summary in `sources/ye-2025-verina-verifiable-code-generation`

> we absolutely need to acknowledge the tension. Certus is a work in progress.
> We hypothesis that we need validation. We experiment with different
> techniques. We have partial results, and there are serious threats to the
> approach which we need to investigate, potentially enhance as future work
> with adverserial validation. We are not claiming we solved everything. We
> are reporting about where we are. what we learned and we need to examine it
> critically.

— Tamar, on review of triage `triage-2026-08-26-certus-modularity-sdlc-2.md`

> Without assurance of translation, the model checkers are verifying code that does not
> exist! Yet more, we can't ask an agent to check itself and expect it to have newly
> found levels of oversight or correctness (well, we can, but only so far).

— `sources/waddington-2026-holding-wild-elephant` §3.5.1
