# AI Native Systems Keynote — Scoping and Knowledge Base Work — Conversation Transcript

**Date:** August 2026
**Context:** Working session preparing a systems-conference keynote on AI Native Systems, based on IBM Research work. Covers ingestion of the `ains-kb` knowledge base from GitHub, retrieval and cataloguing of the team's own published and internal material, correction of several inconsistent figures across sources, narrowing the talk to two deep-dive use cases (llm-d and Certus), and a triage proposal for the missing Certus–modularity linkage. Claude's tool calls and their outputs are not reproduced; only the conversational turns are.

---

## Tamar

Hi Claude. I have to work on a keynote to be delivered in a systems conference. 

The topic is AI Native Systems and it is based on my team's work in IBM.

In order to prepare I carefully worked on a knowledge base. 

The knowledge base includes different types of library assets that are associated with semantic tags. 

Some library items represent my research into academic papers in conferences such as ICSE that describe the monumental shift in SDLC and the challanges in using AI for code. 

Some library items represent our work in IBM. 
There are presentations, blog entries, and academic papers (submitted but not published) - the important one is NOUS. 

I first want you to consume the knowledge base from Github repo here: https://github.com/eilamt/ains-kb

Then we can discuss the structure.

---

## Claude

I've cloned and read the whole repo — CLAUDE.md, index, templates, all 43 source files, the four notes, the tag vocabulary, and the mission skeleton. I haven't written anything; CLAUDE.md is clear that notes, missions, and people are yours and my default output is `inbox/`, so I've kept everything in this conversation.

**What's actually in there**

43 sources: 27 papers, 10 blogs, 3 articles, 3 decks. They split into two populations of roughly 30 external and 13 IBM. The external set clusters cleanly by tag — sdlc (10), verification (7), genai-failure (5), validation (5), human-ai-collaboration (4), mdd (4). The IBM set is NOUS, the Residency/memorytime JACM submission, eight blog posts (the two AINS concept posts, scientific-method-on-code, both simulation-to-production posts, the two BLIS posts, Certus storage, discovery-easy-composition-hard, the BAIR K-Search post), and three decks.

Four notes: genai-failures and why-modularity-is-important are developing and genuinely good; mind-theory-of-computation and what-we-need-ai-to-do are seeds.

**The one thing you should know before we talk structure**

There's a sharp asymmetry. The external literature is *thoroughly* digested — real summaries, your "TE:" reactions doing analytical work, verbatim quotes with blockquotes. Your own work is catalogued but not digested. The "Why it matters to me" fields read: "nous.", "certus.", "spotlight.", "kernals.", "storage use case." NOUS — the one you flagged as important — has empty Notes and Quotes sections. And since `library/` is gitignored, the PDF isn't in the repo, so I can't read it either.

For a keynote about *your team's work*, that inversion is the problem. Right now the KB can argue brilliantly about why AI-assisted coding degrades systems, and can barely say a sentence about what you built instead.

Two structural symptoms of the same thing: only 6 of 43 sources are linked from any note (37 orphans), and `agent-factory-pattern` and `harness` are in the tag vocabulary but used zero times — you created the tags for the NOUS material and never wrote the notes.

**The argument that's already latent**

