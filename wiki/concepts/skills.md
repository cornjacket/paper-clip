---
type: concept
name: Skills (Runtime Skill Injection)
tags: [skills, runtime, context]
---

Agents can learn Paperclip workflows and project context at runtime — without retraining — via runtime skill injection.

## Details
Skills are loaded during [[heartbeats|heartbeat execution]] and are part of what gets exported/imported in [[company-portability]]. A **Skills Manager** has shipped per the [[roadmap]].

## Connections
Lets any [[bring-your-own-agent|adapter agent]] pick up org-specific know-how on the fly.

## Cost note
Skill definitions and agent instruction files are packaged into the prompt as input **tokens on every run** (a creator cites ~5K tokens off the bat), so over-assigning skills directly raises cost. Give an agent only the skills it actually uses — even unused skill definitions are billed. See [[cost-optimization]] and [[token-usage-in-paperclip]].

Parent: [[architecture]] · Source: [[paperclip-readme]], [[token-usage-in-paperclip]]
