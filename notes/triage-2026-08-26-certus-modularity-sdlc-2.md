---
type: triage
source-export: raw/claude-exports/2026-08-26-keynote-scoping.md
created: 2026-08-26
missions:
  - keynote
---

# Triage — Certus, modularity, and the new SDLC

## Provenance — resolved

`source-export:` above points at `raw/claude-exports/2026-08-26-keynote-scoping.md`.
Confirm that file exists before running `/promote`; the `provenance:` pointers
it writes will dangle otherwise.

**One exception.** The meng-jackson passage in candidate 1 did *not* originate in
that conversation — it was already in the source file. It is attributed inline
and must not receive the export provenance pointer.

---

## 1. Summary

Working session scoping a systems-conference keynote. The knowledge base's
thirteen IBM sources were catalogued from the published blog repo, the public
Nous implementation, and five uploaded internal artifacts. The talk was then
narrowed to two deep-dive use cases — llm-d as a self-evolving system, and
Certus as an exemplar of a new SDLC built on composition and verification
rather than optimization search.

---

## 2. Candidate sources

**No new stubs needed.** Every work below is already catalogued and
`verified: true`. Nothing goes to `sources/_unverified/` from this triage.

| Source | Already in repo | Role in the candidates below |
|---|---|---|
| `waddington-2026-certus-storage` | yes | primary evidence |
| `anon-2026-certus-review` | yes | internal deck; the self-proving admission |
| `meng-jackson-2025-legible-software` | yes | modularity renaissance argument |
| `wang-2025-prometheus-dissect-restore` | yes | decompose → verify → recompose |
| `he-miller-2026-speed-cost-quality` | yes | complexity +41.6%, persistent |
| `liu-2026-debt-behind-ai-boom` | yes | code smells dominant debt category |
| `ahmad-2026-comprehension-debt-genai` | yes | debt in team cognition |
| `alenezi-2026-human-ai-collaboration-se` | yes | Naur theory-building |
| `alenezi-2026-rethinking-se-agentic` | yes | verification as rate-limiting |
| `gullstrand-2026-trust-calibrated-code-review` | yes | no confidence signal |
| `ye-2025-verina-verifiable-code-generation` | yes | hackable auto-generated specs |
| `bursuc-2025-vericoding-benchmark` | yes | NL descriptions don't help |
| `farrag-2026-productivity-reliability-paradox` | yes | non-determinism → spec |
| `cito-bork-2025-lost-in-code-generation` | yes | code as post-hoc artifact |

---

## 3. Candidate notes

**Note before you decide.** The linkage is not entirely absent — you already
made it, in a `## Tamar's note` section inside
`sources/meng-jackson-2025-legible-software`. Per your answer to Q4 that line
stays where it is; candidate 1 quotes it with attribution, and a back-pointer
is added by hand after promotion.

**Candidates 1 and 4 both merge into `why-modularity-is-important`** and are
appended in that order. See the pre-flight checklist at the end.

---

### 1. merge -> why-modularity-is-important
decision: merge -> why-modularity-is-important
one-line: (not used by /promote on a merge — kept as a drafting note only)
draft-one-line: Certus is an existence proof that AI-generated code at volume does not have to degrade, if modular boundaries and specifications are enforced structurally rather than left to the agent.
tags: [mdd, sdd, use-case]
people: []
attach-to: [[genai-failures]], [[sources/waddington-2026-certus-storage]], [[sources/meng-jackson-2025-legible-software]], [[sources/he-miller-2026-speed-cost-quality]]
manual-after-promote: /promote does NOT create wikilinks on a merge. Add these by
  hand under `## Connects to` in `notes/why-modularity-is-important`:
  [[sources/waddington-2026-certus-storage]], [[sources/anon-2026-certus-review]],
  [[sources/wang-2025-prometheus-dissect-restore]], [[genai-failures]].
  Also add `See [[why-modularity-is-important]]` under `## Notes` in
  `sources/meng-jackson-2025-legible-software`.

> Certus is a hyper-specialized storage system for KV Cache. Small team of 4
> developed 69K SLOCs of Rust code in less than 5 months. Zero lines of code
> hand-written – Spec Driven Development. Focus on assurance and
> human-maintainability.

