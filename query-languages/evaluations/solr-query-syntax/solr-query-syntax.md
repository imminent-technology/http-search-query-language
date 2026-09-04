# Solr Query Syntax

[↑ Full comparison table](../summary.md)

- Category: Search/full-text
- Official docs: [The Standard Query Parser](https://solr.apache.org/guide/6_6/the-standard-query-parser.html)
- Media type: None known — Solr accepts query strings as URL parameters or within the JSON Request API's generic `application/json`.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Beyond Lucene's base term/boolean/range/proximity/boosting syntax, Solr adds constant-score queries (^=), function-query hooks, nested query-parser clauses, and a cacheable filter(...) syntax. |
| Simplicity | 3 | Basic field:value and boolean queries are intuitive, but escaping the long list of reserved characters and understanding the differences from the plain Lucene parser add real complexity. |
| Flexibility | 3 | Query terms are scoped to fields defined in the Solr Schema; while dynamic fields and NoSQL-style features exist, the parser fundamentally expects indexed/analyzed fields rather than arbitrary schema-less data. |
| Community and Ecosystem | 4 | A top-level Apache project since 2007 with two decades of releases, client libraries in most major languages, and adoption inside Hadoop distributions and enterprise CMS/search products. |
| Extensibility | 3 | Supports pluggable query parsers (DisMax, eDisMax, function queries) and a plugin architecture, though the standard query parser's own grammar is fixed by the Solr version. |
| Transport Compatibility | 5 | Queries are submitted as the `q` parameter of a REST-like HTTP GET/POST request (e.g. `?q=id:SP2514N`), making the syntax natively URL-embeddable. |
| Standardization | 1 | An Apache Solr/Lucene-specific syntax with no independent standards body; the guide itself documents version-specific differences from the plain Lucene query parser. |
| Security | 2 | Query strings are commonly built by concatenating user input into the `q` parameter; without escaping the documented reserved characters, this is exposed to injection-style manipulation of query logic. |
| Performance | 5 | Built directly on the Apache Lucene inverted-index engine, with SolrCloud enabling distributed, horizontally-scalable search across shards and replicas. |
| Orthogonality | 3 | Core Boolean/field/range operators compose consistently, but Solr-specific extensions over the base Lucene parser (open-ended ranges, pure-negative queries, function-query casts) are layered on rather than unified with the base grammar. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

Solr's standard query parser extends Apache Lucene's HTTP-native, URL-embeddable query syntax with additional constant-scoring, function-query, and caching features, backed by a mature, widely-deployed enterprise search project — but it remains a Solr/Lucene-specific syntax with no formal standardization and the same string-based injection exposure as its parent Lucene parser.

## Sources

- The Apache Software Foundation. (2017, June 9). [*The Standard Query Parser*](https://solr.apache.org/guide/6_6/the-standard-query-parser.html).
- Wikipedia. (2026, March 27). [*Apache Solr*](https://en.wikipedia.org/wiki/Apache_Solr).
