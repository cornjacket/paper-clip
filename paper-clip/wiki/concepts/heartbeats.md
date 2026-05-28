---
type: concept
name: Heartbeats (Heartbeat Execution)
tags: [heartbeats, execution, scheduling]
---

Heartbeats are Paperclip's execution engine: agents wake on a schedule (or trigger), check their work, and act. Delegation flows up and down the [[org-chart-and-agents|org chart]].

## Why heartbeats exist (statelessness)
Left alone, an AI agent wakes with technical capability but **zero context** about its long-term goals, prior actions, or company identity — the "amnesia" problem ([[top-level-summary]]). The heartbeat loop re-establishes that context on every wake, which is what turns stateless agents into persistent "employees."

## How it works
A DB-backed wakeup queue with coalescing drives each run. On wake, a run performs budget checks ([[budget-and-cost-control]]), workspace resolution ([[workspaces-and-runtime]]), secret injection ([[secrets-and-storage]]), [[skills|skill loading]], and adapter invocation ([[bring-your-own-agent]]). Runs produce structured logs, cost events, session state, and audit trails ([[activity-and-events]]). Orphaned runs are recovered automatically.

**Agent's-eye checklist** (the run from the agent's perspective, per [[top-level-summary]]) — complements the system steps above:
1. **Identity fetch** — confirm role, persona, system boundaries.
2. **Context retrieval** — check the current project queue and dependencies ([[tasks-and-tickets]]).
3. **Action & execution** — run tools, write files, or delegate a sub-task.
4. **Memory extraction** — log progress, errors, and state changes back to the system.

## Persistent state
Agents resume the same [[tasks-and-tickets|task]] context across heartbeats instead of restarting from scratch.

## Triggers
By default agents run on scheduled heartbeats and event-based triggers (task assignment, @-mentions); continuous agents like [[openclaw|OpenClaw]] can also be hooked in. Recurring work is scheduled via [[routines-and-schedules]].

## Cadence (configuration & cost)
Each agent's heartbeat interval is configured in **seconds**: `5` = every 5 seconds, `60` = every minute, `360` = every hour ([[token-usage-in-paperclip]]). Agents can also be set to run only on **manual/trigger**, never on a timer. Cadence is the **single biggest cost lever** — 15 agents waking every 5 minutes on a frontier model burns budgets fast. Match cadence to the job. See [[cost-optimization]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[token-usage-in-paperclip]]
