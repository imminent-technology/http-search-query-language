# HQL

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [Hibernate - Query Language](https://www.tutorialspoint.com/hibernate/hibernate_query_language.htm)
- **Media type**: Not applicable — HQL is parsed and translated to SQL inside the JVM by Hibernate; it is not transmitted over HTTP with its own media type.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports SELECT/WHERE/JOIN/GROUP BY/ORDER BY, aggregate functions, bulk UPDATE/DELETE/INSERT and named/positional parameters, closely mirroring SQL's expressiveness over entity objects. |
| Simplicity | 4 | Deliberately SQL-like syntax makes it easy to learn for anyone who knows SQL, though understanding entity/property mapping adds a layer of indirection. |
| Flexibility | 2 | Queries operate over statically mapped, annotated or XML-configured entity classes, making it a poor fit for schema-less or rapidly evolving data models. |
| Community and Ecosystem | 4 | Hibernate is the most widely used Java ORM (started 2001, now backed by Red Hat) with extensive documentation, books and tooling, though scoped to the Java ecosystem. |
| Extensibility | 3 | Allows registering custom SQL functions and dialects, but the core HQL grammar itself is fixed by the framework. |
| Transport Compatibility | 1 | HQL is only executed through the in-process Hibernate Session/Query API within a Java application; it has no notion of URL or HTTP transport. |
| Standardization | 3 | Not itself an independent formal standard, but it closely mirrors — and historically influenced — the standardized JPQL defined in the Jakarta Persistence specification. |
| Security | 4 | Named and positional parameters are the idiomatic way to build HQL queries, giving protection against injection comparable to parameterized SQL when used as intended. |
| Performance | 3 | Hibernate translates HQL into native SQL and applies caching/lazy loading, but the ORM abstraction can make manual query-plan tuning less direct than hand-written SQL. |
| Orthogonality | 3 | Clauses compose in a SQL-like way, but the object-relational impedance mismatch (collections, associations, lazy loading) introduces special-casing absent from plain SQL. |

**Overall score (avg, informational only): 3.1**
**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

HQL brings a deliberately SQL-like, database-portable query syntax to Hibernate's object-relational mapping layer, backed by one of the most widely used Java ORM frameworks, but it is usable only from within a Java application process and is tightly coupled to a static entity schema rather than dynamic data.

## Sources

- Tutorials Point. (n.d.). [*Hibernate - Query Language*](https://www.tutorialspoint.com/hibernate/hibernate_query_language.htm).
- Wikipedia. (2026, April 9). [*Hibernate (framework)*](https://en.wikipedia.org/wiki/Hibernate_(framework)).
