# Log

Append-only and chronological. Each entry starts with `## [YYYY-MM-DD] <op> | <title>` so it stays
greppable: `grep "^## \[" wiki/log.md | tail -5`.

## [2026-05-27] init | Wiki scaffolded
Created the LLM Wiki structure for researching PaperClip AI (how to use and set it up): the `raw/`
source layer, the `wiki/` page layer, the `CLAUDE.md` schema, and the index/overview/log seeds. No
sources ingested yet.
