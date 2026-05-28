---
type: concept
name: Goal Alignment
tags: [goals, alignment, mission]
---

Every task traces back to the company mission, so agents know *what* to do and *why* — "manage business goals, not pull requests."

## Details
Tasks carry full **goal ancestry** (company → project → goal → parent), giving "goal-aware execution." Context flows from the task up through project and company goals, so an agent always has the why.

## Goal-driven decomposition (vs step-by-step scripting)
Rather than hardcoding a workflow, you hand Paperclip a high-level goal (e.g. *"Build an IoT data-ingestion service with a time-series database"*) and the lead/"CEO" agent decomposes it into discrete tasks and sub-tasks ([[top-level-summary]]). This top-down breakdown is the counterpart to the bottom-up goal ancestry above.

## Connections
Realized in [[tasks-and-tickets]], assigned through the [[org-chart-and-agents|org chart]], and is the first step of the [[paperclip|Paperclip]] model (define the goal).

Parent: [[architecture]] · Source: [[paperclip-readme]]
