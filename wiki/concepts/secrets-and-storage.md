---
type: concept
name: Secrets & Storage
tags: [secrets, storage, security]
---

Secrets & Storage keeps sensitive values out of prompts unless a scoped run explicitly needs them.

## Details
- Instance and company secrets; encrypted local storage.
- Provider-backed object storage, attachments, and work products.

## Connections
Secrets are injected during [[heartbeats|heartbeat runs]] and scrubbed on export ([[company-portability]]). Scoped per company for [[multi-company-isolation]].

Parent: [[architecture]] · Source: [[paperclip-readme]]
