# Cypher

[↑ Full comparison table](../summary.md)

- **Category**: Graph
- **Official docs**: [Neo4j Cypher Manual](https://neo4j.com/developer/cypher/)
- **Media type**: None known — openCypher/Neo4j statements travel over the Bolt protocol or are wrapped in generic `application/json` via Neo4j's HTTP query API; no dedicated Cypher media type.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | ASCII-art pattern matching over nodes and relationships supports filtering, aggregation, and full CRUD (MATCH/CREATE/MERGE/SET/DELETE), giving high expressiveness for graph traversal and pattern queries. |
| Simplicity | 4 | Explicitly designed to be visual and human-readable — patterns structurally mirror the graph shape being queried — and openCypher markets it as "easy-to-learn and human-readable" for developers, data scientists, and operators alike. |
| Flexibility | 4 | The underlying property graph model (labels + properties on nodes/relationships) is inherently schema-optional, letting labels and properties be added without a rigid predefined schema. |
| Community and Ecosystem | 4 | The dominant graph-database query language via Neo4j, extended through openCypher to other implementations (e.g. AgensGraph), with a sizable community though smaller than SQL's or GraphQL's. |
| Extensibility | 3 | Supports user-defined procedures and functions in practice (e.g. Neo4j's APOC library), but this is implementation-specific tooling rather than a feature defined by the openCypher specification itself. |
| Transport Compatibility | 2 | Typically sent via the binary Bolt protocol or as a JSON request body to a transactional HTTP endpoint, with the query string as one field — not designed for URL query-string embedding. |
| Standardization | 4 | Originated as a single-vendor (Neo4j) language but was opened via the openCypher project in 2015 and directly fed into ISO/IEC 39075:2024 (GQL), a formal ISO standard for graph query languages — a strong and still-improving standardization trajectory. |
| Security | 3 | Supports parameterized queries (e.g. `$yearParameter`) that avoid string concatenation, reducing injection risk when used properly, but string-built Cypher remains possible and vulnerable in the same way as SQL. |
| Performance | 4 | Graph-native storage with index-backed pattern matching is designed for efficient multi-hop traversal — explicitly cited as a core motivation behind the GQL standardization effort for reachability and shortest-path queries. |
| Orthogonality | 4 | Clauses (MATCH/WHERE/RETURN/CREATE/DELETE/SET/MERGE) are composable and follow a consistent pattern-based syntax across both read and write use cases. |

**Overall score (avg, informational only): 3.7**
**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

Cypher combines high expressiveness for graph pattern-matching with unusually strong readability and a clear path toward formal standardization via GQL, but like SQL it is built around persistent driver connections (Bolt) rather than lightweight HTTP transport.

## Sources

- Neo4j, Inc. (n.d.). [*Introduction — Cypher Manual*](https://neo4j.com/developer/cypher/).
- Neo4j, Inc. (n.d.). [*openCypher*](https://opencypher.org/).
- Wikipedia. (2026, April 23). [*Cypher (query language)*](https://en.wikipedia.org/wiki/Cypher_(query_language)).
