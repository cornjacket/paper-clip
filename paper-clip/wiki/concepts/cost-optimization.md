---
type: concept
name: Cost Optimization (Practical Levers)
tags: [cost, tokens, optimization, how-to, budget]
---

Practical, operator-facing levers for keeping a [[paperclip|Paperclip]] deployment affordable — the *how-to* counterpart to the [[budget-and-cost-control]] system. Distilled from a hands-on walkthrough by a creator running ~15 agents 24/7 ([[token-usage-in-paperclip]]).

## The five levers

1. **Model choice.** Each agent's adapter selects the model ([[bring-your-own-agent]]). Not every agent needs Opus 4.6 / Sonnet 4.6 — or even Claude. Reserve frontier models for agents that need them; use small/local models for the rest.
2. **Heartbeat cadence** — the single biggest lever. Cadence is set in **seconds** per agent: `5` = every 5s, `60` = every minute, `360` = every hour. 15 agents × every 5 min × Opus 4.6 burns budgets fast. Match cadence to the job (estate planning: every 6 months; chief of staff: daily; not everything needs hourly). Some agents should only run on **manual/trigger**, never on a timer. See [[heartbeats]].
3. **Instructions & skills.** Agent instruction files and [[skills|skill]] definitions are packaged into the prompt as tokens **on every run** (the author cites ~5K tokens off the bat). Keep instructions lean and **don't assign an agent skills it won't use** — even unused skill *definitions* consume input tokens.
4. **Budgets.** Set a per-agent budget so the agent stops when it hits the limit ([[budget-and-cost-control]]). Caveat: budgets are defeated by the $0-cost bug below.
5. **Measurement.** "You cannot manage what you don't measure" — you can't tune cost you can't see, which is exactly the problem with subscription billing below.

## Tokens in vs out vs cached
- **Tokens in** can be tiny — a wake-up run may send only ~54 tokens ("wake up agent, run").
- **Tokens out** are usually the bulk — verbose run output, context/environment setup, auth chatter (e.g. ~4.8K on one run).
- **Cached tokens** are ~**10× cheaper**. Claude builds a cache across runs (helps manage context in longer conversations) and clears it over time; the cache folder can be deleted manually (advanced). Large cached-token counts are *not* billed at full rate — don't panic at the raw number.

## Cheap-scan pattern (local models)
Run a small **local Ollama model** (e.g. an 8B like Qwen) on a frequent cadence for low-value, high-frequency work — e.g. hourly web-search scans that write results to a file — for ~free. A premium agent (chief of staff) then reads that file once a day to summarize. This keeps expensive model time off repetitive scanning. See [[bring-your-own-agent]].

## ⚠️ The $0 subscription-cost bug (and workaround)
When an agent bills against a Claude **subscription** (Max plan, via the "claw local" adapter passthrough) instead of the Anthropic **API**, Paperclip reports cost as **$0** — it does not compute the real cost. Two consequences:
- The dashboard understates spend (most users are on subscription, since spending subscription tokens is a main reason to use Paperclip).
- **Budget hard-stops never trigger** — a $5 budget can't be hit if cost always reads $0, defeating the safety net in [[budget-and-cost-control]] and [[governance-and-approvals]].

**Workaround** ([[token-usage-in-paperclip]]): prompt Paperclip to query its **embedded Postgres on port `54329`** directly, read the `cost_events` / usage data, apply Anthropic API pricing to the token counts, and **backfill the inferred cost** into Paperclip so the UI shows per-agent spend. The agent writes a Python script to do this; backfilling to the dashboard is flaky and may need repeated prompting. The author expects Paperclip to fix the underlying gap.

## Connections
The enforcement machinery lives in [[budget-and-cost-control]]; this page is the operator playbook on top of it. Levers touch [[heartbeats]] (cadence), [[bring-your-own-agent]] (model), [[skills]] (instruction size), and [[org-chart-and-agents]] (per-agent tuning).

Parent: [[budget-and-cost-control]] · Source: [[token-usage-in-paperclip]]
