---
type: concept
name: Org Chart & Agents
tags: [org-chart, agents, roles, hierarchy]
---

Agents in Paperclip have a boss, a title, and a job description: roles, reporting lines, permissions, and budgets arranged in a hierarchy.

## Details
Adapter types match the [[architecture]] diagram: Claude Code, Codex, CLI agents (Cursor/Gemini/bash), HTTP/webhook bots like [[openclaw|OpenClaw]], and external adapter plugins — "if it can receive a heartbeat, it's hired" ([[bring-your-own-agent]]). Delegation flows up and down the chart via [[heartbeats]].

## Per-agent tuning
Each agent is configured individually — its adapter/model, [[heartbeats|heartbeat cadence]], assigned [[skills]], and budget. Tuning these per agent (frontier model + daily cadence for a chief of staff; cheap/local model + manual run for a rarely-needed one) is the main cost-control practice — see [[cost-optimization]].

## Connections
Each agent has a scoped budget ([[budget-and-cost-control]]) and permissions governed by [[identity-and-access]] and [[governance-and-approvals]]. Work is assigned as [[tasks-and-tickets|tickets]] tied to [[goal-alignment|goals]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[token-usage-in-paperclip]]
