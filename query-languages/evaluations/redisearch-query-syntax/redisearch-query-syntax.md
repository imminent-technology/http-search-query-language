# RediSearch Query Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [FT.SEARCH](https://redis.io/docs/latest/commands/ft.search/)
- **Media type**: None known — issued as arguments to the `FT.SEARCH` command over Redis's RESP protocol, not an HTTP/JSON media type.
- **Evaluated**: 2026-09-07
- **Client Libraries**: Python: mature · JavaScript: mature · Java: mature · Go: mature · Rust: partial · .NET: mature
- **Support Model**: single-vendor-commercial

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | The query string supports field-scoped full-text terms (`@field:value`) with phrase/prefix/fuzzy matching, numeric ranges (`[min max]`, `-inf`/`+inf`), TAG filters (`{value}`), geospatial and geoshape operators (WITHIN/CONTAINS/INTERSECTS/DISJOINT), vector KNN search, and boolean AND/OR/NOT, combined with FT.SEARCH-level SORTBY/LIMIT/RETURN — a very rich combined query-and-command surface. |
| Simplicity | 2 | Field:value and operator shapes are compact, but the full syntax spans both the query string and separate FT.SEARCH command flags, and numeric/geospatial syntax differs across documented query dialect versions (1 through 4), adding real cognitive overhead. |
| Flexibility | 2 | A schema (TEXT/TAG/NUMERIC/GEO/VECTOR fields) must be declared upfront via FT.CREATE before any field can be queried, and fields must additionally be marked SORTABLE to be used with SORTBY, a genuine schema-first constraint. |
| Community and Ecosystem | 3 | Redis is one of the most widely deployed in-memory data stores, and its search capability (RediSearch/Redis Query Engine) ships built into modern Redis and Redis Stack with a large developer community, though full-text search is a narrower use case relative to Redis's core key-value usage. |
| Extensibility | 3 | Supports a documented Extensions mechanism for registering custom SCORER and EXPANDER (query-expansion) functions, a genuine plugin point for extending scoring and stemming behavior beyond the built-in set. |
| Transport Compatibility | 2 | Issued as arguments to a Redis command over the RESP protocol via `redis-cli` or a Redis client library, not natively an HTTP/URL-based transport, so it cannot be embedded directly in a web request URL the way most other languages surveyed can. |
| Standardization | 2 | Open-source and bundled into Redis (dual-licensed under RSALv2/SSPLv1 as of recent Redis versions) but governed by the single vendor Redis Ltd., with no independent, vendor-neutral specification body for the query syntax. |
| Security | 4 | The documented `PARAMS` mechanism lets queries reference named parameters (e.g. `$lon`, `$lat`) that are substituted server-side rather than built via unsafe string concatenation — a genuine, documented prepared-statement-like safety mechanism. |
| Performance | 4 | FT.SEARCH's complexity is explicitly documented as O(n), with detailed, documented sorting optimizations per dialect (Skip Sorter, Partial Range, Hybrid) and an explicit warning that using LIMIT without SORTBY produces non-deterministic paging. |
| Orthogonality | 3 | Field-scoped clauses (`@field:...`) compose consistently across TEXT/TAG/NUMERIC/GEO via implicit AND, explicit OR (`|`), and NOT (`-`), but behavior for the same feature (e.g. numeric range and geoshape operators) differs meaningfully across documented query dialect versions. |

**Overall score (avg, informational only): 2.9**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

RediSearch's FT.SEARCH query syntax combines a field-scoped full-text/numeric/tag/geo query string with command-level SORTBY/LIMIT/RETURN arguments, offering a genuinely rich, schema-first search capability built into Redis. It supports parameterized queries for safety and documents granular performance optimizations, but requires a Redis protocol client rather than a URL-based transport, and its syntax varies across query dialect versions.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
FT.SEARCH products-idx "@category:{electronics} @price:[(100 +inf]" SORTBY price DESC LIMIT 10 10
```

RediSearch natively supports all three ingredients as FT.SEARCH command arguments: a TAG filter for category and a NUMERIC range filter for price (both in the query string), SORTBY for descending order, and LIMIT 10 10 for page 2 of 10 (offset 10, count 10).

## Sources

- Redis. (n.d.). [*FT.SEARCH*](https://redis.io/docs/latest/commands/ft.search/).
- Redis. (n.d.). [*Querying data*](https://redis.io/docs/latest/develop/ai/search-and-query/query/).