— `Certus_Review_Priya_JUL2026.pptx`, slide 3

> Component-based composition solves a practical problem in system synthesis:
> generating correct, efficient low-level code from high-level descriptions is
> hard. [...] This means that the coding agent's inferencing context can be
> limited to a system-wide view that abstracts over the details of internal
> component implementations.

— `waddington-2026-certus-storage`, §5.2

> ery similar to approach in Certus but goes a step further with the
> synchronization service (but specification can be limiting)

— your own reaction, already in `sources/meng-jackson-2025-legible-software`.
  Pre-dates this conversation: do **not** attach the export provenance pointer
  to this passage. It stays in the source file; this note quotes it.

*Assistant's framing, not hers:* the literature converges on a diagnosis —
complexity up 41.6% and persistent, code smells as the dominant debt category,
comprehension debt accumulating where static analysis cannot see it — and every
remedy proposed is an attempt to restore structure the AI erodes. Certus ran at
high volume and did not produce that outcome. Uncontrolled and n=1, but it is a
data point on the open gap you flagged: nobody has connected modularity
discipline to long-horizon agent outcomes.

> agreed. The Certus use case addresses many of the issues identified by
> literature. It is an examplar of the emerging SDLC.

— Tamar, on review of this triage

---

### 2. specification-as-the-durable-artifact.md
decision: promote
one-line: If Naur is right that the durable asset is the theory rather than the source text, then making the specification the authoritative artifact is not a process preference but the only way the theory survives machine-speed code churn.
tags: [sdd, mdd, sdlc]
people: []
attach-to: [[what-we-need-ai-to-do-for-sw-engineering]], [[sources/alenezi-2026-human-ai-collaboration-se]], [[sources/waddington-2026-certus-storage]], [[sources/cito-bork-2025-lost-in-code-generation]], [[sources/farrag-2026-productivity-reliability-paradox]]

> This is the best explanation of why we are moving to spec-driven or
> intent-driven programming.

— your reaction on `sources/alenezi-2026-human-ai-collaboration-se`

> Naur deepened the point by reframing programming as theory building: the
> durable asset of a software project is not its source text but the shared
> mental model of the problem and solution domains held by the people who build
> it, a model that decays when those people leave.

— `alenezi-2026-human-ai-collaboration-se`

> Crucially, the specification is a live document. It evolves together with the
> system and must always be kept in sync with it. This consistency can be
> ensured by treating the specification and not the code as the source of
> authoritative truth.

— `eilam-2026-ai-native-systems-autonomous-evolution`, §3.1

*Tension to record in the note:* Cito and Bork argue the opposite direction —
that code has become the primary artifact and models should be recovered
*post hoc* by reverse engineering. Certus and the AINS vision post both put the
spec first. Both cannot be the general answer; the difference may be greenfield
versus brownfield, which is exactly the llm-d / Certus split in the talk.

> Indeed the difference is GREEN vs. BROWN. This tension goes away if you
> consider that code and spec co-evolve, and always need to be kept in sync.
> The question is an epistemological one - what came first. In brown field it
> is the code, and the spec is created based on it by reverse engineering, it
> is just a bootstraping mechanism. Once a spec is created, keeping them in
> sync at all times is how the process works (of course generating spec from
> code is a non-trivial unsolved problem).

— Tamar, on review of this triage. **This resolves the tension rather than
  recording it** — it is a position, not a note about a source, and it is the
  strongest candidate for the note's one-sentence statement.

---

### 3. the-self-proving-problem.md
decision: promote
one-line: When the AI writes the specification, the code, and the proof, formal verification certifies agreement between three artifacts from one source rather than correctness against intent.
tags: [verification, genai-failure]
people: []
attach-to: [[genai-failures]], [[sources/anon-2026-certus-review]], [[sources/ye-2025-verina-verifiable-code-generation]], [[sources/bursuc-2025-vericoding-benchmark]], [[sources/wang-2025-prometheus-dissect-restore]]

