---
type: concept
name: Bring Your Own Agent (Adapters)
tags: [adapters, agents, byo, integrations]
---

"If it can receive a heartbeat, it's hired." Paperclip is runtime-agnostic: any agent, any provider, one [[org-chart-and-agents|org chart]].

## Supported runtimes
[[openclaw|OpenClaw]], Claude Code, Codex, Cursor, Bash, and HTTP/webhook bots — plus external adapter plugins. Agents bring their own prompts, models, and runtimes ([[positioning]]).

## Ecosystem
Community adapters and providers include OpenCode + LiteLLM, DeepSeek, Gemma, a multi-account Codex router, and OpenClaw-likes such as "PicoClaw" ([[paperclip-github-discussions]]).

## Connections
Adapters are invoked during [[heartbeats]]; sandbox/cloud agents (Cursor/e2b) are on the [[roadmap]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[paperclip-github-discussions]]
