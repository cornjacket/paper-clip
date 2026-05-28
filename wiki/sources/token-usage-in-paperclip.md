---
type: source
title: "Token Usage in Paperclip (YouTube, by Fruit)"
source_path: "raw/transcripts-and-how-tos/Token Usage in Paperclip.md"
source_kind: transcript
date_ingested: 2026-05-27
date_published:
tags: [paperclip, cost, tokens, transcript, how-to]
---

Transcript of a YouTube walkthrough on managing token cost in [[paperclip|Paperclip]] — the first source with concrete operating numbers and cost levers. Author "Fruit" runs ~15 agents 24/7 and demos the cost settings. Feeds [[cost-optimization]] and [[budget-and-cost-control]].

## What it covers
- **Why cost hurts:** Paperclip is fun until the cost conversation; subscription users report blowing weekly limits fast.
- **The cost levers** (the core of the video) — see [[cost-optimization]]:
  1. **Model choice** — each agent's adapter picks the model; not every agent needs Opus 4.6 / Sonnet 4.6, or even Claude at all.
  2. **Heartbeat cadence** — set in seconds (5 = 5s, 60 = 1 min, 360 = 1 hr); the single biggest lever. Match cadence to purpose; some agents should only run on manual/trigger. See [[heartbeats]].
  3. **Instructions & skills** — agent instruction and [[skills|skill]] files are packaged as tokens on every run (~5K off the bat); don't assign skills an agent won't use.
  4. **Budgets** — per-agent budget stops the agent when hit ([[budget-and-cost-control]]).
  5. **Measurement** — "you cannot manage what you don't measure" (Drucker).
- **Tokens in vs out vs cached:** token-in can be tiny (54 tokens = just "wake up and run"); token-out is the bulk (verbose run output, context/env setup, auth). Cached tokens are ~10× cheaper; Claude builds a cache across runs and clears it over time.
- **Local models:** runs a small local Ollama model (e.g. Qwen 8B) hourly for cheap web-search scans that write to a file; the chief-of-staff agent reads that file once a day. See [[bring-your-own-agent]].

## Key facts & numbers
- **The $0 / subscription bug:** when an agent bills against a Claude **subscription** (Max plan) via the "claw local" adapter passthrough — rather than the Anthropic **API** — Paperclip shows cost as **$0**. Because cost reads $0, **budget hard-stops never trigger**. (Author expects Paperclip to fix this.)
- **Workaround:** prompt Paperclip to query its **embedded Postgres on port 54329** directly, read the `cost_events` / usage data, apply Anthropic API pricing to the token counts, and **backfill inferred cost** so the UI shows per-agent spend. The agent writes a Python script to do it; backfilling to the dashboard was flaky and needed repeated prompting.
- **Inferred per-agent cost** in the demo: chief of staff **$2**, career agent **$2.4**, calendar agent **$1.9** (plus pricier demo companies).
- Why subscription matters: the author's main reason to use Paperclip is to spend **subscription tokens** rather than API billing — "not so with OpenClaw."

Source: <https://www.youtube.com/watch?v=XuRfik_tHd4>
