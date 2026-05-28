---
type: hot-cache
title: Wiki Hot Cache
updated: 2026-05-27
sources: [paperclip-readme, paperclip-github-discussions, token-usage-in-paperclip]
---

# Wiki Hot Cache — PaperClip AI

A single-page synthesis of the entire wiki — load this first, then drill into linked pages for detail. Everything here traces to [[paperclip-readme]], [[paperclip-github-discussions]], and [[token-usage-in-paperclip]]; see [[index]] for the full catalog and [[overview]] for the evolving thesis.

> **One-liner:** [[paperclip|Paperclip]] is an open-source control plane that turns a pile of AI agents into a *company* — "if [[openclaw|OpenClaw]] is an *employee*, Paperclip is the *company*." Node.js server + React UI, MIT licensed by Paperclip Labs, Inc.

## Mental model

Paperclip orchestrates agents; it does not build them. You bring your own agents and Paperclip gives them an org chart, goals, budgets, governance, and accountability. It looks like a task manager but underneath models a company.

**The three-step model:**
1. **Define the goal** — e.g. "Build the #1 AI note-taking app to $1M MRR." → [[goal-alignment]]
2. **Hire the team** — CEO, CTO, engineers, designers, marketers; any bot, any provider. → [[org-chart-and-agents]], [[bring-your-own-agent]]
3. **Approve and run** — review strategy, set budgets, monitor from the dashboard. → [[governance-and-approvals]], [[budget-and-cost-control]]

