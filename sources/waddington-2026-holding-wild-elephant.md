---
type: source
title: "Holding on to the Wild Elephant"
citekey: waddington-2026-holding-wild-elephant
authors: [Daniel Waddington, Tamar Eilam, Nara Batsoyol]
year: 2026
kind: blog
container: "Draft — unpublished, August 2026"
publisher:
doi:
url:
lang:

verified: true
holdings: [pdf]
file: Certus__Holding_on_to_the_Wild_Elephant-3.pdf

people: []
tags: [use-case, sdd, verification, human-ai-collaboration]
missions: [keynote]

status: read
added: 2026-08-27
---

## Why it matters to me

This addresses the new SDLC portion of the keynote. 
## Notes

Claude: The Certus methodology paper, with no performance numbers in it at all — which
makes it the primary source for the composition-and-verification half of the talk,
ahead of both [[sources/waddington-2026-certus-storage]] and
[[sources/anon-2026-certus-review]]. Several things here appear nowhere else in the
catalog.

**The core claim, stated more sharply than anywhere else in the corpus.** The oldest
problem in software is that code grows faster than understanding, and the mental model
is "the most valuable and most fragile artifact in software development." Every
industry answer — modular design, typed interfaces, review, tests, architecture
documents — was an attempt to externalize it, and they worked imperfectly *because the
developer was always the primary agent*: understanding and code came from the same
human mind, and that coupling, however imperfect, kept them tethered.

> LLM-based agentic coding did not just make developers faster. It severed the coupling
> entirely. For the first time in the history of software, code can exist without
> anyone having engineered it.

That is the best single sentence available for the problem half of the keynote, and it
reframes the whole degradation literature: the gap between code and mental model "used
to grow at the pace of a team's capacity to absorb complexity" and can now grow
arbitrarily wide, arbitrarily fast. Note this is a *structural* claim, not a claim
about model quality — explicitly "not a criticism of the technology," but a description
of what correctness requires: global reasoning no local generation step can supply.

**"Mutual mind" is the organizing concept and it is new.** Theory of Mind from
cognitive science — the capacity to model another agent's beliefs and intentions — is
what makes high-bandwidth collaboration possible; without it two capable parties talk
past each other, each reasoning from a model the other cannot see. Applied to
human-AI collaboration: a developer prompting without a shared representational layer
has intent, the agent has capability, and there is no mutual mind connecting them.
The result is "code that satisfies the literal request while violating the unstated
assumptions the developer would have recognized as obvious." Spec-driven development
is framed as the first step toward building that mutual mind deliberately, and the
whole methodology as the rest of it. This connects directly to the orphaned
[[mind-theory-of-computation]] note.

**Four observed failure modes, from building Certus rather than from the literature.**
Each is worth more than an equivalent citation because it is first-hand:
1. *Breaking design principles.* Cohesion and coupling explained properly, then: "In
   our experience, Claude does not always adhere to these principles. Making broad
   changes (a high blast radius) and leaking functions and state outside of
   well-defined interfaces are often acceptable strategies for Claude: the agent wants
   to get the job done, with little concern for how."
2. *Defying physical hardware limits.* The agent reports measurements the hardware
   cannot produce. Concrete: Claude claimed hundreds of GB/s from an 8×SSD array whose
   ceiling under perfect scaling is ~48 GB/s (6 GB/s per device, 128 KiB random reads,
   PCIe 4.0). Root cause named precisely — "the agent reasons about software in a
   vacuum. It has a rich model of code and no model at all of the physical machine."
3. *Model bias*, with a worked example far better than the deck's abstract version.
   Claude chose peer-to-peer DMA (SSD→GPU direct) over a bounce-buffer path through
   DRAM, because GPU Direct is heavily marketed as a storage must-have — not because it
   weighed the alternatives. The bias is statistical and *invisible in the output*:
   "the code compiles, the rationale reads plausibly, and only a developer who
   understands the broader architecture would notice that the 'obvious' choice is the
   wrong one." Key observation: the bias surfaces only in the absence of overriding
   context, so the fix is supplying context that outweighs the prior, not fighting the
   training.
