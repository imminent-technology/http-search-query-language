# Elasticsearch/OpenSearch Query DSL

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) (Elastic) · [Query DSL](https://docs.opensearch.org/latest/query-dsl/) (OpenSearch)
- **Media type**: None known — both engines accept Query DSL as a JSON `application/json` request body on `POST _search` (or `GET _search` with a body), not a dedicated registered media type.
- **Evaluated**: 2026-09-07

> Note: distinct from the [ESQL](../esql/esql.md) entry, which covers Elasticsearch's separate `query_string` mini-language (a Lucene-derived text syntax embedded as a plain string). This entry covers the full structured, JSON-based Query DSL (`bool`/`term`/`range`/etc.) shared by Elasticsearch and its OpenSearch fork.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | A JSON AST of leaf queries (match, term, range, multi_match, geo, wildcard, fuzzy) and compound queries (bool with must/should/must_not/filter, dis_max, function_score) that combines search, structured filtering, and a full aggregations framework (metric/bucket/pipeline) in a single request — among the richest query surfaces in this catalog. |
| Simplicity | 2 | Individual leaf clauses are simple, but the JSON AST requires understanding query-vs-filter context and can nest deeply for even moderately complex boolean conditions, with no flat/inline shorthand for common cases. |
| Flexibility | 4 | Built for schema-flexible, dynamically-mapped JSON documents rather than a rigid predefined schema, and the fact that OpenSearch's near-identical fork works interchangeably with Elasticsearch's Query DSL demonstrates real portability across two independent engines. |
| Community and Ecosystem | 5 | Elasticsearch is one of the most widely adopted search/analytics engines with a massive community and Kibana/Logstash/Beats ecosystem, and its OpenSearch fork adds an independently governed, AWS-backed alternative with its own large user base. |
| Extensibility | 4 | Supports custom scoring and filtering via script/script_score queries (Painless scripting in Elasticsearch), custom analyzers/tokenizers, and a plugin architecture that can register entirely new query types. |
| Transport Compatibility | 3 | Queries are submitted as a JSON body on the `_search` endpoint rather than a bare URL query string; a separate, much simpler Lucene query-string syntax exists for the `q=` URL parameter, but the full Query DSL itself requires a structured request body. |
| Standardization | 2 | Elasticsearch is Elastic-licensed (source-available, not OSI-approved open source), but its OpenSearch fork is Apache-2.0 and governed by the OpenSearch Software Foundation under the Linux Foundation — a genuine multi-stakeholder governance model, even though no formally ratified independent specification exists. |
| Security | 3 | Structured JSON avoids raw string-based query injection, and query/filter context is a documented, deliberate security/performance boundary, but script-based queries (script_score, script) introduce a real code-execution surface that both projects explicitly let administrators disable via an `allow_expensive_queries`-style setting. |
| Performance | 4 | Filter context is explicitly documented as faster than query context (no scoring, automatic caching, lower CPU), and both projects maintain an explicit, documented list of "expensive" query types (regexp, wildcard, fuzzy, scripts, joins) that administrators can globally disable. |
| Orthogonality | 4 | Leaf and compound query clauses compose recursively and uniformly — compound queries wrap other leaf or compound clauses in a consistent tree — and aggregations similarly nest into pipelines, though the query-vs-filter context distinction is a meaningful behavioral wrinkle to track. |

**Overall score (avg, informational only): 3.6**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

Elasticsearch's Query DSL (and its near-identical OpenSearch fork) is a JSON-based abstract-syntax-tree query language combining full-text search, structured filtering, and a rich aggregations framework in a single request. It is one of the most expressive and orthogonal languages surveyed, trading a lightweight URL-based transport for a deeply composable JSON request body, with OpenSearch's Linux Foundation governance giving the combined ecosystem more independent standing than most single-vendor search languages.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```json
GET /products/_search
{
  "query": {
    "bool": {
      "filter": [
        { "term": { "category": "electronics" } },
        { "range": { "price": { "gt": 100 } } }
      ]
    }
  },
  "sort": [{ "price": "desc" }],
  "from": 10,
  "size": 10
}
```

Query DSL natively supports all three ingredients directly: structured filtering via the bool/filter clause, sorting via the top-level `sort` array, and page 2 of 10 via `from`/`size` offset-based pagination.

## Sources

- Elastic. (n.d.). [*Query DSL*](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html).
- OpenSearch Project (Linux Foundation). (n.d.). [*Query DSL*](https://docs.opensearch.org/latest/query-dsl/).
