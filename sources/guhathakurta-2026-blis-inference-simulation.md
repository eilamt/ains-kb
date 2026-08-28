---
type: source
title: "The Physics of High-Fidelity Distributed Inference Platform Simulation"
citekey: guhathakurta-2026-blis-inference-simulation
authors: [Dipanwita Guhathakurta, Mert Toslali, Jing Chen, Nick Masluk, Michael Kalantar, Asser Tantawi, Vishakha Ramani, Srinivasan Parthasarathy, Fabio Oliveira]
year: 2026
kind: blog
container: Inference Sim Blog
publisher:
doi:
url: https://inference-sim.github.io/inference-sim/latest/blog/2026/04/09/the-physics-of-high-fidelity-distributed-inference-platform-simulation/
lang:
origin:      own
project:     blis
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [validation, use-case]
missions: [keynote]

status: unread
added: 2026-08-13
---

## Why it matters to me
blis simulator for llm-d.

## Notes

Claude: Note on provenance — the version on the AI Native Systems Research blog is a ~290-word cross-post stub; the full text is on the BLIS blog at the frontmatter URL and is not in the GitHub Pages source repo.

The substantive content available is the argument about *which couplings must be modeled*, and it is the part a systems audience will care about. Three layers:
- **Engine level.** Batches process together, so all requests wait for the slowest operation. KV-cache fills trigger preemptions; long prompts stall short decodes.
- **Cluster level.** Routing policies operate on *stale* cache state; admission control gates overload; prefill/decode disaggregation trades utilization for latency.
- **Control plane.** Autoscalers react to lagged metrics, producing oscillation.

The consequence when these couplings go unmodeled is quantified as an illustration: a back-of-the-envelope model predicting 50 ms time-to-first-token against 200 ms measured in production. That 4x gap is the justification for building a discrete-event simulator rather than an analytical model, and it is the cleanest one-line answer to "why not just estimate it?"

Related and worth cataloguing separately: the August 2026 post on latency modeling reports that, fit once on H100, BLIS predicts held-out configurations across six models and three GPU types at 6.7% median end-to-end error, roughly 200x faster than running them for real.

<!-- TE: full text needs fetching from the BLIS blog or a PDF drop -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
