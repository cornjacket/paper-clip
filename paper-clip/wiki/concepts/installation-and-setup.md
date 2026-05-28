---
type: concept
name: Installation & Setup
tags: [setup, install, quickstart, deployment, config]
---

How to install and run [[paperclip|Paperclip]]. Open source, self-hosted, no Paperclip account required. For the full end-to-end runbook (install → company → hire → cost-safe config → go live), follow [[setup-sop]].

## Quickstart
```
npx paperclipai onboard --yes
```
Defaults to **trusted local loopback** mode for the fastest first run. For authenticated/private mode, pick a bind preset:
```
npx paperclipai onboard --yes --bind lan
npx paperclipai onboard --yes --bind tailnet
```
Re-running `onboard` keeps existing config; use `paperclipai configure` to edit settings. Deployment modes map to [[identity-and-access]].

## Manual / dev
```
git clone https://github.com/paperclipai/paperclip.git
cd paperclip
pnpm install
pnpm dev
```
Starts the API at `http://localhost:3100` with an auto-created embedded PostgreSQL (reachable on port `54329`, per [[token-usage-in-paperclip]] — useful for querying `cost_events` directly; see [[cost-optimization]]). **Requirements:** Node.js 20+, pnpm 9.15+.

Dev scripts: `pnpm dev`, `dev:once`, `dev:server`, `build`, `typecheck`, `test` (Vitest), `test:watch`, `test:e2e` (Playwright), `db:generate`, `db:migrate`. `pnpm test` does not run Playwright.

## Production
Point it at your own Postgres and deploy as you like (e.g. Vercel). Solo users can reach it on the go via Tailscale (pairs with the `tailnet` bind).

## Telemetry
Anonymous usage telemetry is **enabled by default** (no personal info, prompts, or secrets; private repo refs are hashed). Disable with `PAPERCLIP_TELEMETRY_DISABLED=1`, `DO_NOT_TRACK=1`, `CI=true`, or `telemetry.enabled: false` in config.

Parent: [[paperclip]] · Source: [[paperclip-readme]]
