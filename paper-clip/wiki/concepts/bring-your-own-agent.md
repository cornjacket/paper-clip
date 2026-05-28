---
type: concept
name: Bring Your Own Agent (Adapters)
tags: [adapters, agents, byo, integrations]
---

"If it can receive a heartbeat, it's hired." Paperclip is runtime-agnostic: any agent, any provider, one [[org-chart-and-agents|org chart]].

## Supported runtimes
[[openclaw|OpenClaw]], Claude Code, Codex (OpenAI), OpenCode, Cursor, Bash, and HTTP/webhook bots — plus any model via **OpenRouter** and external adapter plugins. Agents bring their own prompts, models, and runtimes ([[positioning]]).

## Two layers: orchestration vs action
Paperclip is the **infrastructure / middleware layer**, not the LLM logic itself ([[top-level-summary]]):
- **Orchestration layer (Paperclip):** routes tasks, tracks token budgets, holds state.
- **Action layer (the connected agent, e.g. Claude Code):** runs terminal commands, edits files, executes scripts.

## Ecosystem
Community adapters and providers include OpenCode + LiteLLM, DeepSeek, Gemma, a multi-account Codex router, and OpenClaw-likes such as "PicoClaw" ([[paperclip-github-discussions]]).

## Adapter, model & billing
An agent's **adapter selects which model it runs** ([[token-usage-in-paperclip]]). The **"claw local" adapter** passes through your authenticated Claude CLI session, so runs bill against your **subscription** (Max plan) rather than the Anthropic **API** — a primary draw of Paperclip ("not so with OpenClaw"), but the source of the [[budget-and-cost-control|$0-cost bug]]. You can also point adapters at small **local models** (e.g. an 8B Ollama model like Qwen) for cheap, frequent work — see the cheap-scan pattern in [[cost-optimization]]. Model and cadence are the top cost levers.

## Connections
Adapters are invoked during [[heartbeats]]; sandbox/cloud agents (Cursor/e2b) are on the [[roadmap]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[paperclip-github-discussions]], [[token-usage-in-paperclip]]
