---
type: source
title: "Trust-Calibrated Code Review: A Participatory Design Study of Review Workflows for LLM-Generated Multi-File Changes"
citekey: gullstrand-2026-trust-calibrated-code-review
authors: [Lo Gullstrand Heander, Agnia Sergeyuk, Ilya Zakharov, Emma Söderberg, Nikita Mukhortov]
year: 2026
kind: paper
container: arXiv
publisher:
doi: https://doi.org/10.48550/arXiv.2606.01969
url: https://arxiv.org/abs/2606.01969
lang:
origin:      external
project:
clearance:   public

verified: true
holdings: [link]
file:

people: []
tags: [human-ai-collaboration, genai-failure]
missions: [keynote]

status: unread
added: 2026-08-11
---

## Why it matters to me

## Notes

Claude: is the sharpest reframing I found for review workflows. Prior work positions diff comprehension and cognitive load as the primary review obstacles; this study argues that when the author is an LLM agent, comprehension is a downstream effect rather than the root cause. Reviewers cannot allocate attention proportionate to segment-level risk because the agent gives no signal about its own confidence or reasoning, so they read every line — the rational response to an author that presents heterogeneous-quality output with homogeneous confidence.

TE: They propose trust calibration — allocating review effort by segment-level risk when the author cannot be interrogated — as the organizing problem.

## Quotes
<!-- Always blockquoted, always with a locator. -->
