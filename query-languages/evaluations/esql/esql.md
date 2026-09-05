# ESQL

[↑ Full comparison table](../summary.md)

- Category: Search/full-text
- Official docs: [Query string query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html)
- Media type: None known — Elasticsearch's Query DSL/ES|QL requests use the generic `application/json` content type.
- Evaluated: 2026-09-04

> Note: `list.csv` labels this entry "ESQL" but links to Elasticsearch's `query_string` query syntax (a Lucene-derived query mini-language), not Elastic's separate, newer ES|QL piped query language. This evaluation covers the syntax actually linked.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports field-scoped terms, wildcards, regular expressions, fuzzy and proximity matching, inclusive/exclusive ranges, boosting, boolean operators, grouping, and multi-field search with configurable matching strategies. |
| Simplicity | 3 | Simple term/phrase queries are easy to write, but the parser is strict and "returns an error if the query string includes any invalid syntax" per Elastic's own docs, which explicitly warn against using it for user-facing search boxes. |
| Flexibility | 4 | Runs over Elasticsearch's schema-free, dynamically-mapped JSON documents, letting queries target arbitrary or wildcard-matched fields without a rigid predefined schema. |
| Community and Ecosystem | 5 | Elasticsearch is one of the most widely deployed search/observability engines, with official clients in Java, C#, PHP, Python and Ruby and a large surrounding Elastic Stack ecosystem. |
| Extensibility | 3 | Analyzers, synonym filters, and custom scoring can be configured, but the query_string mini-language's own grammar is fixed by the Elasticsearch version; it is only one of several related query types (match, simple_query_string) rather than an open grammar. |
| Transport Compatibility | 4 | Submitted over Elasticsearch's HTTP REST API, either as the `q` request parameter on the search endpoint or embedded in a JSON request body — HTTP-native by design. |
| Standardization | 1 | A proprietary Elastic-defined syntax (internally reusing Apache Lucene's query parser) with no independent standards body governing it. |
| Security | 2 | Because the strict parser throws on invalid syntax, un-sanitized user input concatenated into a query_string is a documented anti-pattern; Elastic explicitly recommends match/simple_query_string instead for exposing to end users, underscoring the injection/error-oracle risk of raw usage. |
| Performance | 5 | Built on Apache Lucene with distributed sharding and replication across cluster nodes, purpose-built for low-latency full-text search at scale. |
| Orthogonality | 3 | Boolean, range, boosting, and field-search constructs compose reasonably, but the reserved-character escaping rules, JSON double-escaping requirement, and overlap with sibling query types (match, simple_query_string, multi_match) add inconsistency. |

**Overall score (avg, informational only): 3.4**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

Elasticsearch's query_string syntax (referenced in list.csv as "ESQL"/Elasticsearch Query Syntax) offers Lucene-derived expressiveness over schema-free JSON documents via a native HTTP REST API, backed by one of the largest search ecosystems, but its strict, error-throwing parser is explicitly discouraged by Elastic for direct end-user input and remains a single-vendor, non-standardized dialect.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```json
{
  "query": {
    "query_string": {
      "query": "category:electronics AND price:>100"
    }
  },
  "sort": [{ "price": "desc" }],
  "from": 10,
  "size": 10
}
```

`sort` and `from`/`size` are top-level Elasticsearch request-body fields, not part of the `query_string` mini-language itself — that syntax only expresses the filter predicate.

## Sources

- Elastic NV. (n.d.). [*Query string query*](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html).
- Wikipedia. (2026, August 10). [*Elasticsearch*](https://en.wikipedia.org/wiki/Elasticsearch).
