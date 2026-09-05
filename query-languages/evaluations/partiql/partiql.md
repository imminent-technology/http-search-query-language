# PartiQL

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [PartiQL Query Basics (DQL Overview)](https://partiql.org/dql/overview.html)
- **Media type**: None known — PartiQL statements are submitted as a plain string field within a host service's own JSON API request (e.g., DynamoDB's `ExecuteStatement` API `Statement` parameter), not as a dedicated, independently registered media type.
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | PartiQL layers a full SQL SELECT-FROM-WHERE-GROUP BY-HAVING-ORDER BY-LIMIT/OFFSET pipeline (with INNER/LEFT/RIGHT/FULL/CROSS JOIN and UNION/INTERSECT/EXCEPT plus OUTER variants) on top of nested-data extensions unique to it — implicit UNNEST via FROM-clause path expressions, multistep paths (`e.projects[0].name`), SELECT VALUE for arbitrary (non-tuple) results, GROUP BY...GROUP AS for accessing whole groups, and PIVOT/UNPIVOT for converting between tuples and collections. |
| Simplicity | 4 | PartiQL is explicitly backwards-compatible with SQL-92, so any SQL query is already a valid PartiQL query and reads identically, but its semi-structured extensions (MISSING vs. NULL, tuple/bag/array literals, GROUP AS, PIVOT/UNPIVOT) introduce real additional concepts a pure-SQL user must learn. |
| Flexibility | 5 | The language is explicitly designed to be data-source and data-format independent — the same query runs unmodified over relational tables, JSON, Amazon Ion, Parquet, or CSV data, and over data with or without a fixed schema, per its own "Data Storage Independence" and "First Class Nested Data" design goals. |
| Community and Ecosystem | 4 | PartiQL is maintained by Amazon and used as the query language across multiple AWS services (DynamoDB, Redshift Spectrum/SUPER columns, QLDB, and AWS IoT TwinMaker's knowledge graph), is open-sourced under Apache 2.0 with active Kotlin and Rust reference implementations on GitHub, though its community remains narrower than a general-purpose, vendor-neutral language like SQL or GraphQL. |
| Extensibility | 4 | The project runs a public, GitHub-based RFC process for language extensions (e.g., RFC-0007 for bag operators), and its 2-tiered specification (a small "PartiQL Core" plus SQL compatibility as syntactic sugar) is explicitly designed so new data-format mappings and features can be layered on without altering the core semantics. |
| Transport Compatibility | 2 | PartiQL has no URL query-string or HTTP-native transport convention of its own; it is instead embedded as a plain string parameter inside each host service's own API (e.g., DynamoDB's `ExecuteStatement`/`BatchExecuteStatement` JSON API calls, or Redshift/QLDB's driver-based wire protocols), similar to how SQL itself is typically transported via JDBC/ODBC rather than as a URL parameter. |
| Standardization | 2 | PartiQL has a formal, versioned, publicly published specification and grammar plus a conformance test suite, but it is a single-organization (AWS-led) open-source specification with no ANSI/ISO/IETF/W3C standards-body ratification — a semi-formal tier comparable to JMESPath's own ABNF-grammar-plus-test-suite specification in this dataset. |
| Security | 3 | Host APIs that implement PartiQL (e.g., DynamoDB's `ExecuteStatement`) support parameterized statements with `?` placeholders specifically to avoid string-concatenation injection, but this protection is a host-service API convention rather than a language-level guarantee, leaving PartiQL at the same string-based-injection-risk tier as SQL itself unless the caller opts into parameterization. |
| Performance | 3 | PartiQL itself defines no indexing or query-planning semantics, deferring entirely to the host engine (e.g., Redshift Spectrum's columnar SUPER type optimizations, DynamoDB's key-condition-based execution), the same execution-is-implementation-defined position as most other SQL-family languages in this dataset. |
| Orthogonality | 4 | The specification explicitly treats each clause (FROM, WHERE, GROUP BY, SELECT) as a function that inputs and outputs collections of binding tuples uniformly, and path navigation (`.attr`, `[index]`) composes predictably across tuples, arrays, and bags regardless of nesting depth or data heterogeneity. |

**Overall score (avg, informational only): 3.6**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.8**

## Summary

PartiQL is an open-source, SQL-compatible query language maintained by Amazon that extends SQL-92 with first-class support for nested and semi-structured data (JSON, Ion, Parquet) and schemaless datasets, while remaining backwards-compatible with plain SQL queries. It is used as the query language across several AWS services (DynamoDB, Redshift Spectrum/SUPER, QLDB), with reference implementations in Kotlin and Rust and a public RFC-driven extension process. Its design scores strongly on expressiveness, flexibility, and orthogonality — unifying relational and nested-data querying under one grammar — but it lacks any URL/HTTP-native transport convention (queries are embedded as string parameters within each host service's own API) and, despite a rigorous open specification, has no formal standards-body ratification.

## Sources

- PartiQL. (n.d.). [*PartiQL — An expressive, SQL-compatible query language giving access to relational, semi-structured, and nested data*](https://partiql.org/). Maintained by Amazon; developed by open-source contributors.
- PartiQL. (n.d.). [*PartiQL Tutorial*](https://partiql.org/tutorial.html).
- PartiQL. (n.d.). [*PartiQL Query Basics (DQL Overview)*](https://partiql.org/dql/overview.html).
