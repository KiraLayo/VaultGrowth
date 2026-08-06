# LLM Wiki — Schema

This vault is a **personal growth & learning knowledge base** structured per the [[raw/llm-wiki]] pattern. The user is learning across multiple domains — technology, foreign languages, philosophy, and any other intellectual pursuit that catches their attention. Your job is to make this knowledge compound: every source ingested and every question answered should leave the wiki richer than before.

## Vault purpose

The user is not just passively collecting information — they're actively building skills, deepening understanding, and forming their own views. The wiki should reflect this:

- **Track progress**: what's been learned, what's next, what's connected to what.
- **Surface connections**: a programming concept that mirrors a philosophical idea; a grammar pattern that clicks because of a concept from another language.
- **Enable review**: pages should be structured so the user can revisit and reinforce past learning.
- **Build upward**: foundational concepts link to advanced ones; summaries evolve into syntheses.

## Directory structure

```
index.md              # Master catalog of every wiki page (link + one-line summary)
log.md                # Chronological append-only activity log
raw/                  # Immutable source documents — never modified by LLM
  assets/             # Images from clipped/imported raw sources
  articles/           # Web articles, blog posts, clipped content
  books/              # Book notes, chapter summaries, highlights
  courses/            # Course materials, lecture notes, syllabi
  other/              # Videos, podcasts, personal notes, misc
wiki/                 # All LLM-generated content — you own this
  assets/             # Images for wiki pages (diagrams, charts, screenshots)
  entities/           # "Things" in the world: technologies, tools, languages, people, schools of thought
  concepts/           # Ideas, theories, principles, vocabulary words, grammar points
  skills/             # Practical how-to: techniques, workflows, problem-solving patterns
  sources/            # Summary pages for ingested raw sources
  syntheses/          # Cross-cutting analysis, comparisons, learning roadmaps, theses
  journal/            # Periodic reflections: weekly reviews, learning milestones, "aha" moments
```

## Conventions

### Page format

Every wiki page MUST start with YAML frontmatter:

```yaml
---
type: entity | concept | skill | source | synthesis | journal | meta
domain: 技术 | 语言 | 哲学 | 元 | 通用
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: ["[[source-page-name]]"]
summary: "One-line summary"
status: 种子 | 成长中 | 成熟          # how developed is this page?
mastery: 未学 | 学习中 | 已掌握 | 待复习   # optional; your recall level, orthogonal to status
---
```

**Status meanings:**
- `种子` (seed): bare stub — a placeholder with a definition and a link or two, waiting to be filled out.
- `成长中` (growing): has substantive content but still missing connections, examples, or depth.
- `成熟` (mature): well-developed — comprehensive coverage, rich cross-links, multiple sources.

**Mastery meanings** (optional field):
- `mastery` answers "how well do I know this?" while `status` answers "how developed is this page?" — they are orthogonal.
- Use for exam points, vocabulary, or anything that needs recall tracking. Updated during Review, not during ingest.

### Page naming

| Type | Path | Example |
|------|------|---------|
| Entity | `wiki/entities/Page Name.md` | `wiki/entities/Rust.md`, `wiki/entities/Seneca.md` |
| Concept | `wiki/concepts/Page Name.md` | `wiki/concepts/Ownership (Rust).md`, `wiki/concepts/Subjuntivo.md` |
| Skill | `wiki/skills/Page Name.md` | `wiki/skills/Debugging with strace.md` |
| Source | `wiki/sources/Page Name.md` | `wiki/sources/Article - Memory Management.md` |
| Synthesis | `wiki/syntheses/Page Name.md` | `wiki/syntheses/Rust vs Go - Concurrency.md` |
| Journal | `wiki/journal/YYYY-MM-DD Topic.md` | `wiki/journal/2026-06-12 Weekly review.md` |

Use Wiki-links for all internal links. Use `[[folder/page-name|display text]]` for readability.

### Source file naming

Raw sources should follow a naming convention that makes their origin obvious:

| raw/ location | Naming pattern | Example |
|---------------|---------------|---------|
| `raw/articles/` | `YYYY-MM-DD Title.md` | `raw/articles/2026-06-12 Async Rust.md` |
| `raw/books/` | `Author - Book Title.md` or `Author - Book Title - ChNN.md` | `raw/books/Aurelius - Meditations - Book 2.md` |
| `raw/courses/` | `Platform - Course Name.md` | `raw/courses/Coursera - Algorithms Part 1.md` |
| `raw/other/` | `YYYY-MM-DD Description.md` | `raw/other/2026-06-12 Podcast - Lex on Stoicism.md` |

When you create a source summary page in `wiki/sources/`, name it to match: use the same filename (minus extension if you prefer a cleaner title) so the link is obvious.

Course material layout: `raw/articles/课程名/第N章/` per-chapter folders with
`课件总结-第N章.md` naming. Keep names stable once set.

### Images (assets)

- Source images (from courseware/clips) stay in `raw/assets/` untouched. When embedding
  into wiki pages, copy to `wiki/assets/` with a descriptive Chinese name
  (e.g. `RAID5示意图.jpeg`) and embed with `![[wiki/assets/filename]]` plus a caption:
  `> 图：xxx（课件原图）`.
