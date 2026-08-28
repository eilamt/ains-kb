---
type: source
title: "Towards AI-Native Software Engineering (SE 3.0): A Vision and a Challenge Roadmap"
citekey: hassan-2025-ai-native-se-30
authors: [Ahmed E. Hassan, Gustavo A. Oliva, Dayi Lin, Boyuan Chen, Zhen Ming (Jack) Jiang]
year: 2025
kind: article
container: ACM Transactions on Software Engineering and Methodology (TOSEM)
publisher: ACM
doi: https://doi.org/10.1145/3807901
url: https://dl.acm.org/doi/10.1145/3807901
lang:
origin:      external
project:
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [sdlc]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

Claude: is the dominant framing and the one ICSE reviewers will know. Towards AI-Native Software Engineering (SE 3.0) is now in TOSEM: it posits an intent-centric, conversation-oriented paradigm in which AI moves from task-driven copilot to intelligent collaborator reasoning about SE principles and intents. The follow-on, Agentic Software Engineering: Foundational Pillars and a Research Roadmap, introduces a concrete architecture: the Agent Command Environment (ACE) as a command center where humans orchestrate and mentor agent teams, handling Merge-Readiness Packs and Consultation Request Packs; and the Agent Execution Environment (AEE) where agents work and invoke human expertise when facing ambiguity or trade-offs, with agent-initiated human callbacks and handovers. The organizing duality is "SE for Humans" versus "SE for Agents." There was an ICSE 2026 technical briefing (Apr 15) synthesizing the AIDev characterization, the 567 Claude Code PR study, and the Structured Agentic Software Engineering (SASE) framework, with a vocabulary of agent command environment and agent execution environment for designing trustworthy human-agent workflows.

Comment: terminology collision: "AI-Native SE" is Hassan's label for SE 3.0. differentiate position AINS against it explicitly.

TE: SELF DRIVING CAR ANALOGY IS HERE: https://arxiv.org/pdf/2509.06216

## Quotes
<!-- Always blockquoted, always with a locator. -->

> The core purpose of the SE field has always been to ensure solutions are trustworthy and delivered economically, and much of the SE field exists because we cannot assume that every team is composed of "super developers." The industry has long acknowledged the phenomenon of the "10x developers," a small fraction of developers whose impact far exceeds the median [30]. A significant portion of SE, from structured processes like Agile to sophisticated tools like IDEs, is designed to give non-super developers the scaffolding and opportunity to perform at a 10x level. Agentic SE radically reshapes this landscape, moving the conversation beyond 10x to the realm of 100x and even 1,000x productivity while also redefining the characteristics of such top-tier developers, away from raw coding prowess and toward effective collaboration with fleets of agents (aka AI Teammates).

(p. ?)

> As the industry forges ahead, a Cambrian explosion of ad-hoc practitioner techniques is emerging. However, these grassroots innovations highlight a vacuum of robust, validated approaches. Current methods, relying heavily on informal, conversational prompting, are inadequate for developing trustworthy large-scale, long-lived software. This informality fails to establish robust processes for reproducibility, auditable artifacts for trust, or a durable mechanism for human-agent collaboration. It keeps the paradigm locked in the realm of 1-to-1 "agentic coding," rather than unlocking the potential of N-to-N "agentic software engineering" where teams of humans and agents collaborate at scale. Early attempts to impose order, like the Plan-Do-Assess-Review (PDAR) loop, are a crucial shift but do not constitute a complete engineering methodology. This new reality demands more than incremental adjustments; it compels us to fundamentally reconsider the pillars upon which the SE field is built: the Actors, the Processes they follow, the Tools they use, and the Artifacts they shape.

(p. ?)

> The bitter lesson is the observation in artificial intelligence that, in the long run, general approaches that scale with available computational power tend to outperform ones based on domain-specific understanding because they are better at taking advantage of the falling cost of computation over time. The principle was proposed and named in a 2019 essay by Richard Sutton[1] and is now widely accepted….. the tension: However, the lesson's power is most potent where data is abundant like at lower levels of abstraction or for common problems like building a web application. Its application becomes far more complex for novel tasks or in niche domains where training data is scarce. For these settings, relying solely on large-scale data is inefficient; a human is still needed to provide the overarching structure and connect the dots.

(p. ?)

> A foundational premise of this paper is the distinction between agentic coding and agentic software engineering. Agentic coding, which characterizes the current state of most available tools, focuses primarily on the 1-to-1 interaction between a developer and an AI assistant to accelerate implementation tasks. Agentic coding is fundamentally an augmentation of a solo activity, aimed at boosting individual productivity. Software Engineering (SE), by contrast, has always been a team sport. SE involves not only producing code but also managing complexity, coordinating across diverse roles, reconciling competing stakeholder needs, and ensuring the long-term sustainability of shared artifacts. These inherently collective challenges demand the acceleration of structured collaboration, not just individual acceleration. Structured Agentic Software Engineering (SASE) is explicitly designed for this broader scope. It provides the artifacts, processes, and workbenches necessary to support N-to-N collaboration, where many humans and many agents interact as a coordinated team.

(p. ?)
