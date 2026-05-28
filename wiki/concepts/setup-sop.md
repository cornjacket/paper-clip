---
type: concept
name: Setup SOP (Standard Operating Procedure)
tags: [sop, setup, install, how-to, runbook, onboarding]
---

A step-by-step runbook for standing up [[paperclip|Paperclip]] from nothing to a running, cost-safe company of agents. This is the procedural how-to; [[installation-and-setup]] is the reference for commands/flags and [[cost-optimization]] for the tuning rationale.

> Scope: a self-hosted, single-operator or small-team deployment. Every step traces to a source; UI-level details come from [[token-usage-in-paperclip]], infra from [[paperclip-readme]]. Steps marked **(gap)** are not fully documented in current sources — verify in the app.

## 0. Prerequisites

- [ ] **Node.js 20+** and **pnpm 9.15+** installed ([[installation-and-setup]]).
- [ ] **An agent runtime + provider credentials** ready — e.g. the Claude CLI authenticated (the "claw local" adapter passes through your subscription). Any of OpenClaw, Claude Code, Codex, Cursor, Bash, or an HTTP/webhook bot works ([[bring-your-own-agent]]).
- [ ] Decide the **deployment mode** up front (see Step 2): trusted local loopback, or authenticated LAN/tailnet ([[identity-and-access]]).
- [ ] Optional: a **local model** (e.g. Ollama Qwen 8B) if you plan to use the cheap-scan pattern ([[cost-optimization]]).

No Paperclip account is required — it's open source and self-hosted.

## 1. Install & launch the server

Pick one path.

**A. Quickstart (fastest first run):**
```
npx paperclipai onboard --yes
```
Defaults to trusted local loopback. Re-running `onboard` preserves existing config.

**B. Manual / dev (for hacking or production base):**
```
git clone https://github.com/paperclipai/paperclip.git
cd paperclip && pnpm install && pnpm dev
```
Starts the API at `http://localhost:3100` with an auto-created embedded PostgreSQL (port `54329`).

## 2. Choose & apply the deployment mode

- **Trusted local (loopback)** — default, no auth; fine for a solo machine.
- **Authenticated / private** — required for anything reachable off-box. Pick a bind preset:
  ```
  npx paperclipai onboard --yes --bind lan       # other devices on your network
  npx paperclipai onboard --yes --bind tailnet   # private access over Tailscale (good for solo-on-the-go)
  ```
Modes map to [[identity-and-access]]. Use `npx paperclipai configure` to change settings later.

## 3. Verify the install

- [ ] Open `http://localhost:3100` — the React dashboard loads.
- [ ] (Optional) Confirm embedded Postgres is up on port `54329`.
- [ ] If you chose LAN/tailnet, confirm auth is enforced from a second device.

## 4. Create the company & define the goal

1. Create a **company** (every entity is company-scoped; one deployment can hold many — [[multi-company-isolation]]).
2. Set the **top-level goal** — concrete and measurable, e.g. "Build the #1 AI note-taking app to $1M MRR." This goal becomes the ancestry every task inherits ([[goal-alignment]]). This is step 1 of the Paperclip model.

## 5. Hire the team (build the org chart)

For each agent ([[org-chart-and-agents]]):
1. Add the role/title and **reporting line** (boss) — e.g. CEO → CTO → engineers.
2. Choose the **adapter**, which selects the model. Authenticate the underlying runtime first. Use "claw local" for subscription passthrough, or point at a cheaper/local model where appropriate ([[bring-your-own-agent]]).
3. Write a lean **job description / instructions**. Keep it tight — instructions are re-sent as tokens every run ([[skills]], [[cost-optimization]]).
4. Assign **only the skills the agent needs** — unused skill definitions still cost tokens ([[skills]]).

"If it can receive a heartbeat, it's hired."

## 6. Configure for cost safety (do this before going live)

This is the step most people skip and regret — cost is the #1 real-world pain ([[cost-optimization]]). Per agent:

- [ ] **Cadence** — set the [[heartbeats|heartbeat]] interval in **seconds** to match the job (`360` = hourly; daily/weekly for most). Set low-value agents to **manual/trigger-only**. Cadence is the biggest cost lever.
- [ ] **Model** — reserve frontier models (Opus/Sonnet 4.6) for agents that need them; downgrade or use local models elsewhere.
- [ ] **Budget** — set a per-agent budget hard-stop ([[budget-and-cost-control]]).
- [ ] ⚠️ **Verify cost is actually measured.** If agents bill against a Claude **subscription**, Paperclip may report **$0**, which means **budgets never trigger**. Confirm spend appears; if not, apply the Postgres-backfill workaround (query `cost_events` on port `54329`, apply API pricing) from [[cost-optimization]].

## 7. Approve & run

1. Review strategy and **approve** hires/plans via the board ([[governance-and-approvals]]).
2. **Do a manual run first** on one agent to validate behavior and see token in/out before enabling timers.
3. Enable scheduled [[heartbeats]] (and any recurring [[routines-and-schedules]]).
4. Monitor from the dashboard — activity, cost, and approvals ([[activity-and-events]]).

You can pause, resume, or terminate any agent at any time, and roll back bad config changes ([[governance-and-approvals]]).

## 8. Telemetry (optional)

Anonymous telemetry is **on by default** (no prompts/secrets; private repo refs hashed). To disable, set any of: `PAPERCLIP_TELEMETRY_DISABLED=1`, `DO_NOT_TRACK=1`, `CI=true`, or `telemetry.enabled: false` in config ([[installation-and-setup]]).

## 9. Production & portability (when ready)

- Point Paperclip at **your own Postgres** and deploy (e.g. Vercel) instead of the embedded DB ([[installation-and-setup]]).
- Use `companies.sh` to **export/import** a whole company as a reusable template (secrets scrubbed) — [[company-portability]].

## Quick checklist

1. Node 20+/pnpm 9.15+ + authenticated agent runtime → 2. `npx paperclipai onboard --yes` (+ bind mode) → 3. verify `:3100` → 4. company + goal → 5. hire org chart → 6. set cadence/model/budget + confirm cost shows → 7. approve, manual-run, then schedule → 8. telemetry → 9. prod DB + `companies.sh`.

Parent: [[installation-and-setup]] · Source: [[paperclip-readme]], [[token-usage-in-paperclip]]