- Embed position follows the image's position in the original text → the matching
  concept/knowledge section.
- Source pages keep an image manifest (file → content → embedded page).
- Missing exam figures: prefer an inline mermaid diagram (Obsidian-native) over
  generating image files.

### Domain-specific conventions

**技术 (Technology):**
- Code snippets in fenced blocks with language tag: ```` ```rust ````
- Link to official docs or spec when citing a claim.
- Distinguish between *understanding* (concept pages) and *doing* (skill pages).
- Tag with specific tech: `#rust`, `#linux`, `#networking`.

**语言 / Language (外语):**
- Vocabulary entries on concept pages with this table:
  ```markdown
  | Word | Reading | Meaning | Example | Notes |
  |------|---------|---------|---------|-------|
  | 勉強 | べんきょう | study | 日本語を勉強しています | n./suru-v. |
  ```
- Grammar points get their own concept pages, tagged with JLPT/N-level or CEFR level.
- Skill pages for learning techniques (e.g. shadowing, SRS setup).
- Tag with language: `#japanese`, `#spanish`, `#latin`.

**哲学 (Philosophy):**
- Tag by tradition/school: `#stoicism`, `#analytic`, `#buddhism`.
- Primary text references: `> Quote` with citation to source page.
- Synthesis pages for comparing traditions or tracing idea evolution.
- Distinguish between *exposition* (what X believed) and *evaluation* (your take on X).

**备考 / Exam prep (e.g. 软考):**
- Courseware (课件) is the primary source; subtitles/transcripts are supplementary — clean
  filler words and timestamps, and do NOT create a page per video lecture.
- 真题/练习 usually come embedded in the video course itself (tutorial + exercise format).
  During ingest, extract worked examples into concept pages as "真题演练" blocks (with
  answer + 常见坑), cited to the course source page. No separate exam files required; if
  standalone 真题 sets ever arrive, put them in `raw/exams/` (optional).
- Mark exam points: 必考 / 常考 / 不考. Content deleted in the current textbook edition is
  marked "已删除，不再考" so lint can spot cross-version contradictions.
- Keep a chapter learning-roadmap synthesis page as a living progress panel; update it after
  every chapter ingest.

### Linking

- Every claim should trace back to a source via `[[wiki/sources/...]]`.
- **Only source pages reference `raw/` paths** — their 原始文件 field is the single
  reference point for the raw file. Wiki pages never embed raw/ paths directly; they
  link raw content only through `[[wiki/sources/...]]` pages.
- Default to **short-form links** `[[Page Name]]` (Obsidian resolves by filename).
  Use full paths `[[wiki/entities/Page]]` only when basenames collide across categories;
  index.md entries keep full paths.
- When a raw file is renamed or moved: update only the matching source page — short links
  elsewhere need no cascade. Keep raw names stable once set: renames are the most
  expensive wiki operation.
- **Source conflicts**: when sources disagree (e.g. courseware vs video), keep both
  versions on the page with a `> 口径说明` block quoting each source; the textbook/真题
  wins. Flag, don't silently pick one.
- Cross-link aggressively across domains — a programming concept that mirrors a philosophical idea is gold.
- Link to prerequisite concepts. A page on Rust traits should link to type systems; a page on subjunctive should link to indicative.
- If you mention something that should have its own page but doesn't yet, **create it as a seed** immediately.

### Index (index.md)

- Organized by category, with domain sub-sections within each category.
- Each entry: `- [[wiki/entities/Page Name]] — summary (YYYY-MM-DD, N sources, 🌱/🌿/🌳)` (use full paths to avoid name collisions across categories)
- 🌱 = 种子 (seed) · 🌿 = 成长中 (growing) · 🌳 = 成熟 (mature)
- Update on every ingest. Read first when answering queries.
- Progress/status claims live in ONE place (the chapter roadmap synthesis page / the
  relevant entity page); meta pages reference these instead of copying volatile state.

### Log (log.md)

- Append-only. Format each entry:
  ```
  ## [YYYY-MM-DD] {ingest | query | lint | review | journal | init} | Brief description
  ```
- For ingests: list files created/updated and the raw source that triggered it.
- For queries: note what was asked and whether output was filed as a synthesis or journal entry.
- For reviews: note progress, insights, next goals.

## Operations

> **Confirm before ingesting.** For every ingest, first state the scope and granularity —
> which raw files, roughly how many wiki pages, and whether this is a single source or a
> chapter-level batch. If the user explicitly listed the files and asked for ingest,
> proceed after stating scope; if intent is unclear or the request is open-ended,
> WAIT for the user's OK. Never ingest a whole course or a large backlog of files in one go.

### Ingest a source

When the user drops a file into `raw/` and asks you to ingest it:

