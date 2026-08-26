---
type: source
title: "Why Simulate Before You Scale"
citekey: guhathakurta-2026-why-simulate-before-scale
authors: [Dipanwita Guhathakurta, Mert Toslali, Jing Chen, Nick Masluk, Michael Kalantar, Asser Tantawi, Vishakha Ramani, Srinivasan Parthasarathy, Fabio A. Oliveira]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/03/05/why-simulate-before-you-scale/
lang:

verified: true
holdings: [link]
file:

people: []
tags: [use-case, validation]
missions: [keynote]

status: unread
added: 2026-08-13
---

## Why it matters to me
llm-d blis simulator.

## Notes

Claude: Note on provenance — the version on the AI Native Systems Research blog is a ~150-word cross-post stub. The full text lives on the BLIS blog at the URL in frontmatter and is not in the GitHub Pages source repo, so what follows is from the stub plus cross-references.

The framing is economic rather than technical: a single high-end GPU costs upwards of $30,000 and a production cluster runs into millions per year, yet most teams make their first scaling decisions from rough estimates, vendor benchmarks, or trial and error on live hardware. The pitch is testing a deployment plan before spending a dollar on GPUs — a flight-simulator approach to capacity planning that runs on a laptop with no GPUs required.

For the keynote this is the entry point to the BLIS argument, but [[sources/chen-2026-simulation-production-admission-controller]] states the load-bearing version more usefully: simulation is what lets the loop run at machine speed, and without it the cycle from hypothesis to evaluation is gated by hardware availability and cost.

<!-- TE: full text needs fetching from the BLIS blog or a PDF drop -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
