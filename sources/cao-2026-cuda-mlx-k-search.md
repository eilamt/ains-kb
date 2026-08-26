---
type: source
title: "From CUDA to MLX: How K-Search Brings Decades of Kernel Expertise to Apple Silicon"
citekey: cao-2026-cuda-mlx-k-search
authors: [Shiyi Cao, Gal Bloch, Assaf Toledo, Michael Factor, Gil Vernik, Joseph E. Gonzalez]
year: 2026
kind: blog
container: Berkeley AI Research Blog (BAIR)
publisher:
doi:
url: https://bair.berkeley.edu/blog/2026/07/29/cuda-to-mlx-k-search/
lang:

verified: true
holdings: [link]
file:

people: []
tags: [use-case]
missions: [keynote]

status: unread
added: 2026-08-13
---

## Why it matters to me
kernals.

## Notes

Claude: Note on provenance — this was originally published on the Berkeley AI Research blog; the version on our own blog is a ~140-word stub, and the BAIR original is not retrievable from the GitHub Pages source. What follows is the stub plus the account given in the foundational vision post.

The problem statement: modern AI kernels are overwhelmingly written for CUDA, which makes it hard to bring state-of-the-art optimizations to emerging hardware backends. IBM Research collaborated with the K-Search team to automatically translate CUDA kernels to MLX, the claim being that evolutionary kernel optimization dramatically reduces the engineering effort of porting high-performance kernels while keeping performance competitive.

The result cited in [[sources/eilam-2026-ai-native-systems-autonomous-evolution]]: seeding the system with an optimized CUDA implementation of FlashAttention v2 produced an MLX version for Apple Silicon **in a matter of hours**, at performance comparable to state-of-the-art hand-tuned implementations, against the weeks of expert effort a manual port of similar quality would take.

The conceptual point this proof point carries, and the reason it belongs in the talk: **cross-architecture knowledge transfer**. The existing optimized kernel on a different platform is not merely a reference — it is the input that makes the search tractable. Achieving efficiency requires optimizing per combination of hardware, data shape, model architecture, and numerical precision, and in production only a subset of kernels dominates cost and latency, so the AI-native framing is that the system observes kernel-level behavior, detects when a kernel becomes performance-critical, and hypothesizes optimization *without waiting for an SLO violation*.

K-Search also appears as one of the seven frameworks benchmarked in [[sources/batsoyol-2026-discovery-easy-composition-hard]], where it is classified as reflection-driven search maintaining a world model and planning before generating code.

<!-- TE: BAIR original needs fetching or a PDF drop -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
