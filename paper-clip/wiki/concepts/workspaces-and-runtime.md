---
type: concept
name: Workspaces & Runtime
tags: [workspaces, runtime, git-worktrees]
---

Workspaces ensure agents work in the right directory with the right context every time.

## Details
- **Project workspaces** plus **isolated execution workspaces** (git worktrees, operator branches).
- Runtime services: dev servers and preview URLs.

## Connections
Resolved per run during [[heartbeats|heartbeat execution]], with [[secrets-and-storage|secrets]] injected as needed. Supports the coding workflows of [[bring-your-own-agent|adapter agents]].

Parent: [[architecture]] · Source: [[paperclip-readme]]
