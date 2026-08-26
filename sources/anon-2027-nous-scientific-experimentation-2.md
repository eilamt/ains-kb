---
type: source
title: "NOUS: Scientific Experimentation as Methodology for AI Coding Agents"
citekey: anon-2027-nous-scientific-experimentation
authors: []
year: 2027
kind: paper
container: "International Conference on Software Engineering (ICSE 2027) — submitted, double-blind review"
publisher:
doi:
url:
lang:

verified: true
holdings: [pdf]
file: icse2027-paper153.pdf

people: []
tags: [ains-concept, harness, validation]
missions: [keynote]

status: read
added: 2026-08-13
---

## Why it matters to me
nous.

## Notes

Claude: Read from the submitted PDF. **This supersedes my earlier reconstruction from the public repo — several details differ, and in every case the paper is ahead of the repo documentation.**

**Corrections to what the repo docs say.** Seven arm types, not five: the paper adds `h-dose-response` (how does the metric scale — a sweep, and the schema rejects one with fewer than three values) and `h-tradeoff` (does the gain cost too much elsewhere). Four prediction-error categories, not three: direction, magnitude, regime, and **shape mismatch** (a different response curve than expected). And the human gates are **optional**, with an automated-approval mode for unattended runs — which resolves the apparent contradiction with the GNN post's "fully autonomous after launch." `docs/protocol.md` describes an older, smaller version of the methodology.

**One thing to reconcile in your own framing.** The paper does *not* describe the principle store as append-only. Principles are "flagged for update or pruning," their status is updated as later arms cite, confirm, or contradict them, and the store is described as one where claims "strengthen with evidence, weaken under disconfirmation, and retire when superseded." Contradictions are tracked by associating each principle with the identifiers of those it conflicts with. If the trustworthiness argument on stage rests on append-only immutability, it does not match the submitted paper.

**Architecture.** Two agent roles per iteration — designer and executor — driven by a deterministic orchestrator that makes no LLM calls and no scientific judgments. Three phases per iteration: design, execution, principle extraction. The division of labor is stated crisply and is the best one-line summary of the whole system: **"The agent supplies capability, whereas the orchestrator provides discipline."** Neither agent controls phase transitions; the orchestrator advances only after validation passes, and the agent can neither skip a phase nor revisit a completed one.

**The enforcement argument, which is the paper's core claim.** Compliance is verified externally by a separate process rather than self-reported. Every artifact is typed and schema-checked before the loop may advance; the schema forbids unknown fields, requires every arm to carry prediction + mechanism + diagnostic, and cross-checks per-arm-type requirements. A hard failure blocks the transition until the agent reads the diagnostics, repairs, and resubmits — so validation drives iterative self-correction rather than acting as a one-shot check. Beyond structure, the validator enforces **spec fidelity**: the campaign declares which parameters must stay fixed, and any bundle whose verified parameters deviate is hard-failed. Because validation runs *before* each gate, only schema-valid artifacts ever reach human review. The framing: "The expert can judge scientific soundness; the validator enforces mechanical compliance."

**Why each arm field exists** — worth quoting almost verbatim, it is unusually well-argued. A *prediction* stated in advance "is what separates a finding from a rationalization, since without a pre-registered prediction the agent can explain any observed result after the fact." A *mechanism* is required because "a confirmed prediction with no mechanism teaches only correlation," and mechanism is what enables generalization to untested conditions. A *diagnostic* stated before the outcome is known "transforms a simple refutation from a dead end into a meaningful start of the next iteration." Note the paper cites Kerr on HARKing directly — the pre-registration framing is explicit, not implied.

**Evaluation: 17 campaigns** (not 18), five domains, ~130 iterations total, 200+ accumulated principles, campaigns ranging 3 to 35 iterations. All on Claude Code with Opus 4.6 designer and Sonnet 4.6 executor.

