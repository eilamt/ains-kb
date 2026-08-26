---
type: source
title: "Spotlights Overview"
citekey: anon-2026-spotlights-overview
authors: []
year: 2026
kind: talk
container: "Internal IBM — AI Native Systems / ISRL, leadership briefing"
publisher:
doi:
url:
lang:

verified: true
holdings: [pdf]
file: spotlights_overview_deck.pptx

people: []
tags: [ains-concept, harness, use-case]
missions: [keynote]

status: read
added: 2026-08-13
---

## Why it matters to me
spotlight.

## Notes

Claude: 12 slides plus dense speaker notes, addressed to AINS leadership, ~10 minutes. Internal.

**This deck contains the sharpest strategic framing in the entire catalog, and it is not in any blog post or paper.** The one-line positioning: everything else in this space is an *execution* layer — Nous, AlphaEvolve, OpenEvolve, ShinkaEvolve, AdaEvolve, EvoX, Glia, CORAL, Claude Code, OpenHands, SWE-agent — and **all of them require a human to point and say "optimize this."** The speaker note calls them "exploitation engines without an exploration front-end." Spotlights is the *selection* layer: which functions and code regions in a million-line system are worth the execution machinery's time.

The argument for why that layer is hard and underexplored: today the choice comes from intuition, papers, or colleagues, and "cross-component bottlenecks and recent-literature ideas don't surface from reading code." The explicit note that Spotlights does not compete with execution tools but *feeds* them is the right relationship to state on stage — and it repositions Nous as one consumer of a pipeline rather than the whole story.

**Terminology, which is precise and worth adopting.** An *Objective* is a user statement of what to optimize (coarse: "improve user experience"; focused: "reduce TTFT for agentic workloads"). An *Anomaly* is a noteworthy pattern surfaced from traces, metrics, and logs — "not a raw measurement, but what the system actually did that's worth investigating." A *Finding* is the output of deep research on a question — "conclusions drawn from source, not just facts, but what they mean, with pointers back to the evidence." A *Candidate* is the *where* (a spotted code location with rationale); a *Proposal* is the *how*. Note the discipline that every candidate carries the anomaly ids that motivated it, so a recommendation always traces back to the trace that produced it.

**Two discovery paths converging on one typed output.** The signal-driven path runs telemetry → typed signals (WorkloadProfile, TraceSummary, Anomaly[]) → candidate generation, joined with a ProjectTree from a repo walk. The technique-driven path runs the other direction: per-module candidate discovery (Claude and Codex taking alternating turns reviewing a module), then a per-module literature survey, then a proposal for each (candidate, finding) pair — with an empty-module short-circuit so no cycles are spent drafting proposals for modules where discovery found nothing. Both paths emit the same `Candidates` shape by design.

**The signal-driven worked example is the strongest single piece of evidence in the deck.** Hermes-3-Llama-3.1-8B on vLLM 0.18.0, SWE-Smith, 245 requests, 40% GPU memory, 16 GB CPU offload with LRU. Two independent anomalies: CPU prefix-cache hit rate **0.6%** against 82.1% on the GPU prefix cache, with end-to-end p99/p50 at **14.5×**; and a heterogeneous completion-length distribution, p50 = 63 tokens against max = 1422, with the five slowest requests all ≥600 completion tokens.

The reasoning that connects them is the part worth showing: anomaly 1 alone would point at the offload tier broadly; anomaly 2 alone would point at sampling or scheduling. Together they triangulate to the eviction policy specifically — under recency-only eviction, the request-local working set of long-completion requests pushes reusable cross-request prefix blocks off the LRU tail before the next request can hit them. The candidate is a single ~40-line class (`vllm/v1/kv_offload/cpu/policies/lru.py`) behind a plug-in seam that already exists, with `ARCCachePolicy` as a sibling. The deck's own one-line pitch: "Two independent symptoms — a dead offload cache and a heavy-tailed completion length — point at the same ~40-line class."

**The technique-driven example makes a subtler claim.** Starting from S3-FIFO (Yang et al., SOSP '23), the ranker found the `_CACHE_POLICIES` registry seam in vLLM without a human pointing at it. The deck is scrupulous that the idea was already on vLLM's radar — RFC #14724 lists S3-FIFO as a built-in eviction option — and claims only that Spotlights put paper next to code with a concrete change spec before the RFC was implemented. Two independent discovery paths converging on the same component from opposite directions is the actual result.

**Four input streams**, three live: code structure (ProjectTree over the repo — vLLM measured at 619 modules, 4,924 files, coverage 1.0), literature (a Codex/Gemini/Claude-driven paper harvester with as-of dating and a relevance ranker that scores papers against a code scope by translating both sides to pseudo-code), telemetry (OpenTelemetry → ClickHouse with log correlation by trace_id, SigNoz for humans), and repo history (PRs, issues, commit patterns — on the way, and described as high-signal because "open issues often describe known limitations the maintainers haven't prioritized").

The stated selection principles are quotable: prefer live signals over static analysis, "because much of what makes inference systems hard to optimize is invisible until they run"; and prefer inputs whose value compounds.

**Knowledge architecture.** A single schema-checked wiki with two narrow APIs — Archive for writes, Retrieve for reads — fed by six modules. The rationale is directly relevant to the modularity thread: "Most agentic systems lose coherence because each component invents its own memory." One hub with provenance is what lets a downstream candidate cite this paper, this PR, this anomaly rather than gesturing. A coverage check on the hub catches silent failures where an inserter stops writing.

**Two human roles, deliberately separated.** A Product Manager sets the Objective at the front door; a Developer reviews evidence at the end and owns the PR. On FAIL the change is discarded with no human review at all. The stated future state is that Validation's evidence becomes rich enough that passing changes go straight to PR. That is a concrete, defensible instance of governed autonomy with a shrinking human envelope — better than the abstract version in the vision post, because the gate that gets removed first is named.

Nine workstreams, most marked live. Validation has a real baseline: vLLM KV-offload, 22/25 entries fully green, 316+ tests passed.

**How this relates to the keynote.** If the talk is only about Nous, it presents the execution layer and leaves the audience's obvious question — *how did you know to look there?* — unanswered. Spotlights is the answer, and the selection/execution distinction is a cleaner organizing frame than the Reasoner/Changer split for a systems audience, because it maps onto a gap they already feel. Note it is internal and early, so the claim has to be positioned as direction rather than result.

## Quotes
<!-- Always blockquoted, always with a locator. -->
