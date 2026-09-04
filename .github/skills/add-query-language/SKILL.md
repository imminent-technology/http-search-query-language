---
name: add-query-language
description: 'Add a new query language to this repository''s portfolio: catalog it in list.csv/list.md, research and score it against the 10-criterion rubric, create its evaluation folder (JSON + Markdown), and update the aggregate summary.json/summary.md — including the Media types table and the Observations section. Use whenever asked to add, catalog, or evaluate a new query language for this project.'
argument-hint: 'Name of the query language to add (e.g. "JMESPath")'
---

# Add a Query Language Evaluation

## When to use

The user wants to add a query language that isn't yet in `query-languages/list.csv` to this repository's research portfolio, fully evaluated and folded into the aggregate summaries.

## Reference files (source of truth — read before acting, don't duplicate their content here)

- [`query-languages/list.csv`](../../../query-languages/list.csv) / [`list.md`](../../../query-languages/list.md) — the catalog table.
- [`query-languages/evaluation.md`](../../../query-languages/evaluation.md) — the 10 criteria definitions (Expressiveness, Simplicity, Flexibility, Community and Ecosystem, Extensibility, Transport Compatibility, Standardization, Security, Performance, Orthogonality).
- [`query-languages/evaluations/rubric.md`](../../../query-languages/evaluations/rubric.md) — the 1-5 scoring scale, per-criterion anchors, category taxonomy, slug-naming rule, per-language JSON/Markdown schema, and sourcing constraints.
- [`query-languages/evaluations/summary.json`](../../../query-languages/evaluations/summary.json) / [`summary.md`](../../../query-languages/evaluations/summary.md) — aggregate outputs to update.
- Any existing folder under `query-languages/evaluations/` (e.g. `graphql/graphql.json` + `graphql/graphql.md`) as a concrete formatting example.

## Procedure

### 1. Gather required information

Ask the user (via clarifying questions) for anything not already given in the request:

- **Title** — exact display name, as it should appear in `list.csv`'s Title column.
- **Official documentation URL**.
- **Short description** — the link text used in the catalog (usually the language's expanded/full name).
- Optionally, a **category hint** from the taxonomy in `rubric.md` — otherwise determine it during research.

Before doing anything else, check `list.csv`, `list.md`, and the folder names under `query-languages/evaluations/` for an existing entry with the same or a very similar title.

**A shared name is not automatically a duplicate.** Different query languages can legitimately share the same common name or acronym (e.g. this catalog's Cassandra "CQL" is unrelated to HL7's Clinical Quality Language or OGC's Common Query Language, both also abbreviated "CQL"). Disambiguate before deciding how to proceed:

- **Same title *and* the same (or effectively the same) official documentation URL/underlying language** → true duplicate. Tell the user it's already cataloged (link to the existing entry/folder) and stop — don't create a second entry unless they explicitly confirm they want to re-evaluate it.
- **Same title but a different official documentation URL/underlying language** → a legitimate name collision, not a duplicate. Proceed as a brand-new entry, but see "Handling name collisions" below for how to keep it from clashing with the existing one on disk and in the comparison tables.

### 2. Catalog the language

- Compute the slug: kebab-case of the Title (see the "File naming" section of `rubric.md` for edge cases, e.g. `SQL++` → `sql-plus-plus`).
- If that slug is already used by an *unrelated* language (a name collision, per step 1), pick a disambiguated slug instead — see "Handling name collisions" below — and confirm it with the user before creating any files.
- Add one row to `list.csv` (`"Title","[Description](URL)"`) and one to `list.md` (`| Title | [Description](URL) |`), inserted in strict alphabetical order by Title — both files are alphabetically sorted today. Both rows may show the exact same Title text when it's a genuine name collision; the Description column (always the expanded/full name) is what disambiguates them for a reader.

#### Handling name collisions

When two unrelated languages legitimately share a title:

- **Slug**: since each language lives at `<slug>/<slug>.{json,md}`, the new entry needs a slug that doesn't collide on disk. Append a short, meaningful qualifier derived from its expanded name, publishing organization, or domain (e.g. a second `CQL` from OGC's geospatial filtering spec → `cql-ogc`, not `cql-2`). Only fall back to a plain numeric suffix (e.g. `cql-2`) if no short, recognizable qualifier is available.
- **Comparison tables**: in `summary.md`'s category tables and the Media types table, link the new entry with a disambiguated label, e.g. `CQL (OGC)` instead of a bare `CQL`, so two identical-looking links never appear pointing to different places in the same table.
- **Per-language file**: keep the file's own `title` field and `# Heading` as the plain common name (matching `list.csv`'s Title column) — the disambiguation only needs to live in the slug and in table link labels, not in the language's own display name.

