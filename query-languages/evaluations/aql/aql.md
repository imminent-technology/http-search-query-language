# AQL

[↑ Full comparison table](../summary.md)

- **Category**: Document/NoSQL
- **Official docs**: [ArangoDB Query Language](https://www.arangodb.com/docs/stable/aql/)
- **Media type**: None known — ArangoDB's HTTP API wraps AQL queries in a generic `application/json` request body; no dedicated media type exists.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | FOR/FILTER/COLLECT/RETURN syntax supports full CRUD over documents and graphs, geospatial queries, and aggregation, combining document, graph and key-value access within a single query. |
| Simplicity | 3 | Declarative and SQL-like in spirit, but its FOR-based syntax and multi-model concepts (documents, graphs, joins) require learning a distinct mental model compared to plain SQL. |
| Flexibility | 5 | A native, JSON-oriented multi-model query language spanning documents, graphs and key-value data in one unified language, ArangoDB's core differentiator. |
| Community and Ecosystem | 2 | Driven primarily by a single vendor (ArangoDB GmbH) with a smaller community than mainstream databases; the 2023 shift from Apache 2.0 to a Business Source License may further limit adoption. |
| Extensibility | 3 | Supports user-defined functions via the Foxx JavaScript framework and search/vector extensions (ArangoSearch), though its extension ecosystem is narrower than major open standards. |
| Transport Compatibility | 2 | Executed through ArangoDB's HTTP REST API as request bodies or via language drivers, not designed for compact embedding directly in a URL query string. |
| Standardization | 1 | A single-vendor proprietary language with no independent specification or alternate implementations. |
| Security | 3 | Idiomatic use relies on bind parameters via drivers to avoid injection, a risk profile similar to other declarative query languages. |
| Performance | 3 | Implemented in C++ with self-managed memory for predictable performance and native clustering support, though real-world performance depends heavily on the specific ArangoDB version and deployment. |
| Orthogonality | 3 | FOR/FILTER/COLLECT/RETURN compose reasonably well across document and graph models, but mixing multiple data models in a single query adds complexity relative to a single-model language. |

**Overall score (avg, informational only): 2.9**

## Summary

AQL is ArangoDB's SQL-like, JSON-oriented multi-model query language, offering strong flexibility for combining document, graph and key-value access in one query, but it remains a single-vendor proprietary language with a smaller ecosystem and no HTTP/URL-native transport model.

## Sources

- Wikipedia. (2026, August 16). [*ArangoDB*](https://en.wikipedia.org/wiki/ArangoDB).
