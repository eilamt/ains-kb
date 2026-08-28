---
type: source
title: "What We've Learned About Modeling LLM Latency"
citekey: guhathakurta-2026-modeling-llm-latency
authors: [Dipanwita Guhathakurta, Mert Toslali, Jing Chen, Nick Masluk, Michael Kalantar, Asser Tantawi, Vishakha Ramani, Srinivasan Parthasarathy, Fabio A. Oliveira]
year: 2026
kind: blog
container: BLIS Blog
publisher:
doi:
url: https://inference-sim.github.io/inference-sim/latest/blog/2026/08/06/what-weve-learned-about-modeling-llm-latency/
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
added: 2026-08-26
---

## Why it matters to me
<!-- One or two sentences, your words. Written for you-in-six-months. -->

## Notes

Claude: **Verification note.** Read from the cross-post stub on the AI Native Systems Research blog, which carries the title, date (2026-08-06), and canonical URL. Author list is inferred from the identical username set used on the other BLIS posts in this catalog. The full text lives on the BLIS blog and was not retrievable — confirm authors and fetch the body before promoting.

Third in the BLIS series, and the one that answers the question the first two leave open: **can the predictions be trusted?**

The argument structure is worth noting because it is unusually disciplined for a blog post. Everything BLIS reports at cluster level rests on a single estimate — how long one forward pass takes. If that number is wrong, nothing above it can be right. So the post reduces the trust question to one measurable quantity rather than defending the simulator in general.

The headline claim: fit once on H100, BLIS predicts held-out configurations — **six models across three GPU types** — at **6.7% median end-to-end error**, roughly **200x faster** than running them for real. And, critically for our purposes, those predictions **already steered two serving policies that were subsequently confirmed on a physical cluster**: the probabilistic admitter ([[sources/chen-2026-simulation-production-admission-controller]]) and soft-reflective flow control ([[sources/kalantar-2026-simulation-production-flow-control]]).

That last point is the reason this post matters to the keynote more than its length suggests. The sim2real posts assert that simulation is trustworthy enough to rank algorithms; this post is the evidence for that assertion, generated independently and on held-out configurations rather than on the workloads the policies were tuned against. If anyone in the audience asks "how do you know the simulator isn't just telling you what you want to hear," this is the answer — 6.7% median error on models and GPUs it never saw.

The post also states explicitly that it covers where the approach **falls short**, which the stub does not enumerate. Worth retrieving, since an honest account of the simulator's limits is more persuasive than the accuracy number alone.

## Quotes
<!-- Always blockquoted, always with a locator. -->
