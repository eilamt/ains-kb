---
type: note
title: specification as the durable artifact
tags: [sdd, mdd, sdlc]
people: []
missions: [keynote]
status: seed
created: 2026-08-26
updated: 2026-08-26
---
Specification needs to be the authoritative artifact.  
specification and code need to always co-evolve and kept in sync. 
## Elaboration

The key issue is that spec and code need to be kept in sync. This is hard specifically in brown field where spec needs to be created based on existing code. 
## Tensions
objections will say that the code is the only thing that matters for AI, but the specification is needed for multiple reasons: 1. AI buffer size issue 2. limit scope of change and allow parallelism 3. cognition gap  etc. 
Also, this does not mean we are going BACK to waterfall. We are keeping it agile by continuous synchronization of spec and code - what was manually taxing before, now with AI is actually possible. 

## Connects to
- [[what-we-need-ai-to-do-for-sw-engineering]]
- [[sources/alenezi-2026-human-ai-collaboration-se]]
- [[sources/waddington-2026-certus-storage]]
- [[sources/cito-bork-2025-lost-in-code-generation]]
- [[sources/farrag-2026-productivity-reliability-paradox]]
- [[mind-theory-of-computation]]

## Provenance

provenance: raw/claude-exports/2026-08-26-keynote-scoping.md

> This is the best explanation of why we are moving to spec-driven or
> intent-driven programming.

— your reaction in `sources/alenezi-2026-human-ai-collaboration-se`

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

> Indeed the difference is GREEN vs. BROWN. This tension goes away if you
> consider that code and spec co-evolve, and always need to be kept in sync.
> The question is an epistemological one - what came first. In brown field it
> is the code, and the spec is created based on it by reverse engineering, it
> is just a bootstraping mechanism. Once a spec is created, keeping them in
> sync at all times is how the process works (of course generating spec from
> code is a non-trivial unsolved problem).

— Tamar, on review of triage `triage-2026-08-26-certus-modularity-sdlc-2.md`
