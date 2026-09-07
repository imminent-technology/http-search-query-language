# GitHub Search Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [Understanding the search syntax](https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax)
- **Media type**: None known — GitHub's REST API accepts search queries as a `q` URL query parameter on `GET` endpoints (e.g. `GET /search/repositories?q=...&sort=...&order=...`), not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Combines free-text keywords with `qualifier:value` filters, numeric/date comparators (>, >=, <, <=, ranges with `..`), exclusion via `-qualifier` or `NOT`, and endpoint-level `sort`/`order` parameters with several sortable fields per resource (stars, forks, created, updated, comments, reactions), though queries are capped at 256 characters and at most five AND/OR/NOT operators. |
| Simplicity | 3 | The `qualifier:value` shape is intuitive and works identically in the web search bar and the REST API's `q` parameter, but the available qualifiers and sortable fields differ per search target (repositories, issues, code, commits, users, topics), so the full syntax surface is not uniform across endpoints. |
| Flexibility | 2 | Qualifiers are a fixed, closed set defined per search target by GitHub's own platform (repository/issue/code/user/commit/topic metadata), so the language cannot be pointed at arbitrary or user-defined data outside GitHub's object model. |
| Community and Ecosystem | 4 | GitHub is the world's largest code-hosting platform, and its search syntax is used identically by millions of developers daily through the web UI, extensively documented, though it remains a single-vendor feature rather than an independently implemented language. |
| Extensibility | 1 | The set of qualifiers, operators, and sortable fields is fixed and defined entirely by GitHub, with no mechanism for users or third parties to add new qualifiers or functions. |
| Transport Compatibility | 5 | Passed as a `q` URL query parameter on REST search endpoints (e.g. `GET /search/repositories?q=cats+language:go`), and the identical query string also works directly in github.com's own web search URL — arguably a best-in-class fit for URL-based transport. |
| Standardization | 1 | A closed, single-vendor (GitHub/Microsoft) proprietary search syntax with no published formal grammar specification or independent governance body. |
| Security | 4 | Structured qualifier:value syntax with quoting for phrases avoids raw string concatenation, and GitHub's docs explicitly describe access-control filtering (results are silently restricted to repositories the requester can access) rather than exposing an injectable query surface. |
| Performance | 3 | GitHub's own REST API docs document explicit performance ceilings — up to 1,000 total results per search, a 4,000-repository scan limit for repository search, request timeouts that can return `incomplete_results: true`, and strict rate limits (30 requests/minute authenticated, 10/minute for code search) — real, documented constraints on a hosted search service. |
| Orthogonality | 3 | The qualifier:value/comparator/exclusion model is applied consistently, but available qualifiers and the `NOT` keyword behave differently across search targets and value types (`NOT` only works for string keywords, not numerals or dates), so the same syntax does not compose identically everywhere. |

**Overall score (avg, informational only): 3.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.1**

## Summary

GitHub's search syntax is a closed, single-vendor `qualifier:value` query language for searching repositories, issues, code, commits, users, and topics, combining free-text keywords, numeric/date comparators, range and exclusion syntax, and endpoint-level sort/order parameters. Its qualifiers are fixed and non-extensible, but it is used identically across the github.com web UI and REST/GraphQL APIs, giving it exceptional transport compatibility and adoption at massive scale.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
GET /search/repositories?q=topic:electronics+stars:>100&sort=stars&order=desc&per_page=10&page=2
```

Adapted to GitHub's repository search domain (no built-in "product"/"price" concept), approximating category with `topic:` and price with `stars:>100`. Unlike most other proprietary search syntaxes surveyed, GitHub natively supports all three ingredients: filtering via qualifiers, sorting via the `sort`/`order` API parameters (not part of the `q` string itself), and true page-number pagination via `page`/`per_page`.

## Sources

- GitHub. (n.d.). [*Understanding the search syntax*](https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax).
- GitHub. (n.d.). [*REST API endpoints for search*](https://docs.github.com/en/rest/search/search).