> Using Gen-AI to apply formal verification and reduce the burden has potential
> but proving the chain-of-transformation correctness (spec + code properties
> abstract code proofs/test harness) is tricky; its sort of self-proving – we
> are looking to applying adversarial alternative LLM (e.g., Codex) to attack
> this issue

— `Certus_Review_Priya_JUL2026.pptx`, slide 16

> CLEVER's authors note that FVAPPS used an LLM to auto-create formal
> specifications for 4,715 problems, and that those specifications are often
> easily hackable, with verification correctness guarded by a layer of test
> cases.

— assistant summary in `sources/ye-2025-verina-verifiable-code-generation`

*Why this is worth its own note rather than a line in `genai-failures`:* the
other failure modes in that note are things the AI does wrong. This one is a
property of the *architecture* — it holds even when every component works
exactly as designed. Two independent lines land on it, one internal and candid,
one external and empirical, and the adversarial-LLM mitigation is an open
research direction rather than a known fix.

*Also note the tension with your own published claim,* which should be recorded
honestly: the Certus blog argues that a generated system carrying Spin, Kani,
and Creusot certificates is "more trustworthy than a hand-written system without
any of them." The deck says the chain is sort of self-proving. Both are
defensible. They should not appear in the same talk unacknowledged.

> we absolutely need to acknowledge the tension. Certus is a work in progress.
> We hypothesis that we need validation. We experiment with different
> techniques. We have partial results, and there are serious threats to the
> approach which we need to investigate, potentially enhance as future work
> with adverserial validation. We are not claiming we solved everything. We
> are reporting about where we are. what we learned and we need to examine it
> critically.

— Tamar, on review of this triage

---

### 4. merge -> why-modularity-is-important
decision: merge -> why-modularity-is-important
one-line: (merge candidate — no new note; extends the existing `## Tensions` section)
tags: []
people: []
attach-to: [[why-modularity-is-important]]

Your existing note already argues the position:

> the AI code which is generated is NOT modular, it increases in complexity.
> But what we need is modularity for multiple reasons: reduce context, control
> scope, have readable code, that is easier to continue to evolve and maintain.
> Modularity is more important, not less important because of AI.

— `notes/why-modularity-is-important`, `## Tensions`

What it lacks is the mechanism and the evidence. Two additions proposed:

> By generating compositions of proven components rather than raw code, Certus
> inherits the correctness and performance properties of the component library.

— `waddington-2026-certus-storage`, §5.2

> The key insight behind Prometheus is that complex programs can be made more
> amenable to AI-based automated reasoning by first transforming them into
> semantically equivalent, modular components.

— `wang-2025-prometheus-dissect-restore`

*Assistant's reading:* these are the same move in two directions. Certus builds
modular so the agent can reason; Prometheus refactors *into* modular so the
verifier can reason, then restores the original structure. Both treat modularity
as a precondition for machine reasoning rather than as a human-readability
concern. That is the specific claim your note is missing.

> indeed, and very important to note that modularity is important for multiple
> reasons.. and human readability is only one reason

— Tamar, on review of this triage

---

## 4. Attachments to existing material

Grepped. Current state:

- `notes/why-modularity-is-important` — links to meng-jackson, he-miller,
  cervantes-kazman. **No link to any Certus source, Prometheus, or the
  verification cluster.** This is the structural gap.
- `notes/genai-failures` — links to tang, he-miller, meng-jackson,
  cervantes-kazman. No verification links.
- `notes/what-we-need-ai-to-do-for-sw-engineering` — status `seed`, has an
  empty `[[ ]]` dangling link and no TODO sentence written yet. Candidate 2
  attaches here and would give it its first real connection.
- **No note anywhere in the repo mentions Certus.** Confirmed by grep.
- `missions/keynote/index.md` — `Goal`, `Outline`, `Threads` all empty. All
  four candidates carry `missions: [keynote]` and should surface there once
  the outline exists.

**Backlinks — read carefully, this changed.** `/promote` creates backlinks only
for `promote` decisions. Candidates 1 and 4 are now merges, so `/promote` will
append their passages to `why-modularity-is-important` under a `## Provenance`
section (which that note does not yet have — the command will create it) and
will create **no links at all**. Only candidates 2 and 3 get wired
automatically.

