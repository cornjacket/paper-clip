---
type: concept
name: Work & Task System (Tickets)
tags: [tasks, tickets, issues, work]
---

Paperclip is ticket-based: every unit of work is an issue carrying company/project/[[goal-alignment|goal]]/parent links, so agents always see the "why," not just a title.

## Mechanics
- **Atomic checkout** with execution locks — no double-work, no lost context.
- First-class **blocker dependencies**, comments, documents, attachments, work products, labels, and inbox state.
- Conversations are threaded and sessions persist across reboots (via [[heartbeats|persistent state]]).

## Connections
Tasks are executed by [[heartbeats]], reviewed under [[governance-and-approvals]], metered by [[budget-and-cost-control]], and generated automatically by [[routines-and-schedules]]. Atomic checkout + budget enforcement together are what the README calls "atomic execution."

Parent: [[architecture]] · Source: [[paperclip-readme]]
