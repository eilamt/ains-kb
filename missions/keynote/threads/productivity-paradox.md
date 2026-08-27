---
type: thread
title: The productivity paradox
question: how do we measure productivity? are we more productive with AI? and if not, what are the gaps?
tags:
  - genai-failure
  - sdlc
people: []
missions:
  - keynote
status: open
created: 2026-08-26
updated: 2026-08-26
---

## The question

Practitioners report large productivity gains from AI coding assistants. Project-level
and longitudinal measurement does not agree. This thread establishes that the gap is
real and measured rather than anecdotal, and identifies what it costs. It also established 
the different measures of productivity (individual vs group), scope (temporal and spatial such as single module vs entire project and what time length) and the root causes. 
## Where I stand now

My position (date: aug 27) is that the potential of AI for code is absolutely outstanding - something I as a researcher and practitioner for 26 years in CS is amazed to see. But, using it affectively, collaboratively, to fulfill the most potential is NOT TRIVIAL. 
There are lots of open questions. It is like we are in the cambrian age where everyone are inventing their own methods, and no one knows the right answer. 
This is why it is interesting. AI Native Systems research area (my team) takes on this challenge. 
We identify the challenges, and we work to close these gaps. We need to know how to work with AI collaboratively, and how to increase project productivity in the ling run, not reduce it. We need to make it real. So yes, the academic papers in this thread help establish the gaps and identify some of the root causes of the gaps, that require addressing. 

## Moves in the argument

1. **Velocity rises sharply and transiently; quality degrades persistently.**
   → [[the-productivity-paradox]] — the evidence and the mechanism.



## Open problems

- **Separating inherent limits from generation-specific artifacts.** Your own tension in
  [[genai-failures]]: which of these findings are properties of AI-generated code, and
  which are already solved in newer model generations? Every result here is measured on
  a model generation that has since been superseded.
- **Unit of analysis.** Tang measures per-session; DORA-style measures look at a codebase
  over time. Different units, potentially different conclusions.
- **Whether the paradox is an argument for the AINS thesis or against it.** If AI-written
  code degrades systems, the case for AI as *primary* agent needs the degradation to be a
  property of the human-mediated loop rather than of AI authorship 
  TAMAR: It is an argument that the AINS vision is not there yet, we have to invent how to work effectively with AI. Humans will always be in the loop. One of the open questions is the right model of collaboration between humans and AI. Note that when I describe the AINative (aka, AINS) vision, I need to abstract the role of humans and AI and give more degrees of freedom to define how they collaborate, rathern than determine upfront what humans and AI do. Another alternative is to say it is a nice goal to have to reduce the labor needed from humans, but the journey to that goal will require time, and on the way we need to see how AI and Humans can collaborate effectively. 

## Reading
- [[sources/he-miller-2026-speed-cost-quality]]
- [[sources/liu-2026-debt-behind-ai-boom]]
- [[sources/ahmad-2026-comprehension-debt-genai]]
- [[sources/farrag-2026-productivity-reliability-paradox]]
- [[sources/alenezi-2026-human-ai-collaboration-se]]