Net effect: the structural gap named above — no note linking to Certus,
Prometheus, or the verification cluster — is **not** closed by running
`/promote`. It closes when you add the `## Connects to` lines listed in
candidate 1's `manual-after-promote` field.

---

## 5. Questions for her

1. **Is candidate 1 a note or an expansion of `why-modularity-is-important`?**
   Your `CLAUDE.md` says prefer extending to creating. The argument for a
   separate note is that "Certus is a counterexample" is a claim about
   *evidence*, while the existing note is a claim about *principle*. The
   argument against is that you would then maintain two notes that cite each
   other constantly. 
   
   ANSWER (transcribed from conversation, not typed by her): leave the line where
it is. Candidate 1 quotes it with a pointer back — it should be in both. The
back-pointer into the source file is manual; see candidate 1's
`manual-after-promote` field.

The header drift in that file (`## Claude Summary` / `## Tamar's note` instead
of `## Notes` — the only one of 43 sources that does this) is a separate issue,
deferred to the next `/review` pass.MAKE IT AN EXPENSION. 

2. **Does `sdd` stay a separate tag from `mdd`?** Currently `sdd` has one use
   and `mdd` has four, and `/review` flags singleton tags for removal.
   Candidates 1 and 2 would take `sdd` to three. Worth deciding deliberately
   rather than letting the review command decide.
   
   ANSWER (transcribed from conversation, not typed by her): leave the line where
it is. Candidate 1 quotes it with a pointer back — it should be in both. The
back-pointer into the source file is manual; see candidate 1's
`manual-after-promote` field.

The header drift in that file (`## Claude Summary` / `## Tamar's note` instead
of `## Notes` — the only one of 43 sources that does this) is a separate issue,
deferred to the next `/review` pass.MERGE SDD and MDD

3. **Candidate 3 names a tension with your own published blog post.** Do you
   want that recorded in the KB, or handled only in the talk? It affects how
   the note is written.
   
   ANSWER (transcribed from conversation, not typed by her): leave the line where
it is. Candidate 1 quotes it with a pointer back — it should be in both. The
back-pointer into the source file is manual; see candidate 1's
`manual-after-promote` field.

The header drift in that file (`## Claude Summary` / `## Tamar's note` instead
of `## Notes` — the only one of 43 sources that does this) is a separate issue,
deferred to the next `/review` pass.the tension is fine to record in KB

4. **Should the meng-jackson `## Tamar's note` line move?** That file uses
   non-template headers (`## Claude Summary`, `## Tamar's note` instead of
   `## Notes`). 
   
   If the Certus linkage becomes a note, that line is its seed and
   arguably belongs there, with the source file normalized back to the template.
   
ANSWER (transcribed from conversation, not typed by her): leave the line where
it is. Candidate 1 quotes it with a pointer back — it should be in both. The
back-pointer into the source file is manual; see candidate 1's
`manual-after-promote` field.

The header drift in that file (`## Claude Summary` / `## Tamar's note` instead
of `## Notes` — the only one of 43 sources that does this) is a separate issue,
deferred to the next `/review` pass.

---

## 6. Pre-flight checklist before `/promote`

1. `raw/claude-exports/2026-08-26-keynote-scoping.md` exists.
2. All four `decision:` lines filled — currently:
   `merge -> why-modularity-is-important`, `promote`, `promote`,
   `merge -> why-modularity-is-important`.
3. Decide the `sdd` / `mdd` merge (Q2) — or defer it to `/review`. Not blocking.

## 7. After `/promote`

1. Write the one-sentence statements for candidates 2 and 3. `/promote` leaves
   a TODO line; it will not write them. For candidate 2 your GREEN/BROWN comment
   is already most of the answer.
2. Add the `## Connects to` links listed in candidate 1's
   `manual-after-promote` field. **This is the step that actually closes the
   structural gap** — the merge alone does not.
3. Add `See [[why-modularity-is-important]]` under `## Notes` in
   `sources/meng-jackson-2025-legible-software`.
4. `/verify-refs`, then `/review`, then commit.
