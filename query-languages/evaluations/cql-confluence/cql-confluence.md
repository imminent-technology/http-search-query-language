# CQL (Confluence)

[↑ Full comparison table](../summary.md)

> **Note:** Not to be confused with Cassandra's CQL (Cassandra Query Language), covered in the [CQL](../cql/cql.md) entry. Both languages share the name "CQL" but are unrelated — this entry covers Atlassian Confluence's content search language.

- **Category**: Search/full-text
- **Official docs**: [Advanced searching using CQL](https://developer.atlassian.com/cloud/confluence/advanced-searching-using-cql/)
- **Media type**: None known — Confluence's REST API accepts CQL as a `cql` URL query parameter on `GET` endpoints (e.g. `GET /wiki/rest/api/content/search?cql=...`), not a dedicated media type.
- **Evaluated**: 2026-09-07
- **Client Libraries**: Python: partial · JavaScript: partial · Java: partial · Go: partial · Rust: partial · .NET: partial
- **Support Model**: single-vendor-commercial

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | Provides field/operator/value clauses across a fixed set of content fields (title, text, space, label, creator, contributor, ancestor, type, and more), AND/OR/NOT boolean combination, and ORDER BY, plus functions like currentUser() and startOfWeek(), but has no SELECT projection, no joins, and cannot compare two fields directly. |
| Simplicity | 3 | Individual clauses (`space = DEV AND label = "needs-review"`) are easy to read, but the docs explicitly warn that CQL evaluates strictly left to right without SQL-style operator precedence unless parentheses are used, a common source of unexpected results. |
| Flexibility | 2 | CQL's field set is fixed to Confluence's built-in content model (pages, blog posts, attachments, comments) rather than to a user-definable schema, so unlike JQL's per-project custom fields there is no way to add new queryable fields without a REST API/plugin extension. |
| Community and Ecosystem | 3 | Confluence is a widely deployed enterprise wiki, and CQL is documented with a dedicated reference and used throughout Confluence's REST API and macro ecosystem, though it has a narrower dedicated community than Jira's sibling JQL. |
| Extensibility | 3 | The query-writer cannot add fields or functions inline, but Atlassian's developer platform provides a CQL field module and CQL function module for Confluence apps, letting installed plugins register new searchable fields and functions. |
| Transport Compatibility | 4 | Passed as a `cql` URL query parameter to Confluence's Content REST API (`GET /wiki/rest/api/content/search?cql=...`), fitting naturally into a URL query string. |
| Standardization | 1 | A closed, single-vendor (Atlassian) proprietary query language embedded in the Confluence SaaS product, with no published formal grammar specification or independent governance body. |
| Security | 3 | Structured field/operator/value clauses avoid raw string concatenation, but the CONTAINS (~) text operator runs against Confluence's underlying search index with no documented query-complexity ceiling comparable to parameterized statements. |
| Performance | 3 | Runs against Confluence's indexed content store, but the docs note that certain REST API expansions (e.g. `expand=body.storage.value`) can cap the effective result count at 50 regardless of the requested `limit`, a documented performance-driven constraint. |
| Orthogonality | 3 | The field/operator/keyword model is applied consistently, but the reference documentation shows each field supports only a specific subset of the ten possible operators (e.g. Label only supports =, !=, IN, and NOT IN), so the same operator does not behave uniformly across all fields. |

**Overall score (avg, informational only): 2.8**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

Confluence's CQL (Confluence Query Language) is Atlassian's SQL-like field/operator/value query language for searching wiki content — pages, blog posts, attachments, and comments — via AND/OR/NOT boolean combination and ORDER BY, but explicitly without a SELECT statement or joins. It is a closed, single-vendor language scoped to Confluence's fixed content model, though its field and function set can be extended by installed Confluence apps.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page (adapted to Confluence's wiki-content model, which has no numeric price field).

```cql
space = "PRODUCTS" AND label = "electronics" order by created desc
```

Approximated using a label instead of a numeric "price" comparison, since Confluence's content model has no such field. CQL itself has no LIMIT/OFFSET pagination syntax; pagination (page 2 of 10) is controlled by the surrounding REST API's `start`/`limit` query parameters, not by the CQL query string itself.

## Sources

- Atlassian. (n.d.). [*Advanced searching using CQL*](https://developer.atlassian.com/cloud/confluence/advanced-searching-using-cql/).
