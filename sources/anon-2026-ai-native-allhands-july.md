---
type: source
title: "AI Native Systems All-Hands — July 2026"
citekey: anon-2026-ai-native-allhands-july
authors: []
year: 2026
kind: talk
container: "IBM Research, Midyear 2026 All Hands — marked IBM Confidential"
publisher:
doi:
url:
lang:

verified: true
holdings: [pdf]
file: AI-Native-Systems-allhands-July-2026.pptx

people: []
tags: [ains-concept]
missions: [keynote]

status: read
added: 2026-08-13
---

## Why it matters to me
Self-driving cars angle for AI native systems.

## Notes

Claude: Presented by Priya Nagpurkar, VP AI-native Systems, IBM Research. **Marked IBM Confidential throughout** — most of the content here is org-level achievement reporting that has no place in an external keynote. Two or three things are genuinely useful.

**Note on the "Why it matters" line above: there is no self-driving-car content in this deck.** That analogy appears in Hassan et al.'s agentic SE roadmap (arXiv 2509.06216), flagged in [[sources/hassan-2025-ai-native-se-30]]. Either the memory is of a different deck or it merged with the Hassan note. Worth checking before building a slide on it — and note that borrowing the analogy means borrowing it from the framing this work needs to differentiate itself against.

**The one framing worth taking.** Slide 2 sets up a `+AI` / `AI+` contrast: **"AI helps us work better"** versus **"Systems innovations with AI as workforce."** That is a tighter compression of the AI-as-tool vs AI-as-primary-agent distinction than the vision post's prose, and it survives translation to an external audience because it says nothing proprietary. Five target areas: AI for chip design; AI-native compilers and kernels; self-evolving distributed inference; domain-specific storage for inference; vulnerability detection and remediation (Lightwell).

**A third version of the admission-control number.** This deck says "TTFT p90 decreased by up to 97%, E2E latency decreased by up to 50%." The blog says up to 97% TTFT p90 and 27–50% E2E. The ICSE paper says 37–98% P90 TTFT. Three sources, three phrasings, one result. Cite the paper.

**Results here that are not catalogued anywhere else:**
- **Capacity planning surpassing NVIDIA's AIConfigurator** — 1.8× higher throughput at the same or lower cost, full-stack exploration of 100+ llm-d knobs, 15× fewer evaluations for near-optimal coverage. This is a named-competitor comparison and the only one in the corpus. Almost certainly the most quotable systems result available, and it is not in any blog post.
- **Spyre kernels**, described as a factory: "from months to enable a new model on Spyre to an automated factory," targeting automatic high performance for 80% of kernels, with a convert → test → evolve methodology. The Hugging Face Adapters pipeline is drawn as a concrete loop — introspect HF config, classify lineage, generate adapter from template, CPU accuracy gate against greedy-token match on stock HF, with a self-correct loop on failure — powered by a Spyre knowledge base. Current coverage: adapters support 40% of the top 1000 models. This is a working instance of the "agent factory" pattern and the `agent-factory-pattern` tag in the vocabulary has zero uses; it belongs here.
- **AI for Chip Design**: Agent Factory HLS applied to belief propagation for quantum error correction, ~10× speedup over baseline HLS optimization on a bivariate-bicycle [[18,4,3]] code, with hand-tuned RTL comparison in progress. ICLAD '26 presentation.

The 1H26 achievements slide lists BLIS, Nous, and Spotlights together as "Principles & Design of AI Native Systems" — the first place the three appear as one program rather than separate projects. Useful for how to structure the talk's middle.

Everything else — Z/Spyre/Telum integration figures, llm-d CNCF donation, agent security and Kagenti work, storage and networking releases — is org reporting outside the keynote's scope.

## Quotes
<!-- Always blockquoted, always with a locator. -->
