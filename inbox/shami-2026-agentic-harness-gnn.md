---
type: source
title: "Can an Agentic Harness Rediscover the Insights in a Research Paper?"
citekey: shami-2026-agentic-harness-gnn
authors: [Naima Abrar Shami, Mert Toslali, Srinivasan Parthasarathy, Vasiliki Kalavri, Fabio A. Oliveira]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/06/17/can-an-agentic-harness-rediscover-the-insights-in-a-research-paper/
lang:

verified: false
holdings: [link]
file:

people: []
tags: [harness, use-case, validation]
missions: [keynote]

status: unread
added: 2026-08-26
---

## Why it matters to me
<!-- One or two sentences, your words. Written for you-in-six-months. -->

## Notes

Claude: **Verification note.** Title, date, content, and authorship-by-username are read from the post source in the blog repo. The *full author names* above are inferred by mapping blog usernames (`naima`, `toslali-ibm`, `sriumcp`, `vkalavri`, `oliveira`) against the same usernames appearing in already-verified entries, plus the referenced GRADES-NDA paper. Confirm the names and the exact permalink slug, then promote out of quarantine.

This post was not in the catalog and is arguably the strongest single validation result for Nous, because it is the one case where the harness is measured against a **known human answer** rather than against a baseline it also discovered.

**Setup.** Nous was pointed at a streaming GNN inference pipeline on Apache Flink that the team had already built and characterized in a published paper (Shami & Kalavri, GRADES-NDA '25, doi 10.1145/3735546.3735856). The pipeline retrieves a node's 2-hop neighborhood from Flink keyed state, assembles the local subgraph as JSON, and sends it to a GraphSAGE model in TorchServe. Evaluated on Reddit (233K nodes, 115M edges, 602-dim features). Three campaigns, five iterations each, **fully autonomous after launch — no hints, no intermediate corrections, no experiment designs from the humans**. Total ~$110 in LLM calls and ~32 hours wallclock. Artifacts public at `Naima2002/flink-gnn-nous-artifacts`.

**The headline result: the harness independently recovered all 7 of the paper's major directional conclusions** — TorchServe worker count improves throughput to a saturation point then stops; median E2E latency drops sharply to that same point; smaller 2-hop fanouts give higher throughput; larger fanouts widen the latency distribution; E2E latency stays bounded under sustained load; async inference beats sync; past saturation the bottleneck shifts from TorchServe inference to Flink-side subgraph construction. Absolute numbers shifted 5–10x because the harness ran on a laptop with no GPU, **but every shape, ordering, and threshold reproduced**. That distinction — direction and threshold reproduce, magnitude does not — is exactly the property the sim2real posts rely on, and here it is demonstrated independently.

Four results beyond reproduction, each a different *kind* of contribution:
- **Mapped the regime of a known result.** The paper reported async beats sync by ~35%. Nous swept parallelism and found the advantage is not constant: 25.7% at parallelism 1, largely gone at parallelism 2 or higher, because multiple parallel synchronous operators saturate TorchServe much as one async operator does.
- **Found an untested failure mode.** With ASYNC_CAPACITY and operator parallelism both pinned to 1, async throughput collapsed to ~90 records/s against sync's ~510 at the same parallelism. The async path does not degrade gracefully as its in-flight budget shrinks; below a threshold it stalls. The humans had never probed that corner.
- **Replaced a black-box metric with a mechanism.** The paper reported per-request inference time as one number. Nous instrumented the TorchServe handler for per-stage timing and correlated against subgraph node count: preprocessing scales at ~0.011 ms/node against 0.0076 ms/node for inference, approaching **61% of total handler time** as subgraphs grow. JSON-to-tensor parsing, not the GNN forward pass, is the larger cost — and it points at a specific fix (binary encoding upstream).
- **Explained a null result.** It re-ran and confirmed the paper's finding that increasing TorchServe batch size does not improve throughput, then explained why: preprocessing dominates and runs per-request so batching cannot amortize it, and on CPU the inference step scales close to linearly with batch size.

**The anecdote that will land hardest with a systems audience.** A single PyTorch threading parameter (TORCH_INTRA_THREADS) had cost the team roughly two weeks of debugging during the original build. PyTorch's default of 64 caused thread thrashing on every per-request inference call — per-call thread-pool barrier overhead far exceeding the actual compute. Invisible in system-level metrics; the team never explicitly set the value. Nous rediscovered the anti-pattern (raising it from 1 to 4 dropped E2E throughput 13–37% with no improvement in per-request inference time) and **named the mechanism correctly**: intra-op threads contending for cores on a 16-core machine, barrier overhead dominating ~0.2 ms of real compute.

The authors' own framing of the role is appropriately modest and worth borrowing verbatim in spirit: not a replacement for the researchers who design and build the system, but a way to extend what any single researcher with limited time can practically characterize — sweeping combinations a human would skip, refining coarse-grained results, and pointing back at specific lines of the implementation.

Also note this post describes Nous as running fully autonomously, whereas the public protocol documents two mandatory human gates per iteration. Reconcile before claiming an autonomy level on stage — see [[sources/anon-2027-nous-scientific-experimentation]].

## Quotes
<!-- Always blockquoted, always with a locator. -->