### 3. Research the language

No general web-search tool is available for this work — only fetch specific, identifiable URLs (official docs, a Wikipedia page verified to actually be about this language, standards-body pages, vendor blog/spec pages linked from the official docs). Never fabricate a source's title, publisher, or date; use `null`/`(n.d.)` when a source has no stable date.

- Fetch the official docs URL and any spec/standard pages it links to.
- Look for a canonical Wikipedia page.
- For the media type, check the [IANA Media Types registry](https://www.iana.org/assignments/media-types/media-types.xhtml) and the vendor's/standard's own docs. Don't infer it — if nothing verifiable turns up, record "None known" (or "Not applicable" if the language has no wire format at all, e.g. a language-integrated/in-process API).

### 4. Score the language

Follow `evaluation.md` for what each criterion means and `rubric.md` for the 1-5 scale and per-criterion anchors. For each of the 10 criteria (`expressiveness`, `simplicity`, `flexibility`, `communityAndEcosystem`, `extensibility`, `transportCompatibility`, `standardization`, `security`, `performance`, `orthogonality`) write a 1-3 sentence rationale grounded in a cited source — never an unsupported score. Assign a `category` from the existing taxonomy (propose a new one only if none genuinely fit, and confirm it with the user first). Compute `overallScore` as the unweighted average of the 10 scores, rounded to one decimal.

### 5. Create the per-language files

Create `query-languages/evaluations/<slug>/<slug>.json` and `<slug>/<slug>.md`, following the schema documented in `rubric.md` (`title`, `slug`, `officialDocUrl`, `mediaType`, `category`, `sources[]`, `scores{}`, `overallScore`, `summary`, `evaluatedDate` = today's date). Mirror an existing pair (e.g. `graphql/graphql.json` + `graphql/graphql.md`) exactly for formatting. Cite sources in APA style in the Markdown file's "Sources" section.

### 6. Update the aggregate summary files

- `summary.json`: append a compact object (`title`, `slug`, `category`, `officialDocUrl`, `mediaType`, `scores`, `overallScore`), placed near other entries of the same category to mirror `summary.md`'s grouping. `title` stays the plain common name even for a name collision — `slug` is what keeps the two entries distinct.
- `summary.md`:
  - Add a row to the matching `## <Category>` table (create a new category section — placed after the existing ones — only if it's genuinely a new category not in the taxonomy). If this entry is a name collision (per step 1/2), use the disambiguated label (e.g. `CQL (OGC)`) as the row's link text instead of the bare title.
  - Update the "Status: N of N languages evaluated" line to the new total and mention the addition.
  - Add a row to the "## Media types" table, in the same relative position as its category table above, using the same disambiguated label if applicable.

### 7. Update the Observations section

Read the existing "## Observations so far" bullets in `summary.md`. Only touch this section when the new language's data actually changes something material — don't pad it for every addition:

- If it changes a superlative claim ("the highest/lowest overall score...", "only N languages score X on..."), update that exact bullet with the corrected number/language, re-verified against the full updated dataset.
- If it meaningfully reinforces, extends, or contradicts an existing pattern (e.g. a new data point in a category a bullet already discusses), append a short addition to that bullet or add a new one — grounded strictly in facts established during this evaluation, never speculation.
- If nothing material changes, leave the section untouched.

### 8. Validate

- Confirm the new JSON file parses.
- Confirm `list.csv` and `list.md` each gained exactly one row, in the correct alphabetical position, with matching Title/Description.
- Confirm `summary.json` is still valid JSON and `summary.md`'s tables/counts are internally consistent (row counts, "Status: N of N" line).
- If this was a name collision, confirm the new slug/folder doesn't overwrite the existing one, and that every link to the new entry in `summary.md` uses the disambiguated label consistently.
- Report a concise summary of every file created/changed.

## Notes

- Scores are descriptive snapshots for a future comparison article, not a ranking — keep the same neutral, comparative tone used throughout the existing evaluations.
- A niche/low-documentation language may only have one usable source; note that explicitly rather than fabricating a second one.
