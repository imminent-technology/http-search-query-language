# SQL

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [SQL — Wikipedia](https://en.wikipedia.org/wiki/SQL)
- **Media type**: `application/sql` — IANA-registered, RFC 6922.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | Natively supports filtering, sorting, aggregation, joins, subqueries, window functions, and recursive queries (CTEs) — the reference point most other query languages are compared against. |
| Simplicity | 3 | Basic SELECT/WHERE queries are easy to read, but the full language (three-valued NULL logic, procedural extensions, vendor-specific dialects) has a real learning curve, and Wikipedia's own criticism section highlights orthogonality/completeness gaps that surprise newcomers. |
| Flexibility | 2 | Built around a fixed relational schema; adding or changing fields requires DDL migrations, and while JSON support was added in SQL:2016, dynamic/schema-less data is not a natural fit. |
| Community and Ecosystem | 5 | The most widely deployed query language in the world, with decades of tooling, ORMs, tutorials, and near-universal database support. |
| Extensibility | 4 | Supports user-defined functions and stored procedures (SQL/PSM, PL/pgSQL, T-SQL, PL/Java via SQL/JRT), though the core grammar itself is fixed by the standard. |
| Transport Compatibility | 2 | Designed around persistent connections and wire protocols (JDBC/ODBC) rather than URL embedding; ad-hoc queries are normally sent as request bodies through a REST wrapper, not as URL query strings. |
| Standardization | 5 | Formally standardized as ISO/IEC 9075 since 1986/1987 and maintained by ISO/IEC JTC1/SC32, with revisions through SQL:2023 — though Wikipedia notes vendors rarely implement the full standard. |
| Security | 2 | Historically built via string concatenation, making SQL injection one of the most common web vulnerability classes (OWASP Top 10); parameterized queries mitigate this but are not the language's default mode of use. |
| Performance | 5 | Declarative by design specifically so implementations can optimize execution via query planners and indexes — decades of optimization research back this up (see PostgreSQL's EXPLAIN/planner docs). |
| Orthogonality | 3 | Core CRUD operations compose reasonably well, but Wikipedia's "Orthogonality and completeness" criticism notes historical gaps (no primary keys or subqueries pre-1992) and bolted-on extensions like SQL/XML and SQL/JSON that don't integrate cleanly with the core model. |

**Overall score (avg, informational only): 3.6**
**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.3**

## Summary

SQL is the most expressive, standardized, and performant of the widely-used query languages, backed by an unmatched ecosystem, but its rigid schema, weak default injection resistance, and poor fit for URL-based HTTP transport are the tradeoffs of a language designed in the 1970s for persistent database connections rather than stateless web APIs.

## Sources

- Wikipedia. (2026, August 23). [*SQL*](https://en.wikipedia.org/wiki/SQL).
- International Organization for Standardization (ISO). (2023, June). [*ISO/IEC 9075-1:2023 — Information technology — Database languages — SQL — Part 1: Framework (SQL/Framework)*](https://www.iso.org/standard/76583.html).
- The PostgreSQL Global Development Group. (n.d.). [*Part II. The SQL Language — PostgreSQL Documentation*](https://www.postgresql.org/docs/current/sql.html).
