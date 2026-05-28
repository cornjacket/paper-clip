---
type: concept
name: MCP Integration (paperclip-mcp)
tags: [mcp, integration, api, tools]
---

Paperclip ships a first-party **Model Context Protocol (MCP) server** so any MCP-compatible client can drive a Paperclip workspace as a set of standard tools.

> **Verified 2026-05-28** against the [paperclipai/paperclip](https://github.com/paperclipai/paperclip) repo. Originally surfaced (with some embellishment) by the secondary [[top-level-summary]]; now confirmed first-party.

## What it is
- Package **`@paperclipai/mcp-server`**, living in-repo at `packages/mcp-server`.
- The README calls it "a **thin MCP wrapper over the existing Paperclip REST API** — it does not talk to the database directly and it does not reimplement business logic." The REST API stays the single source of truth.
- Exposes **~40+ tools** over core entities — Issues, Comments, Documents, Projects, Approvals, Goals, Agents — split into read tools (~23) and write tools (~15), plus a `paperclipApiRequest` escape hatch for anything not wrapped.

## What this enables
Any MCP client/IDE can query, trigger, or monitor the multi-agent workspace through tool calls — e.g. create [[tasks-and-tickets|issues]], file [[governance-and-approvals|approvals]], read [[goal-alignment|goals]], or inspect [[budget-and-cost-control|costs]] in natural language. (The package README itself doesn't name specific clients; [[top-level-summary]]'s claim of Cursor/Windsurf/Claude Desktop is the standard MCP-client set, not an official list.)

## Not to be confused with
A **separate namesake** project, `matsjfunke/paperclip`, is an MCP server for retrieving research papers from **arXiv / OSF / OpenAlex** — unrelated to the agent-orchestration Paperclip ([[paperclip]]). [[top-level-summary]]'s "academic variant" is this different project; the conflation is confirmed. Community MCP servers also exist (e.g. `Wizarck/paperclip-mcp`) distinct from the first-party `@paperclipai/mcp-server`.

## Connections
A programmatic front door alongside the [[plugins|plugin]] system; both extend how outside tools reach the [[architecture|control plane]].

Parent: [[architecture]] · Source: [[top-level-summary]] (claim), paperclipai/paperclip repo (verification)