4. *Overfitting to the tests.* A fix that passes single-client single-threaded tests
   will fail for multiple clients because the locking and atomicity were never needed
   to pass.

**Four countermeasures, mapped one-to-one onto those four problems** — which is why
this reads as a methodology rather than a list of practices. Component architecture
counters principle erosion; a hardware knowledge base holds the agent to physics;
deliberate context and curated knowledge bases counter statistical defaults; formal
verification counters skin-deep correctness.

**The hardware knowledge base is new detail.** An *inspection agent* runs before any
design or optimization agent and measures rather than assumes: NVMe throughput and
IOPS at representative block sizes (fio), PCIe link bandwidth (lspci), network
bandwidth and latency (ib_perf), DRAM bandwidth (Intel mlc), and DMA throughput on the
paths that matter — GPU-to-CPU (gdrcopy_copybw) and GPU-to-SSD (custom tool). Measured
properties are injected into every design context as hard boundaries and checked
against reported results. It works in the forward direction too: knowing real
per-device and per-link limits tells the agent how many SSDs are needed to saturate a
NIC. "The knowledge base turns the physics of the machine into another part of the
shared model."

**The knowledge base has four entry types**: design patterns curated from literature
and reference implementations; component specs recording interfaces, data flows, and
invariants; verified properties established by the verification pipeline; and
third-party library/API documentation (SPDK, libibverbs, vLLM). Authored by the
developer or drafted by a knowledge-curator agent, reviewed before use, kept current,
and selected into a working agent's context by task scope.

**Four verification channels, not three.** The published blog describes Spin, Kani,
and Creusot. Here the pipeline is: (A) functional correctness — generate abstract code
for Creusot; (B) bounded model checking — instrument concrete code with harnesses for
Kani and **Loom** (new to this document); (C) concurrency — generate a Promela model
for Spin; (D) targeted runtime tests for properties proof cannot reach. Routing is by
the nature of the property. The translation mechanics are described concretely: for
Creusot the agent reads the implementation and extracts key correctness properties
*rather than transliterating the code*, strips what cannot be reasoned about (HashMap,
Arc), reduces to pure functions, then converts. For Kani and Loom it replaces
unsafe/FFI with safe stubs, finds hot-spots of checkable properties, and writes
harnesses using `kani::any()` and `kani::assume()`.

**§3.5.1 is the most important section for the keynote, because the self-proving
problem is now stated publicly *and* has a validated mitigation.** The framing is
sharper than the internal deck's: soundness depends on correctly transforming specs and
code into checkable models, and "without assurance of translation, the model checkers
are verifying code that does not exist." Then: "we can't ask an agent to check itself
and expect it to have newly found levels of oversight or correctness (well, we can, but
only so far)."

The mitigation has moved from aspiration to practice. Certus employs a *different*
coding agent (Codex) to independently cross-check translation source against target —
and, critically, they validated the cross-checker itself by building a systematic
method of **poisoning** code and specifications to create deliberate source/target
mismatches, then confirming all poison items were caught. That is an evaluated
countermeasure, not a plan, and it materially changes what
[[the-self-proving-problem]] should say.

**Two citations not in the catalog.** Osborn, "AI didn't make programming easier. It
just made it differently difficult," CACM 2026 (doi 10.1145/3795534) — used for the
mental-model rebuild cost, and squarely in the pessimistic-community literature. And a
newer Kani reference: Delmas et al., ASE 2026 Industry Showcase, arXiv 2607.01504,
which differs from the VanHattum ICSE 2022 citation used in the published Certus blog.

**Number to watch.** The opening scenario describes an 80,000-line Rust storage system;
that is a hypothetical framing device, not Certus. Certus is 69K SLOC per
[[sources/anon-2026-certus-review]]. Do not conflate.

## Quotes
<!-- Always blockquoted, always with a locator. -->
