# Log

Append-only and chronological. Each entry starts with `## [YYYY-MM-DD] <op> | <title>` so it stays
greppable: `grep "^## \[" wiki/log.md | tail -5`.

## [2026-05-27] init | Wiki scaffolded
Created the LLM Wiki structure for researching PaperClip AI (how to use and set it up): the `raw/`
source layer, the `wiki/` page layer, the `CLAUDE.md` schema, and the index/overview/log seeds. No
sources ingested yet.

## [2026-05-27] ingest | Paperclip README + GitHub Discussions
Ingested both `Clippings/` sources (README and Discussions index). Created 2 source pages, 2 entity
pages ([[paperclip]], [[openclaw]]), and 21 concept pages covering the twelve-system
[[architecture]], cross-cutting concepts ([[goal-alignment]], [[multi-company-isolation]],
[[skills]], [[bring-your-own-agent]]), and operational pages ([[installation-and-setup]],
[[positioning]], [[roadmap]], [[community-and-ecosystem]]). Dense wikilinks added with [[paperclip]]
and [[architecture]] as primary hubs. Updated [[index]] and [[overview]] (thesis + open questions).
No screenshots present in `raw/screenshots/` yet — nothing to connect.

## [2026-05-27] synth | Wiki hot cache created
Synthesized every wiki page into [[wiki-hot-cache]] — a single load-first digest covering the mental
model, org chart, the twelve-system control plane, execution lifecycle, key commands, common
pitfalls (757K-token cost burn, OpenClaw integration, bind-mode confusion), shipped-vs-planned,
community, quick facts, and open questions. Added to [[index]] under Overview. No source content
changed; derived entirely from existing pages.

## [2026-05-27] ingest | Token Usage in Paperclip (YouTube, Fruit)
Ingested the `raw/transcripts-and-how-tos/` transcript on cost. Created source page
[[token-usage-in-paperclip]] and new concept [[cost-optimization]] (five levers + the $0-subscription
bug & Postgres-backfill workaround). Folded into [[budget-and-cost-control]] (flagged a contradiction:
budget hard-stops don't fire under subscription billing), [[heartbeats]] (cadence in seconds; #1 cost
lever), [[bring-your-own-agent]] (adapter selects model; "claw local" subscription passthrough; local
Ollama), [[skills]] (defs cost tokens every run), [[org-chart-and-agents]] (per-agent tuning),
[[community-and-ecosystem]] (creator "Fruit"), and [[installation-and-setup]] (embedded Postgres port
54329). Updated [[index]], [[overview]] (open questions), and [[wiki-hot-cache]]. First source with
concrete operating numbers (per-agent cost ~$2).

## [2026-05-27] synth | Setup SOP authored
Created [[setup-sop]] — a 9-step runbook (prereqs → install → bind mode → verify → company/goal →
hire org chart → cost-safe config → approve & run → telemetry → prod/portability) synthesized from
[[installation-and-setup]], [[cost-optimization]], [[identity-and-access]], and the operating model.
Cross-linked from [[installation-and-setup]] and [[wiki-hot-cache]]; added to [[index]] under setup.
Steps not fully covered by sources are marked "(gap)". No source content changed.

## [2026-05-27] synth | "How Paperclip works" canvas
Created `wiki/how-paperclip-works.canvas` (Obsidian Canvas, 27 nodes / 21 edges) visualizing four
bands: the 3-step operating model, the org-chart hierarchy, the heartbeat run lifecycle (trigger →
budget → workspace → secrets → skills → adapter → ticket → outputs, with a resume loop), and the
cross-cutting governance/cost/data systems. All cards carry clickable wikilinks to concept pages; the
cost card flags the $0-subscription bug in red. Added to [[index]] under Overview.
