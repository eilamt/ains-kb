---
type: source
title: "From Simulation to Production: How an AI-Native Pipeline Discovered a Better Admission Controller for llm-d"
citekey: chen-2026-simulation-production-admission-controller
authors: [Jing Chen, Mert Toslali, Michael Kalantar, Dipanwita Guhathakurta, Srinivasan Parthasarathy, Fabio A. Oliveira]
year: 2026
kind: blog
container: AI Native Systems Research Blog
publisher:
doi:
url: https://ai-native-systems-research.github.io/ai-native-systems-research/blog/2026/05/13/from-simulation-to-production-how-an-ai-native-pipeline-discovered-a-better-admission-controller-for-llm-d/
lang:
origin:      own
project:     llm-d
clearance:   public

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
Simulation to Production challanges Admission Control.

## Notes

Claude: The first complete end-to-end traversal of the loop — observe, reason, change, validate, deploy — with an upstream merge at the end. System under control: llm-d. Discovery: Nous. Validation substrate: BLIS.

**Observe.** The default llm-d admission controller admits everything until the cluster saturates, then hard-rejects all sheddable traffic. Saturation is computed from queue depth and KV-cache utilization across serving instances. The failure mode is a binary cliff: by the time saturation reaches 1.0, queues are deep and KV caches nearly full, so even protected traffic is already degraded. Nous identified the opportunity; the curve shape, math, and parameters were left entirely to discovery.

**Two evolutions, and the difference between them is the lesson.** The first ran 10 iterations and found a linear-ramp algorithm cutting critical latency 42% — but with four threshold parameters tuned to one model and workload. It worked and it did not port. The second run added an efficiency metric (milliseconds saved per request shed, to penalize wasteful shedding) and a constraint that the result be explainable and parameter-free. Ten more iterations moved through linear (over-sheds at low load), quadratic (not aggressive enough at overload), and higher-power polynomials, converging on quintic.

*Note for the keynote:* the −42% figure that circulates in our internal materials is the **first, non-portable** evolution, not the shipped algorithm. The published numbers for the probabilistic admitter are 24–47% simulated reduction in critical E2E and TTFT, and up to 97% TTFT p90 on real hardware. Worth correcting before the talk.

**The algorithm** (strikingly small, which is part of the point): saturation = average across serving instances of `max(queue_depth/QD_threshold, kv_utilization/KV_threshold)`, mapping exactly to how llm-d already computes it. Priority >= 0 always admitted. Priority < 0 rejected with probability `min(saturation^5 * 300, 1.0)`. Both the exponent 5 and the multiplier 300 were discovered by Nous. Effect: ~1% shedding at saturation 0.12, ~29% at 0.25, 100% at 0.34 — a smooth transition with no cliff, and no explicit thresholds.

**Validate.** Qwen3-14B on vLLM, 4x H100-SXM-80GB, routed through llm-d. Eight scenarios: four traffic shapes (balanced 50/50, chatbot 80/20, code completion 30/70, "blindspot" 10/90) x two load levels. Critical-tier latency improved across all workloads. Largest gain TTFT p90 up to **97%** on blindspot, because early dropping prevents the queue buildup that causes scheduling delay. E2E improved 27–50% in most workloads, 8–17% at lighter load. Chatbot benefited least (~2%) — predominantly critical traffic, ~2k+ output tokens, latency dominated by generation. Tradeoff stated plainly: 5–19 percentage points more traffic shed, total throughput down 6–31%, but the shed requests are low-priority work that would have incurred very long latencies regardless.

**Deploy.** Merged into llm-d-router as the `probabilisticadmitter` plugin with simulation-suggested defaults.

Four lessons from the post, all quotable:
- **Simulation fidelity matters less than simulation speed.** BLIS does not need exact latency numbers; it needs to *rank* algorithms correctly. Getting the ordering right in seconds rather than hours is what makes agentic exploration viable.
- **Parameter-free designs transfer better.** Constraining the search space produced the more robust result.
- **AI agents need structured boundaries, not micromanagement.** Objective (beat baseline 30%), constraints (no tunable parameters, must be explainable), fitness metric (efficiency) — no prescribed curve shapes.
- **Translation is a distinct problem from discovery.** Generating production Go from a simulation algorithm requires understanding two codebases and mapping signals across abstraction layers; keeping it a separate AI-assisted phase kept both phases reliable.

Provenance framing to reuse: "The algorithm was not pulled from training data or proposed speculatively. It was discovered through repeated experimentation against a simulator... and only then translated into production code with full provenance."

<!-- TE: -->

## Quotes
<!-- Always blockquoted, always with a locator. -->
