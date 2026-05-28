---
type: concept
name: Positioning (What Paperclip Is & Isn't)
tags: [positioning, comparison, scope]
---

Paperclip models a *company* of agents, not the agents themselves. It "manages business goals, not pull requests."

## What it is not
- **Not a chatbot** — agents have jobs, not chat windows.
- **Not an agent framework** — it runs companies of agents; it doesn't tell you how to build them.
- **Not a workflow builder** — no drag-and-drop pipelines; it models org charts, [[goal-alignment|goals]], budgets, governance.
- **Not a prompt manager** — agents bring their own prompts/models/runtimes ([[bring-your-own-agent]]).
- **Not a single-agent tool** — for teams; one agent probably doesn't need it, twenty do.
- **Not a code review tool** — it orchestrates work, not pull requests.

## Versus alternatives
- vs agents like [[openclaw|OpenClaw]] / Claude Code: Paperclip *uses* them, adding org charts, budgets, goals, governance, accountability.
- vs pointing an agent at Asana/Trello: Paperclip handles work checkout, sessions, [[budget-and-cost-control|cost monitoring]], and [[governance-and-approvals|governance]] that generic trackers don't.
- vs **agent libraries** (LangChain / AutoGen / CrewAI): those are code-driven — you wire agents together in Python with state machines/graphs. Paperclip is a **UI-driven runtime**: autonomous CEO/lead delegation instead of coded orchestration, and built-in persistent state instead of custom DB setups ([[top-level-summary]]).

| | Single assistant (ChatGPT/Claude) | Agent libraries (CrewAI/AutoGen/LangChain) | **Paperclip** |
|---|---|---|---|
| Operation model | Task-by-task chat | Code-driven Python scripts | **UI-driven runtime** |
| Coordination | Human coordinates | Coded state machines/graphs | **Autonomous CEO/lead delegation** |
| User persona | End-user | Developer (writes Python) | **System architect / "the Board" (review & direct)** |
| State | Lost at session end | Custom DB required | **Built-in dashboard, [[heartbeats]], logs** |

## See also
- Reliability at scale via reviewer hierarchies: [[quality-assurance-loops]].
- Programmatic access via the first-party MCP server → [[mcp-integration]].

Parent: [[paperclip]] · Source: [[paperclip-readme]], [[top-level-summary]]
