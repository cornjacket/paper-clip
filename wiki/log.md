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
