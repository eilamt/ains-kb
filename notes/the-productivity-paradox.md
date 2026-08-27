---
type: note
title: the productivity paradox
tags: [genai-failure, sdlc]
people: []
missions: [keynote]
status: seed
created: 2026-08-26
updated: 2026-08-26
---
Developers report large productivity gains, but project levels measurements over time such as DORA reveal degradation, code smells increase etc. There are a number of root causes, but also a trajectory for a possible solution, pointing to the important of specification to establish a context, address the non-determinism, and human cognitive readabity over time and across a group of people. 
## Elaboration

Developers report large productivity gains. Project-level measurement over time does
not agree, and the disagreement is not a matter of sampling or enthusiasm — it is
visible in the cleanest causal design available. Adoption produces a velocity increase
that is large and transient, alongside a rise in complexity and static-analysis
warnings that is smaller and permanent. The velocity fades; the complexity does not.

Both observations can be true because they are measured on different timescales and
by different instruments. Self-report captures the session. Complexity and debt
accumulate across sessions, in the codebase and — the part no tool sees — in the team's
shared understanding of it. Verifying generated output requires the domain knowledge
that people reach for generation precisely because they lack.

The mechanism is not mysterious. A non-deterministic generator is being asked to
satisfy deterministic dependability requirements; identical prompts yield functionally
different code, and specification gaps resurface unpredictably on regeneration. That
is a context problem before it is a model-quality problem, which is why the remedy
points at specification rather than at better prompting.

## Tensions
<!-- What complicates this? What would a serious objector say? -->

**The strongest objection is that this is an argument against the thesis, not for it.**
If AI-written code degrades systems, why put AI in charge of more of them? The answer
has to be that the degradation is a property of the *human-mediated* loop — code
generated faster than it can be understood, reviewed by people with no confidence
signal to allocate attention by — and not of AI authorship as such. That claim is
load-bearing for the whole talk and it is not yet established anywhere in this KB.
[[why-modularity-is-important]] and Certus are the closest thing to evidence for it.

**Every result here was measured on a superseded model generation.** The same tension
is already recorded in [[genai-failures]]: which findings are properties of AI-generated
code, and which are artifacts of a particular model's limitations? The honest position
is that nobody knows yet, and the results keep being re-measured on models that no
longer exist.

**The unit of analysis differs across the evidence.** Per-session studies and
longitudinal codebase studies can both be right and still point in opposite directions.

**Novice and senior effects run opposite.** Reported 30–40% gains for less-experienced
developers come with measurable skill atrophy; seniors pay a verification tax that can
cancel the speedup entirely. An aggregate number hides both.

## Connects to
- [[genai-failures]]
- [[what-we-need-ai-to-do-for-sw-engineering]]
- [[specification-as-the-durable-artifact]]
- [[sources/he-miller-2026-speed-cost-quality]]
- [[sources/liu-2026-debt-behind-ai-boom]]
- [[sources/ahmad-2026-comprehension-debt-genai]]
- [[sources/farrag-2026-productivity-reliability-paradox]]

## Provenance

provenance: raw/claude-exports/2026-08-26-keynote-scoping.md

> this paper does a good job in identifies the issue : increased code complexity -
> not sustainable in the long run, and proposes we need "comprehension tax" when we
> train these models.

— your reaction on `sources/he-miller-2026-speed-cost-quality`. Pre-dates this
  conversation.

> great explanation for why we need specification - it is a context window problem.
> Also explains the apparent paradox where developers report productivity but
> actually code dependability degrades!


— your reaction on `sources/farrag-2026-productivity-reliability-paradox`. Pre-dates
  this conversation.

> ~28.6% more lines added (peaking at 281% in month one), 30.3% more static analysis
> warnings, 41.6% higher complexity, with quality degradation persisting after
> velocity gains dissipate.

— assistant summary in `sources/he-miller-2026-speed-cost-quality`
