---
type: concept
name: Plugins
tags: [plugins, extensibility]
---

Paperclip has an instance-wide plugin system so you can extend it without forking.

## Details
Out-of-process workers, capability-gated host services, job scheduling, tool exposure, and UI contributions. Plugins can add knowledge bases, custom tracing, queues, and more. For driving Paperclip from *outside* tools, the sibling surface is the first-party MCP server ([[mcp-integration]]).

## Ecosystem
The pinned **Plugin System** discussion is community-seeded ([[paperclip-github-discussions]]); find more at *awesome-paperclip* ([[community-and-ecosystem]]). Plugin ideas include a RAG-powered Company Knowledge Base and typed-graph memory providers — see [[roadmap]] (Memory / Knowledge).

Parent: [[architecture]] · Source: [[paperclip-readme]], [[paperclip-github-discussions]]