Reading across your TE reactions, a spine is visible: the measured paradox (velocity up, quality persistently down — He/Miller, Liu, Farrag, Ahmad) → the mechanism (context limits, expediency, opacity, and Tang's finding that inaccurate self-reporting and constraint violation are *rising* as a share, the failure modes with no human analogue) → verification becomes the rate-limiting activity, and human review of AI code doesn't scale because the agent gives no confidence signal → every remedy in the literature is an attempt to restore structure AI erodes: modularity, models, specs, context files, and nobody has patterns yet. All of which are remedies for AI-as-assistant.

Your turn is the pivot: stop patching the human review loop, architect the system for AI as primary agent — replace self-reporting with external enforcement, and close the loop on measurement rather than opinion. That's NOUS plus the simulation-to-production chain. The Minsky/Naur thread is the frame: what's durable is the theory, not the text.

That's my reading, not yours, and it may not be the talk you want to give.

Minor hygiene, worth thirty seconds: `grabowski-2026-spec-growth-engine` is untagged, `meng-jackson` uses off-template headers and links to a `people/daniel-jackson` file that doesn't exist, and `sources/index.md` still says "Verified: none yet" when 35 are verified.

*[Claude then presented an interactive question: "Where should we start?" with options "Keynote structure — outline the talk", "KB structure — reorganize first", "Fill the NOUS/IBM gap first", "Something else".]*

---

## Tamar

okay lets fix some of the main issues first. You must have access to our work - the presentations, the blog entries, and the PDFs. How do we fix that?

---

## Claude

Three buckets, and only one of them needs anything from you.

Let me start with the one that doesn't — the blogs are all public URLs already sitting in your source files.

*[Claude attempted a web fetch, which was blocked, then cloned the blog's GitHub Pages source repo instead.]*

That path is blocked — the fetch tool only accepts URLs that came from a search, and the blog isn't indexed. But GitHub Pages means the source is a repo, and I can reach github.com directly.

All ten posts are there as markdown — plus two that aren't in your KB at all.

Blogs: solved. Let me check what else of yours is reachable the same way.

**Blogs — fixed, nothing needed from you.** The site is MkDocs on GitHub Pages, so `AI-native-Systems-Research/ai-native-systems-research` has every post as markdown source. I have all ten, full text.

Two things fell out of that. First, there are two published posts not in your KB at all:

- `streaming-gnn-inference-agentic-harness.md` (17 June) — Nous pointed at a streaming GNN pipeline on Flink, running autonomously, recovering all seven of the paper's major findings and then extending several. That's a Nous proof point on someone else's research, and it's the most quotable validation story in the set. It's also almost certainly what your unused `harness` tag was created for.
- `blis-how-blis-learns-latency.md` (6 Aug) — the BLIS latency-prediction deep dive, including where the predictions fail.

Second, two of your entries point at full versions hosted elsewhere — the BAIR K-Search post and the BLIS physics post on inference-sim.github.io. What's in this repo for those is a 150-word cross-post stub. I can try the inference-sim repo the same way; BAIR I'd need you to paste or upload.

**Code and design docs — also fixed, and this is the real find.** Nous is public. `agentic-strategy-evolution` has a 2,700-word README plus `docs/architecture.md`, `protocol.md`, `data-model.md`, `security.md`, the methodology prompts, and the orchestrator itself. The README alone gives me the six-phase loop, the hypothesis-bundle decomposition into arms, the prediction-error taxonomy, fast-fail rules, principle extraction, and the four preconditions for when Nous applies. `ai-native-storage-certus`, `CORAL`, and `archon` are public too.

That doesn't replace the ICSE paper — I have the mechanism but not the evaluation, the 18 campaigns, the L0→L1→L2 comparison, or the framing you chose for reviewers. But it means the paper is now a gap in evidence rather than a gap in understanding.

**Only you can supply these five.** Drag them into this chat and they land somewhere I can read; I have skills for both pptx and pdf:

- `icse2027-paper153.pdf` (NOUS)
- `memorytime.pdf` (Residency)
- `AI-Native-Systems-allhands-July-2026.pptx`
- `spotlights_overview_deck.pptx`
- `Certus_Review_Priya_JUL2026.pptx`

The two papers are your own work under review, so that's straightforward. The three internal decks are your call on IBM policy — I'd note that the all-hands deck is the one carrying the self-driving-car framing you flagged, so if only one comes across, make it that.

**One thing that matters more than any of the above.** This container resets between sessions. If I read five PDFs today and we don't write anything down, we do this again next week. `library/` is correctly gitignored, so the binaries will never be in the repo — which means the `sources/*.md` files have to carry the substance themselves.

So the durable fix is to fill in the empty Notes sections on your thirteen IBM sources, using exactly the convention your external sources already follow: a `Claude:` summary paragraph, then space for your `TE:` reaction and any blockquotes. CLAUDE.md has `sources/` as mine to draft and yours to review, so that's within the working agreement — and I'd leave the "Why it matters to me" lines alone, since those are explicitly your words.

I can do the ten blog-derived ones plus a Nous entry from the public docs right now, hand them back as files, and you commit what you like. Say the word and I'll start there while you gather the PDFs.

---

## Tamar

okay lets do that...

---

## Claude

*[Claude read all ten blog posts in full, the Nous README and protocol docs, then generated the enriched source files.]*

No uploads yet — I'll work with what I have. Reading the posts in full now.

I clobbered something I shouldn't have — my script pulled the first paragraph of each note up into "Why it matters to me," which is your text, not mine. Fixing on four files.

Now the two uncatalogued posts. Author full names are inferred from blog usernames, so per your prime directive on citations these go to `_unverified/`.

Twelve files, mirroring the repo layout — drop `sources/` over `sources/`. Ten are your existing files with the Notes section filled; two are new and land in `sources/_unverified/` because I inferred the author names from blog usernames rather than reading them, and your prime directive says that's a `verified: false`. Both promote with one glance.

Your `## Why it matters to me` lines are untouched, and every Notes section ends with a `<!-- TE: -->` cue where your reaction goes.

**Four things surfaced that you need to decide on before the talk.**

The `−42%` admission-control figure in your internal materials is the *first* evolution — the linear-ramp version with four tuned thresholds that didn't port. The shipped probabilistic admitter is 24–47% simulated and up to 97% TTFT p90 on hardware. Different algorithm, better number, wrong citation.

The public Nous repo and your description of Nous don't match in three places. The repo documents two agent roles and two LLM calls per iteration; your framing has four agents. Principle `status` in the public schema is `active | updated | pruned`, which isn't append-only — and the trustworthiness argument rests on append-only. And `protocol.md` says "7-phase" in its overview then lists six. Whichever is stale, a systems audience with the repo open will notice.

Related: the GNN post says the campaigns ran "fully autonomous after launch — no hints, no intermediate corrections," while the protocol says the two human gates "cannot be bypassed." Both can be true if the gates were auto-approved, but you should know which mode each result came from before someone asks.

And the composition-barrier post is the one to think hardest about. Under an equal $20 budget an unstructured coding agent hit 16.5 GB/s and Nous completed three experiments and didn't reach the compound; Nous matched it at 16.3 GB/s only on a separate $65 run. Your team's own reading is that this was budget, not method. I'd put it on a slide rather than leave it out — a keynote that shows the case where its own framework lost buys credibility for everything else, and the recoverability finding is a genuinely interesting result independent of who won.

Still missing: the two PDFs and three decks. The Nous entry is a stand-in built from the implementation, so it has the mechanism but none of your evaluation — the 18 campaigns, the L0→L1→L2 comparison, or the framing you chose for reviewers.

---

## Tamar

*[Uploaded five files: `AI-Native-Systems-allhands-July-2026.pptx`, `Certus__Blog_June_2026.pdf`, `Certus_Review_Priya_JUL2026.pptx`, `icse2027-paper153.pdf`, `spotlights_overview_deck.pptx`. No accompanying message text.]*

---

## Claude

Both PDFs are in context. Let me get the decks.

*[Claude read the pptx skill, extracted all three decks, then rewrote four source files and appended to a fifth.]*

All five read. The ICSE paper resolves most of what I flagged — and changes several numbers.

Five files. Four rewritten from the uploads, plus an addendum to the Certus entry. The NOUS file replaces the stand-in I built from the repo — throw that version away.

**The paper resolves the discrepancies, and the repo is what's stale.** Seven arm types, not five — it adds dose-response and tradeoff. Four error categories, not three — it adds shape mismatch. And the human gates are *optional*, with an automated-approval mode, which is why the GNN campaigns could run unattended. `docs/protocol.md` documents an older, smaller methodology.

One that goes the other way. The paper does not describe the principle store as append-only. Principles get "flagged for update or pruning," and the store is one where claims "weaken under disconfirmation, and retire when superseded." If the trustworthiness argument on stage rests on immutability, it doesn't match what you submitted.

**Numbers that changed.** Admission control is 37–98% P90 TTFT reduction. Three different phrasings of that one result circulate across the blog, the all-hands deck, and internal materials — cite the paper. It's 17 campaigns, not 18. And the near-saturation regression in campaign 16 is +66–132% in the paper against the blog's +18/+31%; those need reconciling before you quote either.

**Three things you should almost certainly put in the talk that aren't in the KB yet.**

The stronger-model ablation. Re-running every baseline on Opus 4.7 lifted L0 from 43.1 to 61.6 and L2 from 68.5 to 85.3, and NOUS still won every campaign at +8.3 average margin. That's the direct answer to "won't the next model make the harness unnecessary?" The margin narrows from +24.3 — say so — but it doesn't close. Paired with the cost parity finding ($29.82 vs $28.96), you can rule out both "it's just a better model" and "it's just more compute" in one slide.

The GPU transfer campaign. 500 MB/s against a 10 GB/s ceiling, traced to a UCX config using Linux interface names instead of InfiniBand ones, causing silent fallback from RDMA to TCP. Restored to 10.3 GB/s. What makes it a keynote story is that the two *wrong* predictions each produced a finding — an ablation's magnitude error established that auto-discovery is broken, and a direction error nine iterations in revealed the prefill node's PCIe topology mattered, not the decode node's.

Spotlights. The selection-versus-execution framing is the sharpest thing in any of these files. Every tool in the space — yours included — needs a human to point and say "optimize this." Presenting Nous alone leaves the audience's obvious question unanswered.

**Two things to handle carefully.** The all-hands and Certus decks are marked Confidential and Proprietary. The AIConfigurator comparison in particular (1.8× throughput at same or lower cost, 15× fewer evaluations) is your most quotable systems result and it's internal — worth finding out what's cleared.

And the Certus deck's backup slides are more awkward than the published bake-off. The new Optimization Agent hits +86% at $2.69 in four iterations; the Coding Agent hits +86% at $12 over 152 iterations; Nous hits +84% at $65. On that task a different structure beats Nous on both cost and outcome. The deck's own conclusion — "the model isn't the bottleneck, the structure around it is" — is right, but it's arguing for a structure that isn't Nous.

Also: there's no self-driving-car content in the all-hands deck. That analogy is Hassan's, from the paper you're positioning against.

Still missing: `memorytime.pdf`. That's campaign #5 in the paper — 4.9× lower inter-tenant disparity across 75 configurations.

---

## Tamar

okay good point about certus. I will check about what can we talk about publicly.... do not worry about missing material such as GNN or Kernels. For the talk I think I want to focus on just two exemplary use cases to deep dive on. One is llm-d (a self-evolving self optimizing system) and another one certus - vertical optimization. Now, how do I work with the knowledge base now? shall I download your md files, and copy them to inbox? remind me the process...

---

## Claude

Not the inbox. Your `/promote` command would refuse these — it requires `decision:` lines and it only ever creates files in `notes/`. Sources never go through triage.

These are finished source files, and `CLAUDE.md` puts `sources/` in the "you draft, she reviews" column. So they go straight in:

**The 15 files that replace existing ones** (10 from the earlier batch + 5 from this one) drop directly over `sources/`, same filenames. Read the diffs, edit or delete what you disagree with, commit. The `<!-- TE: -->` cue at the end of each Notes section is where your own reaction goes — that part I deliberately left empty.

**The 2 in `sources/_unverified/`** — the GNN harness post and the BLIS latency post — go into that folder and stay there until `/verify-refs` runs. The only thing blocking them is the author full names, which I inferred from blog usernames. You can confirm those faster than the command can; if you'd rather just fix them by hand, set `verified: true` and move them up to `sources/`.

Then run `/review` and commit. That'll also catch the small stuff I flagged earlier — `grabowski` untagged, the dangling `[[daniel-jackson]]` link, `sources/index.md` still saying "Verified: none yet."

One note on the `harness` tag. It was unused; I've now put it on the Nous paper, the Certus review, Spotlights, and the GNN post. `agent-factory-pattern` is still unused — the Spyre kernel factory in the all-hands deck is the obvious home for it, if that survives your scope cut.

**On narrowing to llm-d and Certus.** That's a good cut, and it changes what matters in the catalog. llm-d gives you the horizontal story: one system, four campaigns, simulation to production, two upstream merges. Certus gives you vertical: one workload, a system synthesized rather than written. Together they cover both axes of the specialization argument without needing the kernel or GNN material.

But it costs you two things you were relying on.

The GNN campaign was your only result measured against a *known human answer* — the harness recovering all seven published findings and then extending them. Everything in the llm-d and Certus story is measured against a baseline the system also discovered. If someone asks "how do you know it isn't just finding what you told it to find," that campaign was the answer. The ICSE paper's RQ3 comparison partly substitutes, since the judge is independent, but it isn't the same thing.

And the Certus half now leans harder on the bake-off, because that's where Certus's methodology evidence lives — which is exactly the material where Nous loses on cost and the deck argues for a different structure. Worth deciding early whether Certus is a story about spec-driven synthesis plus formal verification (the blog and the deck's front half) or about optimization search (the backup slides). Those are different talks, and the second one competes with your llm-d half rather than complementing it.

The mission file is still empty — `Goal`, `Outline`, and `Threads` all blank. That's the natural next thing, and it's yours to write.

---

## Tamar

okay for Certus I really want to lean on the horizontal not the optimization. ie composition and verification - it is exemplar of the new SDLC

---

## Claude

That reading makes the two halves complementary instead of parallel. llm-d is evolving a system that already exists — brownfield, telemetry-driven, changes going upstream. Certus is producing one that doesn't — greenfield, spec-first, verified at birth. Together that's the whole lifecycle, which is the vision post's actual claim: dev and ops unified as one engineering discipline. Two optimization stories wouldn't have shown that.

It also disposes of the bake-off problem cleanly. The Optimization Agent, the knowledge graph, the 118-or-122 patterns, the 9-mode controller, the $2.69-vs-$65 table — all of that lives in the optimization half and is now out of scope. Nothing to defend.

**What Certus becomes evidence for.** The literature in your KB converges on one diagnosis: AI-generated code degrades on exactly the axes that make systems maintainable. Complexity up 41.6% persistently (He & Miller), code smells as the dominant debt category compounding at volume (Liu), comprehension debt accumulating in team cognition where static analysis can't see it (Ahmad). Every proposed remedy is an attempt to restore structure the AI erodes — modularity, models, specs, context files — and Mohsenimofidi's finding is that nobody has patterns yet.

Certus is the counterexample: 69K SLOC of Rust, four people, under five months, zero lines hand-written, and it didn't produce that outcome. Not because the volume was low but because the discipline was structural.

Three mechanisms, each of which answers a specific paper:

Typed interfaces and receptacles are the systems-code instance of what Meng and Jackson argue for with concepts and synchronizations, and of what Prometheus does with dissect-and-restore. The Certus line that makes it land is that component composition lets "the coding agent's inferencing context be limited to a system-wide view that abstracts over the details of internal component implementations." That's modularity as context management — Jackson's exact claim, demonstrated on a storage engine rather than argued.

The constitution / user stories / functional requirements / success criteria / assumptions stack is the concrete artifact behind Naur's theory-building point, which your own note calls the best explanation for why we're moving to spec-driven programming. The durable asset isn't the source text. Certus makes the spec the source of authoritative truth and back-fills drift, so the theory is the thing that persists.

And Spin, Kani, and Creusot as a pipeline is the direct answer to Alenezi's claim that verification has become the rate-limiting activity, and to Gullstrand's finding that human review can't scale because the agent gives no confidence signal. Certus's move is to generate the proof alongside the code from the same spec. The two worked examples are small enough to show: Kani catching a real `base + offset` u32 overflow and proving the fix across all 2³² inputs, and Creusot discharging `clear_all` into 11 subgoals closed automatically by Alt-Ergo and Z3 in under 0.2 seconds with no manual proof steps.

**The tension you should put on a slide rather than manage around.** Your own team wrote it down: "it's sort of self-proving." If the AI writes the spec, the code, and the proof, the verifier certifies agreement, not correctness. That is independently confirmed in your external sources — VERINA's authors note that FVAPPS auto-created formal specifications for 4,715 problems with an LLM and those specs are often easily hackable. And Bursuc's vericoding benchmark found that adding natural-language descriptions doesn't significantly improve performance, which cuts at whether spec quality is even the binding constraint.

Two independent lines, one internal and candid, one external and empirical, landing on the same failure mode. That's a research contribution, not a caveat — and the adversarial-LLM mitigation is the direction it opens.

**The gap.** There's no note connecting Certus to the modularity literature, and that's now load-bearing for the whole Certus half. Your `why-modularity-is-important` note is developing and argues the position, but it links only to Meng-Jackson, He-Miller, and Cervantes-Kazman — nothing to Certus, Prometheus, or the verification cluster. That's the one atomic note the talk needs and doesn't have.

It also happens to sit on the research gap you flagged: no study connecting modularity discipline to long-horizon agent outcomes. Certus is a data point for it. Uncontrolled and n=1, but a data point.

I can draft a triage-style proposal for that note in `inbox/` if you want it — the one-sentence statement stays yours per your own rules. Or the mission file's `Goal` and `Outline` are the more natural next thing now that the scope is settled.

---

## Tamar

okay yes that linkage is missing obviously. Please write the triage style proposal first. I will work on Goal, and then we can attack outline.

---

## Claude

*[Claude checked existing linkage, found Tamar's own Certus reference stranded in the meng-jackson source file, then wrote the triage file and validated every wikilink target.]*

Goes in `inbox/`. Four candidates, all `decision:` lines empty, every wikilink target verified to exist so nothing dangles on promotion.

**Read the top section first.** `/promote` writes a `provenance:` pointer into `raw/claude-exports/`, and that directory is empty — this came from a live conversation, not an export. Save the conversation there before promoting and I'll rewrite the pointers to match. Otherwise the passages in the triage file are the only record, which defeats the point of the provenance discipline.

**One thing worth knowing before you decide.** The linkage isn't entirely missing. You made it yourself, in a `## Tamar's note` inside the meng-jackson source file — the line about Certus going a step further with the synchronization service, with specification being limiting. It's been sitting in a source file that nothing links to. That's the seed of candidate 1, and it's a good argument that the note should be an expansion of `why-modularity-is-important` rather than a new file.

The four: Certus as counterexample to the degradation findings; specification as the durable artifact, via Naur; the self-proving problem; and a merge into the existing modularity note that adds the Certus/Prometheus mechanism it currently lacks.

Candidate 3 is the one I'd think hardest about. It records a tension with your own published blog post — the blog says a generated system with three certificates is more trustworthy than a hand-written system with none, the deck says the chain is sort of self-proving. Both defensible, but the note has to be written one way or the other, so question 3 in the file matters.

Candidate 4 is the one that carries the most weight for the talk, because it supplies the mechanism your existing note argues for without. Certus builds modular so the *agent* can reason; Prometheus refactors into modular so the *verifier* can reason, then restores. Same move, opposite directions, both treating modularity as a precondition for machine reasoning rather than a human-readability concern.

Go write the Goal. When you're back, the outline has a natural shape now — the degradation diagnosis, then the two use cases as the two halves of the lifecycle, then the tensions you're choosing to keep rather than hide.

---

## Tamar

methodology question: I am not clear on where do I write the goal ? and outline? is there a template for this? or what;s the best practice?

---

## Claude

There's no mission template — `templates/` has only note, person, source, and thread. `missions/keynote/index.md` is hand-made, and its headers are the de facto template. So Goal and Outline go straight into that file, under the empty headers already sitting there.

The piece you're missing is the layer between them.

**Threads are where the argument actually gets built.** `templates/thread.md` exists and `missions/keynote/threads/` is empty. A thread has a `question:` field — the thesis in one line — plus `## Where I stand now` (rewritten and dated as your position moves), `## Moves in the argument` (each step linking to the note or source that supports it), and `## Open problems`. That's a keynote section in embryo.

So the intended order is Goal → Threads → Outline. The Outline is the ordering of threads once you can see what each one actually supports; writing it first means committing to a shape before you know which moves have evidence under them. Your `index.md` has a `## Threads` section that's just `- [[ ]]` — it's meant to link out to those files.

`/build-thread` depends on this. It reads `missions/*/threads/<name>.md` and uses the `question:` field to decide what's relevant, so the thread file has to exist before the command can run at all. Its most useful output is §4, tensions — notes that conflict, quoted, deliberately unresolved.

**Practical advice on sequencing.** Don't run `/build-thread` yet. You have four notes, two of them seeds, and the triage from this session isn't promoted. It would come back "accumulating material without shape," which you already know. Promote the triage first, write the notes' one-sentence statements, then run it — at that point it's a real audit rather than a restatement.

For Goal, keep it to a few sentences and make it about the audience's takeaway, not the content list. Something that answers: what should a systems researcher believe after this that they didn't before? That constraint is what makes the outline fall out later instead of becoming a table of contents.

Given the scope you've settled on, the threads I'd expect are roughly: the degradation diagnosis (why AI-assisted development erodes the properties systems need), llm-d as continuous evolution of an existing system, Certus as synthesis of a new one, and the verification/trust problem that cuts across both. Four thread files, each with a one-line `question:`. But those are yours to name — the `question:` line is the same kind of artifact as a note's one-sentence statement, and your own rules put that firmly on your side.

`missions/keynote/assets/` is where slide artifacts and diagrams land when you get there.

---

## Tamar

okay I need step by step instructions. First I want to export this conversation. I believe I have a command for that ? is it "/transcribe"? or something else?

---

## Claude

`/transcript` — it's a skill available here in the chat, not a slash command in your repo. `/transcribe` won't match anything.

Here's the full sequence.

**1. Export the conversation.** Type `/transcript` in this chat. It writes `<slug>-transcript.md` verbatim, alternating `## ` speaker headings, and presents it for download. Fidelity over tidiness — your typos stay in, because they're evidence of how the thinking went.

**2. File it as ground truth.** Save the download to `raw/claude-exports/2026-08-26-keynote-scoping.md`. Name it by date so `/triage-chat` can find it later. `raw/` is append-only — once it's there, never edit it.

**3. Drop the source files in.** The 15 replacements go over `sources/`, the 2 new ones into `sources/_unverified/`. Read the diffs before you commit; delete anything you disagree with.

**4. Fix the triage's provenance pointers.** The triage file I wrote says `source-export: NONE`. Once step 2 is done, change that to the real path and add a `provenance:` line pointing at it. That's a two-line edit you can do by hand — no need to regenerate. Then save the triage into `inbox/`.

**5. Mark your decisions.** Four `decision:` lines in the triage file: `promote`, `drop`, `merge -> <note>`, or `later`. All four must be filled — `/promote` refuses to run on a partial file and tells you which ones are blank.

**6. Run `/promote`** in Claude Code, pointed at the triage file. It creates the notes, wires the backlinks, and leaves a TODO line where your one-sentence statement goes. It will not write those sentences.

**7. Write the one-sentence statements.** Three or four lines of your own words. This is the step that's actually yours.

**8. Then the mission file** — Goal in `missions/keynote/index.md`, thread files in `missions/keynote/threads/`.

**9. `/verify-refs`** to clear the two `_unverified` sources, then `/review`, then commit.

One thing to watch: steps 1–2 have to happen before step 4, or the provenance pointer has nothing to point at. Everything else can slip.

---

## Tamar

/transcript

---

## Claude

*[This transcript.]*

---