**Campaigns absent from the rest of this catalog, several of them strong keynote material:**
- **#2 GPU transfer debug (11 iterations).** GPU-to-GPU KV-cache transfer achieving 500 MB/s against 10 GB/s hardware. Two faults found: a UCX config variable using Linux network interface names instead of InfiniBand transport device names, causing silent fallback from RDMA to TCP; and only 2 of 8 NICs in use, fixed by `UCX_MAX_RNDV_RAILS=8`. Restored to 10.3 GB/s. The instructive part is the *wrong* predictions — an ablation predicting UCX would auto-discover the InfiniBand devices produced a magnitude error (throughput stayed at 220 MB/s), establishing that auto-discovery is broken; a direction error at iteration 9 revealed the *prefill* node's PCIe topology matters, not the decode node's. This is the cleanest "two wrong predictions produced two actionable findings" story in the paper.
- **#16 real-cluster flow control (35 iterations).** −54% critical TTFT under saturation, but **+66–132% harm in a near-saturation band invisible to the simulator.** This is the same regression the Part II blog reports as +18/+31% on interactive chat; the paper's numbers are larger. Reconcile before quoting either.
- **#13 SSD-tier transfer.** Refuted: the meter works, but throttling SSD transfers adds 83.8 ms for all tenants — "preventing an incorrect production recommendation." The cleanest example of a negative result with direct engineering value.
- **#12 fairness transfer.** Refuted with a direction error: a fairness principle does not transfer to bursty arrivals. Principles have regimes; this is the proof.
- **#5 KV-cache fairness**, 4.9× lower inter-tenant disparity across 75 configurations — this is the Residency/memorytime work.
- **#17 SSD-to-GPU:** NVMe queue depth was the bottleneck; 8 → 64 took throughput from 2.4 to 6.0 GB/s.
- Also #7 prefill-decode validation (formula accurate to ~1% at moderate rates, diverges 29% at 120 req/s — a regime boundary the expert's constant-cost assumption missed), #8 concurrency scaling (optimum in ≤8 evaluations vs 30 exhaustive), #10 multi-objective search, #14/#15 saturation detectors.

**Admission control number, definitively: 37–98% P90 TTFT reduction for critical requests**, validated on a real H100 cluster, merged into llm-d. Not 42%, not "up to 97%." Three different figures for this one result are circulating across the blog, the all-hands deck, and internal materials — the paper is the one to cite.

**RQ3, the controlled comparison — this is the evaluation to build a slide around.** Four variants: L0 (single agent session, no methodology), L1 (adds a scientific-reasoning preamble), L2 (N sequential sessions with the L1 preamble and feed-forward context), NOUS. Scored 0–110 on an 11-metric rubric by an independent GPT-5.5 agentic judge with shell access to recompute reported numbers, blind to variant identity, three seeds. Baselines got **Opus 4.6 throughout — a stronger model than NOUS's own executor.**

Result: L0 43.1 → L1 55.0 (+11.9) → L2 68.5 (+13.5) → NOUS 92.8 (+24.3). NOUS wins all 15 campaign-seed judgments without exception, and is far more consistent (87–99 range against L0's 16–60). Largest gains are exactly where enforcement bites: pre-registration 5.7→8.9, error correction 6.1→8.7, provenance 4.2→7.3, auditability 5.0→8.1.

Two supporting findings that pre-empt the obvious objections:
- **Cost parity.** L2 $29.82, NOUS $28.96. "The quality gains come from methodology and enforcement, not from additional compute."
- **The stronger-model ablation, which you should not omit.** Re-running all baselines on Opus 4.7 lifted every one — L0 43.1→61.6, L1 55.0→78.7, L2 68.5→85.3 — yet the best baseline still trailed NOUS on every campaign, average margin +8.3. This is the direct answer to "won't the next model make the harness unnecessary?" The margin narrows from +24.3 to +8.3, which is worth saying honestly, but it does not close.

Note L1's near-zero pre-registration score (0.6→1.5): "telling an agent to form hypotheses does not guarantee it records them before executing." That single sentence is the enforcement thesis in miniature.

**Related work positioning.** Distinguishes itself from coding-agent harnesses (RepairAgent, FlowGen — "construction loops terminate when code passes tests; scientific loops terminate when understanding accumulates"), from SBSE/GI/APR ("NOUS maintains no population, applies no variation operators, and optimizes no scalar fitness"), and from LLM-guided code evolution. **Engram (Karimi et al., CAIS '26) is explicitly subsumed by the L2 baseline** — so that comparison is already made, not pending. Glia (Hamadanian et al., CAIS '26) is cited but not compared against. The stated complementarity is a good line: "after search discovers an improved variant, NOUS can investigate why it improves, where the gain breaks down, and what principles should carry forward."

**Threats to validity, useful for the honest-limitations slide.** Requires a programmatic interface — GUI-only apps and services without local reproduction are out of scope. Requires quantitative outcomes; correctness properties and security vulnerabilities would need schema extensions. Single generation per variant — the three seeds vary only the *judge*, not the underlying investigation, so the reported spread measures evaluation reliability, not run-to-run variance. Human gates were disabled for the controlled comparison. And the memorization concern on DIMACS is addressed head-on rather than waved away.

## Quotes
<!-- Always blockquoted, always with a locator. -->
