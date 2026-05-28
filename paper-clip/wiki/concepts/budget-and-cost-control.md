---
type: concept
name: Budget & Cost Control
tags: [budget, cost, tokens, governance]
---

Paperclip tracks tokens and cost by company, agent, project, [[goal-alignment|goal]], issue, provider, and model, and enforces scoped budgets so agents stop when they hit a limit.

## Mechanics
Scoped **budget policies** carry warning thresholds and **hard stops**. Overspend pauses agents and cancels queued work automatically. Budget checks run on every [[heartbeats|heartbeat]], and checkout + budget enforcement are atomic ([[tasks-and-tickets]]) — no runaway spend.

## Why it matters
Runaway loops can burn hundreds of dollars before you notice; the community reports test hires consuming 757K tokens and asks for token-reducing defaults ([[paperclip-github-discussions]]). Budgets are enforced under [[governance-and-approvals]]. For the operator playbook on *reducing* spend, see [[cost-optimization]].

## ⚠️ Known gap: budgets don't fire under subscription billing
The README presents budget hard-stops as the safety net, but in practice they only work when cost is actually computed. When an agent bills against a Claude **subscription** (Max plan, via the "claw local" adapter passthrough) instead of the Anthropic **API**, Paperclip reports cost as **$0** — so a $5 budget never triggers and queued work is never cancelled. Since most users run on subscription, the headline "no runaway spend" guarantee is weaker than the README implies. Workaround (query the embedded Postgres and backfill inferred cost) is in [[cost-optimization]] and [[token-usage-in-paperclip]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[paperclip-github-discussions]], [[token-usage-in-paperclip]]
