# SQL++

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [SQL++](https://www.couchbase.com/sqlplusplus/)
- **Media type**: None known — Couchbase's Query REST API accepts SQL++/N1QL as a `"statement"` field inside a generic `application/json` body.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Extends SQL with native support for nested/heterogeneous JSON, arrays and joins over both structured and semi-structured data, aiming to be a superset of SQL's expressiveness for JSON. |
| Simplicity | 3 | Deliberately reuses familiar SQL syntax and keywords, but added constructs for nested arrays/objects and flexible schemas increase complexity versus plain SQL. |
| Flexibility | 5 | Purpose-built to query JSON data with flexible, schema-less/nested structures while retaining a declarative SQL-like syntax — its core selling point. |
| Community and Ecosystem | 2 | Primarily driven by a single vendor (Couchbase) with adoption by AsterixDB; a smaller ecosystem/community than mainstream SQL or NoSQL query languages. |
| Extensibility | 3 | Supports user-defined functions in Couchbase's implementation, but as a younger, vendor-led specification its extension model is less mature than long-established languages. |
| Transport Compatibility | 3 | Accessible over Couchbase's HTTP-based Query/Analytics REST APIs as a request body, but not designed for compact embedding in a URL query string. |
| Standardization | 2 | Developed as an open specification with academic origins (co-invented by Don Chamberlin) and adopted beyond Couchbase (e.g. AsterixDB), but lacks formal standards-body backing like ISO SQL. |
| Security | 2 | As a SQL-family language it is commonly built via string concatenation/query text in application code, sharing SQL's classic injection exposure unless parameterization is used. |
| Performance | 3 | Designed to let query engines (Couchbase Analytics, AsterixDB) apply indexing and optimization to JSON data, though real-world performance depends heavily on the specific engine implementation. |
| Orthogonality | 3 | Extends SQL's composable clause structure to nested JSON, but the added array/object navigation constructs are layered on top of SQL rather than fully unified with it. |

**Overall score (avg, informational only): 3.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.3**

## Summary

SQL++ extends familiar SQL syntax to natively query nested and heterogeneous JSON data, giving it strong flexibility for document-style workloads, but it remains a smaller, largely Couchbase-driven specification without ISO-style standardization or SQL's mature security/optimization track record.

## Sources

- Couchbase, Inc. (n.d.). [*SQL++*](https://www.couchbase.com/sqlplusplus/).
