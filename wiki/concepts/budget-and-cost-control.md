---
type: concept
name: Budget & Cost Control
tags: [budget, cost, tokens, governance]
---

Paperclip tracks tokens and cost by company, agent, project, [[goal-alignment|goal]], issue, provider, and model, and enforces scoped budgets so agents stop when they hit a limit.

## Mechanics
Scoped **budget policies** carry warning thresholds and **hard stops**. Overspend pauses agents and cancels queued work automatically. Budget checks run on every [[heartbeats|heartbeat]], and checkout + budget enforcement are atomic ([[tasks-and-tickets]]) — no runaway spend.

## Why it matters
Runaway loops can burn hundreds of dollars before you notice; the community reports test hires consuming 757K tokens and asks for token-reducing defaults ([[paperclip-github-discussions]]). Budgets are enforced under [[governance-and-approvals]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[paperclip-github-discussions]]
