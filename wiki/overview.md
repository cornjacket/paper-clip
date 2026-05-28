---
type: overview
updated: 2026-05-27
---

# PaperClip AI — Overview

> A research wiki on how to use and set up Paperclip — open-source orchestration for teams of AI agents.

The home page of this LLM-maintained research wiki. See [[index]] for the full catalog and
[[paperclip]] for the product entity.

## Current thesis
[[paperclip|Paperclip]] is an open-source control plane that turns a pile of AI agents into a
*company*: you define [[goal-alignment|goals]], hire agents into an [[org-chart-and-agents|org chart]],
and let them work [[tasks-and-tickets|tickets]] driven by [[heartbeats]] — under
[[budget-and-cost-control|budgets]] and [[governance-and-approvals|governance]] you control. Its
distinguishing bet is orchestration, not agent-building: it is [[bring-your-own-agent|runtime-agnostic]]
("if [[openclaw|OpenClaw]] is an employee, Paperclip is the company") and explicitly *not* a chatbot,
agent framework, or workflow builder ([[positioning]]). The whole system is a twelve-part
[[architecture|control plane]]. Setup is self-hosted and fast ([[installation-and-setup]]).

## Open questions
- What does day-to-day operation actually look like beyond the README claims (e.g. the real cost of a "test hire" — the community saw 757K tokens)?
- How mature is the [[plugins|plugin]] system, and what's in *awesome-paperclip*?
- What's the status of the planned **Memory / Knowledge** work ([[roadmap]])?
- How do the deployment/bind modes ([[identity-and-access]]) behave in practice for a solo vs team setup?

## Next steps
- Capture screenshots of the dashboard/UI into `raw/screenshots/` so pages can reference them.
- Ingest the official docs (paperclip.ing/docs) and DEVELOPING.md for setup depth.
