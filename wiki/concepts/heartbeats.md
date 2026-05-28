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

## Cadence (configuration & cost)
Each agent's heartbeat interval is configured in **seconds**: `5` = every 5 seconds, `60` = every minute, `360` = every hour ([[token-usage-in-paperclip]]). Agents can also be set to run only on **manual/trigger**, never on a timer. Cadence is the **single biggest cost lever** — 15 agents waking every 5 minutes on a frontier model burns budgets fast. Match cadence to the job. See [[cost-optimization]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[token-usage-in-paperclip]]
