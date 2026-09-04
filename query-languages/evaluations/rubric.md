# Evaluation rubric and file schema

This directory contains per-language evaluations of every entry in [`../list.csv`](../list.csv) against the criteria defined in [`../evaluation.md`](../evaluation.md). The evaluation is descriptive, not a ranking: the goal is to inform a comparison article, not to declare a "best" query language.

## Scoring scale

Each of the 10 criteria is scored on an integer scale from 1 (worst) to 5 (best):

| Score | Generic meaning |
|---|---|
| 1 | Absent / very poor — the language lacks this attribute or is a significant outlier in a negative way. |
| 2 | Limited — minimal or awkward support, with notable gaps compared to peers. |
| 3 | Moderate — adequate support that covers common cases without standing out. |
| 4 | Strong — robust, well-designed support with only minor gaps. |
| 5 | Excellent — best-in-class support; comprehensive with few or no limitations. |

Every score must be accompanied by a short rationale (1-3 sentences) grounded in the cited sources. Scores are inherently comparative snapshots (as of the `evaluatedDate`), not permanent judgments — languages evolve.

### Per-criterion notes

- **Expressiveness**: 5 = supports filtering, sorting, aggregation, joins, and nested/complex queries natively; 1 = only basic equality/lookup queries.
- **Simplicity**: 5 = small, readable syntax with a shallow learning curve; 1 = steep learning curve, verbose or unintuitive syntax.
- **Flexibility**: 5 = works cleanly across schema-less/dynamic and evolving data models; 1 = rigid, tightly coupled to a fixed schema.
- **Community and Ecosystem**: 5 = large active community, extensive docs/tools/libraries, active maintenance; 1 = little to no community, sparse or outdated docs, unmaintained/deprecated.
- **Extensibility**: 5 = first-class support for user-defined functions/operators/extensions; 1 = closed, fixed set of operations with no extension points.
- **Transport Compatibility**: 5 = fits naturally in a URL query string/header with minimal escaping and also works as a request body; 1 = effectively requires an out-of-band request body or heavy custom encoding to use over HTTP.
- **Standardization**: 5 = defined by a formal, vendor-neutral specification (RFC/W3C/ISO/etc.) with multiple independent implementations; 1 = single-vendor proprietary syntax with no formal spec.
- **Security**: 5 = structurally resistant to injection (parameterized/structured query building, no string concatenation needed); 1 = commonly built via raw string concatenation, prone to injection.
- **Performance**: 5 = language design enables implementations to optimize (indexes, query planning); 1 = typically forces full scans or has no optimization surface.
- **Orthogonality**: 5 = features are independent, composable, and consistent (see sub-attributes in [`../evaluation.md`](../evaluation.md)); 1 = features overlap, interfere, or require special-casing to combine.

## Category taxonomy

Assigned per language for grouping in `summary.md` and, later, the article. Adjustable during article writing.

- Relational/SQL-family
- Document/NoSQL
- Search/full-text
- Graph
- Analytics/Observability
- API/data-fetching
- Language-integrated
- Log/security search
- Scripting
- Path/document navigation
- Niche/misc

## File naming

Slug = kebab-case of the `Title` column in `list.csv` (e.g. "AWS Athena Query Syntax" → `aws-athena-query-syntax`, "SQL++" → `sql-plus-plus`). Each language gets its own folder named after its slug, containing that language's JSON and Markdown files: `<slug>/<slug>.json` and `<slug>/<slug>.md`.

## Per-language JSON schema (`<slug>/<slug>.json`)

```json
{
  "title": "string, matches list.csv Title",
  "slug": "string, kebab-case",
  "officialDocUrl": "string, from list.csv",
  "category": "string, one of the taxonomy above",
  "sources": [
    { "title": "string, the page/article title", "publisher": "string, the site/organization responsible for the source (e.g. Wikipedia, the standards body, the vendor)", "url": "string", "date": "YYYY-MM-DD, YYYY-MM, or null if no fixed publication/revision date exists (e.g. continuously-updated docs)" }
  ],
  "scores": {
    "expressiveness": { "score": 1, "rationale": "string" },
    "simplicity": { "score": 1, "rationale": "string" },
    "flexibility": { "score": 1, "rationale": "string" },
    "communityAndEcosystem": { "score": 1, "rationale": "string" },
    "extensibility": { "score": 1, "rationale": "string" },
    "transportCompatibility": { "score": 1, "rationale": "string" },
    "standardization": { "score": 1, "rationale": "string" },
    "security": { "score": 1, "rationale": "string" },
    "performance": { "score": 1, "rationale": "string" },
    "orthogonality": { "score": 1, "rationale": "string" }
  },
  "overallScore": 1.0,
  "designQualityScore": 1.0,
  "summary": "string, 2-3 sentences, neutral/comparative tone",
  "evaluatedDate": "YYYY-MM-DD"
}
```

`overallScore` is the unweighted average of the 10 criterion scores, rounded to one decimal — informational only, not a ranking signal.

`designQualityScore` is a second, additive metric: the unweighted average of only 8 of the 10 criteria — Expressiveness, Simplicity, Flexibility, Extensibility, Transport Compatibility, Security, Performance, and Orthogonality — rounded to one decimal. It deliberately excludes Community and Ecosystem and Standardization, which measure a language's adoption and governance history rather than its inherent design quality, and therefore structurally favor established, long-lived products over newer or niche ones regardless of how well-designed the language itself is. Like `overallScore`, it is informational only, not a ranking signal, and every future evaluation must compute both.

## Per-language Markdown (`<slug>/<slug>.md`)

Mirrors the JSON for human reading: title + doc link, category, a scores table (criterion | score | rationale), the summary paragraph, and a "Sources" list. Sources are cited in APA style so the publisher/organization (provenance) is always visible alongside the title and date, e.g. `- Wikipedia. (2026, August 23). [*SQL*](https://en.wikipedia.org/wiki/SQL).` or `- The PostgreSQL Global Development Group. (n.d.). [*Part II. The SQL Language*](https://www.postgresql.org/docs/current/sql.html).` when no fixed publication/revision date is available (common for continuously-updated docs and marketing pages).

## Aggregate files

- `summary.json`: array of compact objects `{ title, slug, category, officialDocUrl, mediaType, scores: { <criterion>: number }, overallScore, designQualityScore }` for all evaluated languages — data-viz friendly.
- `summary.md`: comparison matrix (languages as rows grouped by category, 10 criteria as columns, plus `Avg` (overallScore) and `DQ` (designQualityScore)) plus a short methodology note linking back to this rubric and to `../evaluation.md`.

## Sourcing constraint

No general web-search tool is available for this evaluation — secondary sources must be specific, identifiable URLs (Wikipedia, standards bodies, vendor docs/blogs) rather than search-engine queries. Niche/low-documentation languages may only have one usable source; when that happens it's noted explicitly in `sources` rather than fabricating a second one.

Each source must record its actual page/article title, its publisher/organization (the entity providing provenance — e.g. "Wikipedia", "International Organization for Standardization (ISO)", "The PostgreSQL Global Development Group") and, where the source exposes one, its publication or last-revised date (fetched from the page itself, e.g. a Wikipedia "last edited" timestamp, a standard's "Publication date", or a copyright/footer notice for the publisher name). Never fabricate a title, publisher, or date — use `null`/`(n.d.)` when the source has no stable date.
