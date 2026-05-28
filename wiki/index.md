---
type: index
updated: 2026-05-28
---

# Index

Content catalog for the PaperClip AI research wiki. Every page is listed by category with a
one-line summary, and updated on every ingest. See [[overview]] for the big picture.

## Overview
- [[overview]] — top-level summary and evolving thesis.
- [[wiki-hot-cache]] — single-page synthesis of the whole wiki; load this first.
- `how-paperclip-works.canvas` — visual board: operating model, org chart, heartbeat run lifecycle, cross-cutting systems.

## Sources
- [[paperclip-readme]] — clipped GitHub README: product overview + quickstart.
- [[paperclip-github-discussions]] — clipped Discussions index: community + ecosystem signal.
- [[token-usage-in-paperclip]] — YouTube transcript: cost levers, the $0-subscription bug, real per-agent costs.
- [[top-level-summary]] — secondary explainer: orchestration-runtime framing, vs agent libraries; its MCP/traction claims were verified against the repo.

## Entities
- [[paperclip]] — the product: open-source orchestration for teams of AI agents (central hub).
- [[openclaw]] — the archetypal agent "employee" Paperclip orchestrates.

## Concepts

### Architecture & execution
- [[architecture]] — the twelve-system control plane (hub).
- [[heartbeats]] — the execution engine: agents wake, check work, act.
- [[tasks-and-tickets]] — ticket-based work with goal ancestry and atomic checkout.
- [[workspaces-and-runtime]] — project + isolated execution workspaces, dev servers.
- [[routines-and-schedules]] — recurring work via cron/webhook/API triggers.

### Organization & governance
- [[org-chart-and-agents]] — roles, titles, reporting lines, budgets, adapters.
- [[goal-alignment]] — every task traces back to the company mission.
- [[governance-and-approvals]] — approvals, policies, rollback, audit.
- [[quality-assurance-loops]] — reviewer hierarchies that fight compounding error in long agent chains.
- [[identity-and-access]] — auth, deployment modes, users, agent keys.
- [[multi-company-isolation]] — many companies per deployment, fully isolated.

### Cost, data & extensibility
- [[budget-and-cost-control]] — token/cost tracking and scoped budget enforcement.
- [[cost-optimization]] — operator playbook: the five cost levers + the $0-subscription bug & workaround.
- [[secrets-and-storage]] — secrets, encrypted + object storage, attachments.
- [[activity-and-events]] — durable audit log of actions and events.
- [[company-portability]] — export/import whole organizations.
- [[plugins]] — out-of-process extension system.
- [[skills]] — runtime skill injection.

### Agents, setup & positioning
- [[bring-your-own-agent]] — adapters: any agent, any provider.
- [[installation-and-setup]] — quickstart, requirements, deployment modes, telemetry.
- [[setup-sop]] — step-by-step runbook to stand up a cost-safe deployment end to end.
- [[positioning]] — what Paperclip is and is not; vs alternatives.
- [[roadmap]] — shipped vs planned capabilities.
- [[community-and-ecosystem]] — channels, maintainers, notable community builds.
