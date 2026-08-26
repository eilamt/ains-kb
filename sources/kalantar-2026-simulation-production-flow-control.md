---
type: source
title: "From Simulation to Production Part II: Soft-Reflective Flow Control for llm-d"
citekey: kalantar-2026-simulation-production-flow-control
authors: [Michael Kalantar, Mert Toslali, Jing Chen]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/07/27/from-simulation-to-production-part-ii-soft-reflective-flow-control-for-llm-d/
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
simulation to production challanges in llm-d.

## Notes

Part II of [[sources/chen-2026-simulation-production-admission-controller]].

Claude: Same loop, second problem class — and the pairing is what makes it evidence of a *methodology* rather than a lucky result. The distinction is drawn carefully: admission control acts at the gate and may reject a request; flow control acts at the dispatch queue and decides which already-admitted request goes to a backend next. Neither replaces the other.

**Observe.** llm-d's default static-usage-limit policy applies one threshold to every priority band, defaulting to 1.0 — effectively a no-op until pods fully saturate. Lowering the threshold does not help, because threshold=0.5 gates critical and sheddable traffic at the same saturation point. There is no way to express "shed non-critical work first," so critical requests queue behind sheddable work.

**The algorithm.** For N priority bands: `ceiling[0] = 1.0` (critical never gated), `ceiling[i] = 1 - i * saturation / (N-1)`. When a band exceeds its ceiling the plugin rate-limits rather than blocking, dispatching every `round(saturation / (1 - saturation))`-th tick — a proportional duty cycle. It exploits the existing dispatch loop, which already treats `saturation >= ceiling` as a head-of-line block, so alternating 1.0 and 0.0 on successive ticks yields proportional throughput with no change to the dispatch code path.

**The contrast with Part 1 is the strongest single point in the post.** The probabilistic admitter has two discovered constants (exponent 5, multiplier 300). The reflective ceiling has **no free parameters at all** — the shape follows entirely from the number of priority bands and the current saturation reading, and adding a new priority level extends the reflection automatically with no config change. Two-tier case collapses to `1 - saturation` for the sheddable band. Dead zone below saturation 0.5, steep tail beyond 0.8, and the gate never fully closes: bounded latency rather than indefinite starvation.

**Validate.** 2x H100-SXM-80GB (note: different from Part 1's 4x), Qwen3-14B, three workloads (code generation, interactive chat, reasoning), all metrics critical-class only.
- Code generation @ 16 QPS: critical TTFT p99 **13.6 s -> 263 ms (-96.7%)**. The post's own framing — the difference between a usable and an unusable developer experience — is the right line for a slide.
- Reasoning @ 0.7 QPS: TTFT p99 330 s -> 16 s (-91.2%), E2E -48.5%, **throughput recovers +64.4%** because the baseline was overloaded enough to drop requests the treatment completed.
- Under-capacity cases: correctly a no-op. Explicitly framed as important, not as absence of result — a flow control policy that penalizes traffic under no contention would do harm.

**The reported regression is worth keeping rather than trimming.** Interactive chat @ 40 and 60 QPS is modestly *worse* than baseline (+18% and +31% TTFT p99, at low absolute values) in the transition zone where the ceiling begins to engage but protection has not yet outweighed the rate-limiting overhead. It disappears at 80 QPS. Presenting this alongside the 96.7% figure is what makes the 96.7% figure credible.

Deployed as `soft-reflective-ceiling-policy` in llm-d-router, enabled with a single YAML change.

<!-- TE: -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
