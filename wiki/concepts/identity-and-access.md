---
type: concept
name: Identity & Access
tags: [identity, auth, access, deployment]
---

Identity & Access covers how people and agents authenticate, with every mutating request traced to an actor.

## Details
- **Two deployment modes**: trusted local (loopback) or authenticated/private. See bind presets in [[installation-and-setup]].
- Board users, agent API keys, short-lived run JWTs, company memberships, invite flows, and [[openclaw|OpenClaw]] onboarding.

## Connections
Underpins [[multi-company-isolation]], [[governance-and-approvals]], and per-actor [[activity-and-events|audit]]. The community has requested richer roles (Admin/Operator/viewer) — see [[paperclip-github-discussions]].

Parent: [[architecture]] · Source: [[paperclip-readme]]
