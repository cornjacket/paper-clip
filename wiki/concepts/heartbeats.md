---
type: concept
name: Heartbeats (Heartbeat Execution)
tags: [heartbeats, execution, scheduling]
---

Heartbeats are Paperclip's execution engine: agents wake on a schedule (or trigger), check their work, and act. Delegation flows up and down the [[org-chart-and-agents|org chart]].

## How it works
A DB-backed wakeup queue with coalescing drives each run. On wake, a run performs budget checks ([[budget-and-cost-control]]), workspace resolution ([[workspaces-and-runtime]]), secret injection ([[secrets-and-storage]]), [[skills|skill loading]], and adapter invocation ([[bring-your-own-agent]]). Runs produce structured logs, cost events, session state, and audit trails ([[activity-and-events]]). Orphaned runs are recovered automatically.

## Persistent state
Agents resume the same [[tasks-and-tickets|task]] context across heartbeats instead of restarting from scratch.

## Triggers
By default agents run on scheduled heartbeats and event-based triggers (task assignment, @-mentions); continuous agents like [[openclaw|OpenClaw]] can also be hooked in. Recurring work is scheduled via [[routines-and-schedules]].

Parent: [[architecture]] · Source: [[paperclip-readme]]