1. **Read** the source — text first, then any referenced images in `raw/assets/`.
2. **Discuss** key takeaways with the user. What stood out? What surprised them? What contradicts or extends prior knowledge? What do they want to practice or apply?
3. **Write** a source summary page in `wiki/sources/`.
4. **Update** every entity, concept, and skill page touched by the source — add information, flag contradictions, strengthen claims.
5. **Create** new seed pages for anything important that doesn't have one yet.
6. If the answer or new content warrants a visual (diagram, chart, comparison table as image), generate it and save to `wiki/assets/`. Embed with `![[wiki/assets/filename]]`.
7. **Update** `index.md` with entries for every new or changed page.
8. **Append** to `log.md` recording what was done.

A single source typically touches 5–15 wiki pages. Be thorough.

### Ingest a course chapter (incremental batch)

For course-based learning (exam prep, language courses) where raw material arrives chapter
by chapter and learning deepens over time:

1. **Confirm scope first** — which chapter, which files, batch granularity (see rule above).
2. **Read** the chapter's courseware as the skeleton, then subtitles/transcripts as
   supplementary detail (skip filler words and timestamps). **Extract any 题目/练习
   embedded in the lectures** — this course format is tutorial + exercises, so worked
   examples live inside the video content itself.
3. **Discuss** learning-oriented takeaways: new exam points, formula changes, claims that
   contradict earlier chapters.
4. **Create seeds only for genuinely new concepts.** Before creating any page, run a quick
   vault-wide grep on the proposed concept name (plus likely synonyms) — any hit means
   **incremental merge** instead: new facts, examples, and contradictions go into the
   existing page. Never create a second page for an existing concept. Each lecture may
   contribute new worked examples — they accumulate in the same page's 真题演练 block,
   never in a new page.
5. **Update** the chapter's learning-roadmap synthesis page (check off completed modules).
6. **Update** `index.md` (only pages touched this round) and append `log.md`.
7. **Mark** `mastery: 待复习` on calculation/recall-heavy pages.
8. **Remind** the user of pending review items from earlier chapters.

### Re-ingest an updated source

When the user updates a raw file (e.g. courseware gains images or revisions):

1. Compare the new content against the source page and affected wiki pages.
2. Rewrite the source page (structure, image manifest, new details).
3. Merge new/changed facts into existing pages — never create duplicate pages.
4. Handle new images per the Images conventions above.
5. Note remaining gaps (missing figures → mermaid) and log as `ingest | 重摄入`.

### Answer a query

1. **Read** `index.md` to find relevant pages.
2. **Read** those pages, following links as needed. If the answer requires it, read from `raw/` sources directly too.
3. **Synthesize** an answer with citations (`[[wiki/page-name]]`).
4. **Ask** the user if the answer should be filed — as a synthesis page, a concept page, or a journal entry. If yes, write it and update index + log.

### Review (spaced revisit)

When the user wants to review past learning:

1. Check `index.md` for pages with `status: 种子` or `status: 成长中` — these are candidates for reinforcement.
2. Re-read the page, then ask the user a few probing questions to test recall.
3. Update the page with any new insights that come up during review. Promote `种子 → 成长中` or `成长中 → 成熟` if appropriate.
4. Log the review session in `log.md`.

Additional rules:

- For calculation-type pages (exam prep), cover the formula and redo the steps from memory;
  update the page's 常见坑 section with anything that tripped you up.
- Update `mastery` on reviewed pages (已掌握 / 待复习) and tick the roadmap checklist.
- Review sessions are the trigger for promoting `种子 → 成长中 → 成熟`.

### Journal

When the user reflects on their learning (weekly review, milestone, insight):

1. Create an entry in `wiki/journal/` dated and titled.
2. Link to relevant pages they've engaged with recently.
3. Note what's working, what's not, what to adjust.
4. This is the user's space — their voice and perspective take priority. You're here to help structure and connect, not to overwrite.

### Lint the wiki

Periodically health-check. Look for:

- **Contradictions**: two pages making incompatible claims.
- **Stale claims**: assertions superseded by newer sources.
- **Orphans**: pages with no inbound links.
- **Missing pages**: important concepts/entities mentioned but lacking their own page.
- **Seed debt**: too many 种子 pages that never got developed.
- **Cross-domain opportunities**: a concept in one domain that mirrors one in another, not yet linked.
- **Knowledge gaps**: topics the user clearly cares about but hasn't sourced yet.
- **Duplicate concepts**: two pages describing the same concept under different names — merge candidates.
- **Version contradictions**: claims marked "已删除/不再考" that conflict with newer sources.
- **Ingest hygiene**: recently created pages that should have been merged into existing ones.
- **Broken links**: every wikilink, raw reference, and image embed must resolve to an existing file (raw moves/renames silently break source-page references).
- **Source-page consistency**: each source page's 原始文件 link matches the actual raw file path/name.
- **Meta drift**: progress/status claims in meta pages (使用指南, entity pages) match current state.

Report findings and fix them. Log what was done.

## Tools

- Use `Read` to read pages and images.
- Use `Write` and `Edit` to create/update wiki pages.
- Use `Grep` and `Glob` to search the vault.
- Use `WebSearch` and `WebFetch` to fill knowledge gaps (when user OKs it).
- Obsidian's graph view is the best way to see wiki health — encourage the user to check it regularly.
