---
type: concept
name: Quality-Assurance Loops (Compounding Error)
tags: [qa, reliability, governance, review]
---

Reviewer hierarchies that catch errors before a deliverable reaches you — Paperclip's answer to *compounding error* in long agent chains.

## The compounding-error problem
Chained autonomous steps multiply their failure rates. The framing from [[top-level-summary]]: 10 sequential tasks each ~95% accurate yield only ~0.95¹⁰ ≈ **60%** end-to-end accuracy. The longer the chain, the worse it compounds.

## The mitigation
Define **rigid reporting hierarchies** in the [[org-chart-and-agents|org chart]] — e.g. an **Engineer agent → QA agent review loop** — so a reviewer resets the error probability before work surfaces to the human "board." This rides on Paperclip's existing review/approval machinery rather than being a separate system.

## Connections
- Enforced through [[governance-and-approvals]] (review/approval stages, pause/resume) and the reporting lines in [[org-chart-and-agents]].
- Complements [[goal-alignment]]: catching drift from the goal, not just code defects.

> Note: the compounding-error framing and the explicit "Engineer → QA loop" come from a secondary summary ([[top-level-summary]]); the underlying review/approval stages are confirmed by [[paperclip-readme]] via [[governance-and-approvals]].

Parent: [[architecture]] · Source: [[top-level-summary]], [[paperclip-readme]]
