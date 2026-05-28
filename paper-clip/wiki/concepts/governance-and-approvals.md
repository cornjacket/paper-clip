---
type: concept
name: Governance & Approvals
tags: [governance, approvals, audit, policy]
---

Nothing ships without sign-off: Paperclip provides board approval workflows, execution policies with review/approval stages, and the ability to pause, resume, or terminate any agent at any time.

## Mechanics
- Approval gates are enforced; config changes are revisioned and **bad changes can be rolled back** ("governance with rollback").
- Decision tracking and **budget hard-stops** ([[budget-and-cost-control]]).
- Full audit logging via [[activity-and-events]].

## Connections
Governs [[org-chart-and-agents|agents]] and their [[tasks-and-tickets|work]], scoped by [[identity-and-access]]. Approvals also gate hires and supervise [[routines-and-schedules]]. The same review/approval stages power reviewer hierarchies that fight compounding error — see [[quality-assurance-loops]].

Parent: [[architecture]] · Source: [[paperclip-readme]]
