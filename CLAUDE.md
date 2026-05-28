# PaperClip AI Research Wiki — Agent Guide

This repository is an **LLM-maintained research wiki**, following the "LLM Wiki" pattern: a
persistent, interlinked markdown knowledge base that the LLM builds and keeps current, sitting
between the user and raw sources. Knowledge is compiled once and maintained — not re-derived from
scratch on every query.

**Subject:** PaperClip AI — how to use it and set it up.

The user curates sources, directs exploration, and asks the questions. **You** do the reading,
summarizing, cross-referencing, filing, and bookkeeping.

## Three layers

1. **`raw/`** — immutable source documents (articles, papers, notes, images). Read from these;
   **never modify them.** This is the source of truth.
2. **`wiki/`** — LLM-generated markdown. You own this layer entirely: create pages, update them
   when new sources arrive, maintain cross-references, keep it internally consistent.
3. **`CLAUDE.md`** (this file) — the schema: conventions + workflows. Co-evolve it with the user
   as the domain and preferences clarify.

## Directory layout

```
raw/
  articles/   clipped web articles (markdown)
  papers/     papers, reports, PDFs
  notes/      your own notes, transcripts, podcast notes
  assets/     downloaded images referenced by sources
wiki/
  index.md    content catalog — every page, one-line summary, by category
  log.md      append-only chronological log of ingests / queries / lints
  overview.md top-level overview + evolving thesis (the wiki "home")
  sources/    one summary page per ingested source
  entities/   pages for products, components, people, orgs, tools
  concepts/   pages for concepts, topics, how-tos, comparisons
```

## Page conventions

- Every wiki page opens with YAML frontmatter (rendered by Obsidian Properties; future-proof for
  Dataview).
- The first body line is a one-sentence summary of the page.
- Link between pages with Obsidian wikilinks: `[[page-name]]`. Link liberally.
- Cite sources by linking to their summary page, e.g. `[[some-article]]` in `wiki/sources/`.
- Filenames: kebab-case and descriptive.

Frontmatter templates:

```yaml
# source page
---
type: source
title:
source_path: raw/articles/...
source_kind: article | paper | note | image
date_ingested: YYYY-MM-DD
date_published:
tags: []
---
```
```yaml
# entity page
---
type: entity
name:
category: product | component | person | org | tool
tags: []
---
```
```yaml
# concept page
---
type: concept
name:
tags: []
---
```

## Operations

### Ingest
When the user drops a source into `raw/` and asks you to process it:
1. Read the source. If it references images in `raw/assets/`, read the text first, then view the
   key images for extra context (LLMs can't read inline-image markdown in one pass).
2. Discuss key takeaways with the user (unless told to batch silently).
3. Write or update a summary page in `wiki/sources/`.
4. Update or create relevant `entities/` and `concepts/` pages — fold the new information in,
   strengthen or challenge existing claims, and **flag contradictions** with older sources
   explicitly.
5. Update `wiki/index.md` (add new pages, refresh one-liners).
6. Update `wiki/overview.md` if the big picture / thesis shifted.
7. Append an entry to `wiki/log.md`.

A single source may touch 10–15 pages. Ingest supervision style is **undecided** — default to
one-at-a-time and involved; the user will refine and this section should be updated when they do.

### Query
When the user asks a question:
1. Read `wiki/index.md` to find relevant pages, then drill into them.
2. Synthesize an answer with citations (links to source pages).
3. Offer to file valuable answers back into the wiki as new pages, so explorations compound like
   ingested sources do.

Answer formats available: markdown pages/tables, **Marp** slide decks, **matplotlib** or
**Mermaid** charts, and **Obsidian canvas** boards. Pick the format that fits the question.

### Lint
When asked to health-check the wiki, look for:
- Contradictions between pages.
- Stale claims that newer sources have superseded.
- Orphan pages (no inbound links).
- Concepts mentioned but lacking their own page.
- Missing cross-references.
- Data gaps that a web search could fill.

Also suggest new questions to investigate and new sources to look for.

## Index & log

- **index.md** is content-oriented: a catalog organized by category, each entry a wikilink + a
  one-line summary. Update it on every ingest.
- **log.md** is chronological and append-only. Start every entry with a consistent prefix so it
  stays greppable: `## [YYYY-MM-DD] ingest | Source Title` (or `query` / `lint` / `init`). Then
  `grep "^## \[" wiki/log.md | tail -5` shows recent activity.

## Rules

- Never modify anything in `raw/`.
- You own `wiki/`; keep the index, cross-links, and log current on every ingest.
- Don't invent facts about PaperClip AI. Every claim traces to a source — if something is unknown,
  say so or flag it as a data gap.
- Prefer updating an existing page over creating a duplicate.

## Optional / future

- A local markdown search engine (e.g. `qmd`) once the wiki outgrows the index file.
- Obsidian community plugins: Dataview (frontmatter queries), Marp (slides).