**What it is *not*** ([[positioning]]): not a chatbot, not an agent framework, not a workflow builder, not a prompt manager, not a single-agent tool, not a code-review tool. Tagline: "manage business goals, not pull requests." For teams (one agent doesn't need it, twenty do).

## Org chart & agents

Every agent has a **boss, a title, a job description, a scoped budget, and permissions**, arranged in a hierarchy. Delegation flows up and down the chart via [[heartbeats]]. Work arrives as [[tasks-and-tickets|tickets]] tied to [[goal-alignment|goals]]. See [[org-chart-and-agents]].

```
              Company goal ($1M MRR)
                       │
                      CEO
                ┌──────┴───────┐
               CTO         Marketing/Design...
          ┌─────┴─────┐
      Engineer     Engineer        ← each = an adapter-backed agent
      (budget,     (budget,           with scoped budget + permissions
       perms)       perms)
```

**Adapters ("if it can receive a heartbeat, it's hired"):** OpenClaw, Claude Code, Codex, Cursor, Bash, HTTP/webhook bots, plus external adapter plugins. Agents bring their own prompts, models, and runtimes. → [[bring-your-own-agent]], [[openclaw]]

## The twelve-system control plane

Paperclip is a full control plane, not a wrapper. Twelve server-side systems coordinate agents end to end ([[architecture]]):

| System | What it does |
|---|---|
| [[identity-and-access]] | Auth; deployment modes, board users, agent API keys, run JWTs, memberships, OpenClaw onboarding. Every mutating request traced to an actor. |
| [[org-chart-and-agents]] | Roles, titles, reporting lines, permissions, budgets, adapters. |
| [[tasks-and-tickets]] | Issues with full goal ancestry, atomic checkout + execution locks, blockers, comments, attachments, work products. |
| [[heartbeats]] | DB-backed wakeup queue (with coalescing) that runs agents — the execution engine. |
| [[workspaces-and-runtime]] | Project + isolated execution workspaces (git worktrees, operator branches), dev servers, preview URLs. |
| [[governance-and-approvals]] | Approval workflows, execution policies, pause/resume/terminate, revisioned config with rollback, budget hard-stops. |
| [[budget-and-cost-control]] | Token/cost tracking by company/agent/project/goal/issue/provider/model; scoped budget policies with warnings + hard stops. ⚠️ Hard-stops don't fire under subscription billing (see pitfalls). Operator playbook: [[cost-optimization]]. |
| [[routines-and-schedules]] | Recurring work via cron / webhook / API triggers; each run creates a tracked issue. |
| [[plugins]] | Out-of-process extension system: capability-gated host services, job scheduling, tool exposure, UI contributions. |
| [[secrets-and-storage]] | Instance + company secrets (encrypted local), object storage, attachments, work products. |
| [[activity-and-events]] | Durable audit log of actions, heartbeat state changes, cost events, approvals, comments. |
| [[company-portability]] | Export/import whole organizations via `companies.sh`, with secret scrubbing + collision handling. |

**Cross-cutting concepts** that span many systems: [[goal-alignment]], [[multi-company-isolation]], [[skills]] (runtime skill injection).

## How the pieces connect (execution lifecycle)

A [[heartbeats|heartbeat]] is the spine that ties the systems together. On each wake, a run:
1. **Budget check** ([[budget-and-cost-control]]) — overspend pauses the agent and cancels queued work.
2. **Workspace resolution** ([[workspaces-and-runtime]]) — right directory, right context.
3. **Secret injection** ([[secrets-and-storage]]) — only what the scoped run needs.
4. **Skill loading** ([[skills]]) — picks up org-specific workflows at runtime.
5. **Adapter invocation** ([[bring-your-own-agent]]) — the actual agent runs.
6. **Outputs** — structured logs, cost events, session state, audit trails ([[activity-and-events]]).

Tasks ([[tasks-and-tickets]]) are atomically checked out (no double-work), executed across heartbeats with **persistent session state** (resume context, don't restart), reviewed under [[governance-and-approvals]], metered by [[budget-and-cost-control]], and can be generated automatically by [[routines-and-schedules]]. Everything is company-scoped for [[multi-company-isolation]] and portable via [[company-portability]]. "Atomic execution" = atomic checkout + budget enforcement together.

## Key commands

For the full end-to-end runbook (install → company → hire → cost-safe config → go live), see [[setup-sop]].

**Quickstart** (open source, self-hosted, no Paperclip account; → [[installation-and-setup]]):
```
npx paperclipai onboard --yes                 # trusted local loopback (fastest first run)
npx paperclipai onboard --yes --bind lan      # authenticated/private over LAN
npx paperclipai onboard --yes --bind tailnet  # authenticated/private over Tailscale
npx paperclipai configure                      # edit settings (onboard keeps existing config)
```

**Manual / dev:**
```
git clone https://github.com/paperclipai/paperclip.git
cd paperclip && pnpm install && pnpm dev       # API at http://localhost:3100, embedded Postgres auto-created
```

**Dev scripts:** `pnpm dev`, `dev:once`, `dev:server`, `build`, `typecheck`, `test` (Vitest), `test:watch`, `test:e2e` (Playwright), `db:generate`, `db:migrate`. Note: `pnpm test` does **not** run Playwright.

**Company export/import:** `companies.sh` ([[company-portability]]).

**Telemetry** (anonymous, on by default; no prompts/secrets, private repo refs hashed). Disable with any of:
```
PAPERCLIP_TELEMETRY_DISABLED=1   DO_NOT_TRACK=1   CI=true   # or telemetry.enabled: false in config
```

## Cost: the #1 real-world pain (levers + a bug)

Cost is the most-reported friction. A community "test hire" burned **757K tokens**; subscription users report blowing weekly limits. The five levers ([[cost-optimization]], [[token-usage-in-paperclip]]):

1. **Model** — adapter picks the model; not every agent needs Opus/Sonnet 4.6, or even Claude. → [[bring-your-own-agent]]
2. **Cadence** — heartbeat interval in **seconds** (`5`=5s, `60`=1min, `360`=1hr); the biggest lever. Match to the job; some agents run manual-only. → [[heartbeats]]
3. **Instructions/skills** — packaged as input tokens *every run* (~5K off the bat); don't assign unused [[skills]].
4. **Budgets** — per-agent hard stop (but see bug below). → [[budget-and-cost-control]]
5. **Measure** — tokens in (tiny, ~54 = "wake & run") vs out (the bulk) vs **cached (~10× cheaper)**.

**⚠️ The $0-cost bug:** agents on a Claude **subscription** (Max plan via "claw local" passthrough, not the API) show cost as **$0**, so **budget hard-stops never trigger**. Workaround: prompt Paperclip to query its **embedded Postgres (port 54329)**, read `cost_events`, apply API pricing, and backfill inferred cost to the UI (demo showed ~$2/agent). → [[cost-optimization]]

**Cheap-scan pattern:** run a small local Ollama model hourly for web scans → file; a premium agent reads it once daily.

## Other gotchas

- **OpenClaw integration issues** recur in Discussions — [[openclaw]] connects as an HTTP/webhook bot; onboarding via [[identity-and-access]].
- **Deployment-mode confusion.** Default is trusted-local loopback (no auth); for off-box access use `--bind lan`/`--bind tailnet` (authenticated). → [[identity-and-access]]
- **Coarse roles.** Only board users + agent keys today; richer roles (Admin/Operator/viewer) are a community request, not yet shipped.

## Status: shipped vs planned ([[roadmap]])

- **Shipped:** plugin system, OpenClaw/claw-style agents, `companies.sh` import/export, AGENTS.md configs, Skills Manager, Scheduled Routines, better budgeting, agent reviews & approvals, multiple human users.
- **Planned:** Cloud/Sandbox agents (Cursor/e2b), Artifacts & Work Products, **Memory/Knowledge** (active community thread), Enforced Outcomes, MAXIMIZER MODE, Deep Planning, Work Queues, Self-Organization, Automatic Organizational Learning, CEO Chat, Cloud deployments, Desktop App.

## Community & ecosystem ([[community-and-ecosystem]])

Discord, Twitter/X (@papercliping), GitHub Issues/Discussions, website paperclip.ing. Plugin directory: **awesome-paperclip**. Maintainer `cryppadotta` seeded the pinned Plugin System discussion plus Evals and Memory threads. Notable community builds: a "Zero-Human Journalism Company," a LINE Messaging API plugin (APAC), a multi-account Codex router, and "Paperclip for free" via Gemma + subscription rotator. Adapter ecosystem beyond defaults: OpenCode + LiteLLM, DeepSeek, Gemma, PicoClaw (OpenClaw-like).

## Quick facts

- **License:** MIT © 2026 Paperclip Labs, Inc.
- **Stack:** Node.js server + React UI; embedded PostgreSQL auto-created (port `54329`; holds `cost_events` — point at your own Postgres in prod, deploy e.g. Vercel).
- **API:** `http://localhost:3100`.
- **Requirements:** Node.js 20+, pnpm 9.15+.

## Open questions / data gaps

- Will Paperclip fix the **$0-cost bug** so budget hard-stops work under subscription billing? (Until then, Postgres backfill is the only way to see real spend.)
- Maturity of the [[plugins|plugin]] system and what's actually in *awesome-paperclip*.
- Status of planned **Memory/Knowledge** work.
- How deployment/bind modes behave for solo vs team setups in practice.
- No official docs (paperclip.ing/docs) or DEVELOPING.md ingested yet — next ingest targets.
