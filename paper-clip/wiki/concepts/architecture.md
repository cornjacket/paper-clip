---
type: concept
name: Architecture (Control Plane)
tags: [architecture, systems, control-plane]
---

Paperclip is a full control plane, not a wrapper — twelve server-side systems coordinate agents end to end. This page maps them; each links to its own page.

## The twelve systems
- [[identity-and-access]] — deployment modes, users, agent keys, run JWTs, memberships.
- [[org-chart-and-agents]] — roles, titles, reporting lines, permissions, budgets, adapters.
- [[tasks-and-tickets]] — issues with goal ancestry, atomic checkout, blockers, work products.
- [[heartbeats]] — DB-backed wakeup queue that runs agents.
- [[workspaces-and-runtime]] — project + isolated execution workspaces, dev servers, preview URLs.
- [[governance-and-approvals]] — approval workflows, policies, hard-stops, audit.
- [[budget-and-cost-control]] — token/cost tracking and scoped budget enforcement.
- [[routines-and-schedules]] — recurring work via cron/webhook/API triggers.
- [[plugins]] — out-of-process extension system.
- [[secrets-and-storage]] — secrets, encrypted + object storage, attachments.
- [[activity-and-events]] — durable audit log of actions and events.
- [[company-portability]] — export/import whole organizations.

## Clients / adapters
Agents connect as adapters — Claude Code, Codex, CLI agents (Cursor/Gemini/bash), and HTTP/webhook bots like [[openclaw|OpenClaw]]. See [[bring-your-own-agent]].

## Cross-cutting themes
[[goal-alignment]], [[multi-company-isolation]], and [[skills]] run across many of these systems.

Parent: [[paperclip]] · Source: [[paperclip-readme]]
