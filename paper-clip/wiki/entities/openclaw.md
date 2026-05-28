---
type: entity
name: OpenClaw
category: tool
tags: [agent, adapter, openclaw]
---

OpenClaw is the archetypal autonomous agent that [[paperclip|Paperclip]] orchestrates — the "employee" to Paperclip's "company." It connects as an HTTP/webhook bot and can run continuously.

## Relationship to Paperclip
Paperclip *uses* agents like OpenClaw rather than replacing them: it gives them an [[org-chart-and-agents|org chart]], budgets, [[goal-alignment|goals]], [[governance-and-approvals|governance]], and accountability. OpenClaw is one of several supported runtimes — see [[bring-your-own-agent]]. Because Paperclip triggers work via [[heartbeats]] and event-based triggers, continuous agents like OpenClaw can also be hooked in. OpenClaw onboarding is handled by [[identity-and-access]].

## Ecosystem notes
The community discusses OpenClaw-like adapters such as "PicoClaw," plus recurring OpenClaw integration issues. See [[paperclip-github-discussions]] and [[community-and-ecosystem]].
