---
type: source
title: "The Productivity-Reliability Paradox: Specification-Driven Governance for AI-Augmented Software Development"
citekey: farrag-2026-productivity-reliability-paradox
authors: [Sabry E. Farrag]
year: 2026
kind: paper
container: arXiv
publisher:
doi: https://doi.org/10.48550/arXiv.2605.01160
url: https://arxiv.org/abs/2605.01160
lang:
origin:      external
project:
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [genai-failure, mdd, sdd]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

Claude: grounds SDD in a specific failure mode: the non-determinism of LLM generators means identical prompts produce functionally different code across invocations, and specification gaps resurface unpredictably on regeneration.

TE: great explanation for why we need specification - it is a context window problem. Also explains the apparent paradox where developers report productivity but actually code dependability degrades!

See [[notes/specification-as-the-durable-artifact]].

## Quotes
<!-- Always blockquoted, always with a locator. -->

> Productivity-Reliability Paradox (PRP), that arises from the fundamental mismatch between non-deterministic code generation and the deterministic requirements of dependable software systems.

(p. ?)

> Three moderating variables dissolve the paradox: (a) task abstraction level, where AI tools excel at low-abstraction syntactic tasks and struggle with high-abstraction architectural decisions (Imai, 2023); (b) codebase maturity, where Greenfield projects benefit disproportionately while mature codebases incur verification overhead that can exceed generation savings (Becker et al. 2025); and (c) developer experience, where novice developers show productivity gains of 30–40% but exhibit measurable skill atrophy (Joyner et al. 2024; Anthropic, 2026), while senior developers experience a "verification tax" that can negate nominal speedups (DZone, 2024).

(p. ?)

> Transaction Cost Economics (Williamson, 1985) explains governance choices, market, hierarchy, or hybrid, as functions of three transaction attributes: asset specificity, uncertainty, and frequency. TCE has been extensively applied to IT outsourcing (Lacity & Willcocks, 2012; Aubert et al. 2012) and has recently been reinterpreted for AI-mediated production. A California Management Review analysis "From Coase to AI Agents" (Berkeley, 2025) argues that AI agents reshape firm boundaries without eliminating the Coasean rationale for the firm, warning of an "Illusion of Efficiency" when agent proliferation produces coordination failures that mirror classical TCE concerns. No prior work has applied TCE specifically to the governance of AI code generators, that is, to the question of what contractual form (specification, test, constitution) optimally governs the human-AI principal-agent relationship in software production. This is the theoretical gap the SGM addresses.

(p. ?)

> Definition. The Productivity-Reliability Paradox is the empirically observed phenomenon in which AI-powered coding assistants produce statistically significant improvements in individual-level output metrics (task completion speed, lines of code, suggestion acceptance rates) that coexist with statistically significant degradation in system-level dependability metrics (delivery stability, change failure rate, code churn, defect density in production). variables: abstraction level / architectural complexity, Green vs Brown (Green easier), Developer experience.

(p. ?)

> 4.2.5 The Context Window Constraint
> A technical limitation that compounds the PRP in practice, yet receives little attention in the empirical literature, is the finite context window of current LLMs. Even the largest available models (supporting 128K–200K tokens of context) cannot simultaneously hold the full codebase, test suite, architectural documentation, and conversation history of a non-trivial project. As projects grow beyond a few thousand lines, the AI agent progressively loses awareness of distant modules, implicit conventions, and cross-cutting dependencies.
> This context limitation has three practical consequences for reliability. First, AI-generated code in large projects may violate architectural patterns or naming conventions established in files outside the current context window, producing subtle inconsistencies that pass local review but cause integration failures. Second, when AI agents operate autonomously over multi-step workflows (Tier 3), context loss across iterations can produce drift in which later steps contradict decisions made in earlier steps. Third, the context window creates a bias toward local correctness at the expense of systemic coherence: the generated code works in isolation but fails in the broader system context.
> The SGM's specification mechanisms partially mitigate this constraint by encoding critical context (architectural rules, API contracts, invariants) in compact, persistent documents (constitutions, specifications) that can be included in every AI invocation. This is an engineering rationale for specification governance that complements the economic rationale derived from TCE: specifications serve not only as contractual constraints but as compressed representations of project context that compensate for the AI's finite memory.

(p. ?)

> A system-level mechanism that amplifies the PRP is the code review bottleneck. When AI tools accelerate individual code generation without proportional acceleration of the review pipeline, the result is a growing queue of unreviewed pull requests that absorbs the productivity gains at the organizational level. Faros AI's 2025 telemetry study of over 10,000 developers across 1,255 teams quantifies this effect: teams with high AI adoption completed 21% more tasks and merged 98% more pull requests, but PR review time increased by 91%, average PR size grew by 154%, and bug counts rose by 9% (Faros AI, 2025). Organizational-level DORA metrics (deployment frequency, lead time, change failure rate) showed no measurable improvement despite the individual-level gains.

(p. ?)

> At Tier 3, the emergence of SDD has drawn explicit comparison to Waterfall, with Gojko Adzic characterizing SDD as "the Revenge of Waterfall or BDD Taken to a New Level." We argue that the comparison is imprecise: SDD shares Waterfall's emphasis on upfront specification but differs fundamentally in its iterative verification mechanism (specifications are continuously validated against implementation, not frozen). The more accurate analogy is that Tier 3 AI creates a specification-constrained iteration model that combines Waterfall's specification rigor with Agile's iterative feedback, a hybrid that neither traditional framework anticipated.

(p. ?)
