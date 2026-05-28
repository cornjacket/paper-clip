---
type: entity
name: Paperclip
category: product
tags: [paperclip, orchestration, agents]
---

Paperclip is an open-source app for managing teams of AI agents at work — "if [[openclaw|OpenClaw]] is an *employee*, Paperclip is the *company*." Built by Paperclip Labs, Inc. (MIT licensed).

## What it is
A Node.js server with a React UI that orchestrates a team of AI agents to run a business. You bring your own agents, assign goals, and track work and costs from one dashboard. It looks like a task manager; under the hood it models org charts, budgets, governance, [[goal-alignment|goal alignment]], and agent coordination.

## The model
1. **Define the goal** — e.g. "Build the #1 AI note-taking app to $1M MRR." See [[goal-alignment]].
2. **Hire the team** — CEO, CTO, engineers, designers, marketers; any bot, any provider. See [[org-chart-and-agents]] and [[bring-your-own-agent]].
3. **Approve and run** — review strategy, set budgets, monitor from the dashboard. See [[governance-and-approvals]] and [[budget-and-cost-control]].

## How it works
Agents wake on [[heartbeats]], check [[tasks-and-tickets|tickets]], and act. The full control plane is described in [[architecture]]. Set it up via [[installation-and-setup]].

## See also
- What it is *not*: [[positioning]]
- Ecosystem: [[community-and-ecosystem]], [[plugins]], [[roadmap]]
- Sources: [[paperclip-readme]], [[paperclip-github-discussions]]
