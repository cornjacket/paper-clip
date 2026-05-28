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
[[architecture|control plane]]. Setup is self-hosted and fast ([[installation-and-setup]]). The
recurring real-world friction is **cost**: tokens add up fast, and the main levers are model choice,
[[heartbeats|heartbeat cadence]], lean instructions/[[skills]], and budgets ([[cost-optimization]]).

## Open questions
- How mature is the [[plugins|plugin]] system, and what's in *awesome-paperclip*?
- What's the status of the planned **Memory / Knowledge** work ([[roadmap]])?
- How do the deployment/bind modes ([[identity-and-access]]) behave in practice for a solo vs team setup?
- Will Paperclip fix the [[cost-optimization|$0-cost bug]] so [[budget-and-cost-control|budget hard-stops]] work under subscription billing? Until then the Postgres-backfill workaround is the only way to see real spend.

## Next steps
- Capture screenshots of the dashboard/UI into `raw/screenshots/` so pages can reference them.
- Ingest the official docs (paperclip.ing/docs) and DEVELOPING.md for setup depth.
