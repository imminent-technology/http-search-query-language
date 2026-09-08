# Meilisearch Filter Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [Search with POST](https://www.meilisearch.com/docs/reference/api/search)
- **Media type**: None known — Meilisearch's API accepts `filter`, `sort`, and pagination parameters as fields in the JSON body of `POST /indexes/{index_uid}/search`, not a dedicated media type.
- **Evaluated**: 2026-09-07
- **Client Libraries**: Python: mature · JavaScript: mature · Java: mature · Go: partial · Rust: mature · .NET: mature
- **Support Model**: single-vendor-small-team

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | The `filter` expression supports comparisons, ranges, boolean combination with AND/OR and parentheses, and geo functions (`_geoRadius`, `_geoBoundingBox`, `_geoPolygon`), and is paired with a separate `sort` parameter and `page`/`hitsPerPage` (or `offset`/`limit`) pagination — genuinely covering filter, sort, and pagination as first-class request parameters. |
| Simplicity | 4 | The SQL-like filter syntax (e.g. `genres = horror OR genres = mystery`) is readable, though the API accepts filters as either a string or an array-of-arrays representation, and this dual representation adds a small amount of conceptual overhead. |
| Flexibility | 2 | Attributes used in `filter` or `sort` must be explicitly declared in the index's `filterableAttributes`/`sortableAttributes` settings, so filtering/sorting is scoped to a pre-configured subset of fields rather than working against arbitrary attributes out of the box. |
| Community and Ecosystem | 3 | Meilisearch is a fast-growing, actively developed open-source (MIT) search engine with a sizeable GitHub community and official SDKs, though its ecosystem is smaller and younger than Elasticsearch's or Algolia's. |
| Extensibility | 2 | The filter/sort operator set is fixed and defined by Meilisearch itself with no user-defined functions at query time, though being MIT-licensed and open-source means the community can and does contribute new operators upstream via pull requests. |
| Transport Compatibility | 3 | `filter`, `sort`, and pagination fields are submitted in the JSON body of the recommended POST search route (a GET route also exists but is documented as discouraged), fitting well as structured request parameters rather than a single bare URL query string. |
| Standardization | 2 | Open-source (MIT-licensed) but governed entirely by the single Meilisearch project/company with no independent, vendor-neutral specification body for the query syntax. |
| Security | 4 | Filters are structured field/operator/value clauses rather than raw string concatenation, and attributes must be explicitly allow-listed in `filterableAttributes` before they can be filtered on, limiting the surface for filter-based data enumeration. |
| Performance | 3 | The docs explicitly warn that combining `rankingScoreThreshold` with `page`/`hitsPerPage` "may reduce performance because Meilisearch must score all matching documents," and cap total results at 1000 hits by default (configurable via a `pagination.maxTotalHits` index setting), showing documented, real performance trade-offs. |
| Orthogonality | 3 | Filter, sort, and pagination are cleanly separated into independent request parameters that compose predictably, though `page`/`hitsPerPage` and `offset`/`limit` are two parallel, mutually-exclusive pagination mechanisms with documented precedence rules that must not be mixed. |

**Overall score (avg, informational only): 3.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.1**

## Summary

Meilisearch exposes filter, sort, and pagination as independent, well-documented parameters of its search API — a SQL-like `filter` expression language, a `sort` array of attribute:direction pairs, and dual offset/limit or page/hitsPerPage pagination mechanisms. All attributes used for filtering or sorting must be explicitly declared in index settings, trading some flexibility for fast, pre-indexed filtering and sorting, similar in spirit to Elasticsearch's separation of query concerns.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```json
POST /indexes/products/search
{
  "filter": "category = \"electronics\" AND price > 100",
  "sort": ["price:desc"],
  "page": 2,
  "hitsPerPage": 10
}
```

Meilisearch natively supports all three ingredients — filter, sort, and page-based pagination — directly as documented, first-class search-request parameters, provided the `category`/`price` attributes are declared in filterableAttributes and `price` is declared in sortableAttributes.

## Sources

- Meilisearch. (n.d.). [*Search with POST*](https://www.meilisearch.com/docs/reference/api/search).
