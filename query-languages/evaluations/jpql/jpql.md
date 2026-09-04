# JPQL

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [Chapter 34: The Java Persistence Query Language](https://docs.oracle.com/javaee/6/tutorial/doc/bnbtg.html)
- **Media type**: Not applicable — like HQL, JPQL is used internally by the JPA provider and is not transmitted over HTTP with a dedicated media type.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | SQL-like SELECT/UPDATE/DELETE queries with joins, subqueries, aggregate functions, GROUP BY/HAVING, and case/functional expressions over entities. |
| Simplicity | 4 | Intentionally close to SQL syntax, easy to learn for Java/SQL developers, though entity path expressions add a layer over plain table/column SQL. |
| Flexibility | 2 | Queries operate over a fixed, annotated object-relational entity schema, making it a poor fit for dynamic or schema-less data. |
| Community and Ecosystem | 4 | Formally part of the widely-adopted Jakarta Persistence (formerly JPA) specification, implemented by Hibernate, EclipseLink, OpenJPA, DataNucleus and others, with broad documentation and tooling. |
| Extensibility | 3 | Supports generic/native database functions and, since JPA 2.1, stored procedures, but the core grammar is fixed by the specification. |
| Transport Compatibility | 1 | Executed only through the Java EntityManager API inside an application process; has no notion of URL or HTTP transport. |
| Standardization | 5 | Defined by the vendor-neutral Jakarta Persistence specification (formerly JSR 220/317/338), implemented independently by Hibernate, EclipseLink, OpenJPA and DataNucleus. |
| Security | 4 | Named and positional parameter binding is the idiomatic way to build JPQL queries, giving strong protection against injection when used as intended. |
| Performance | 3 | JPA providers translate JPQL to native SQL and apply caching, but the abstraction can make query-plan and index tuning less direct than hand-written SQL. |
| Orthogonality | 3 | Clauses generally compose in a SQL-like way, but object-relational mapping concepts (path expressions, collection-valued associations) introduce special-casing not present in plain SQL. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

JPQL is the formally standardized, SQL-like query language of the Jakarta Persistence specification, offering strong expressiveness and injection resistance over Java entity objects across independently maintained implementations, but like other ORM query languages it is confined to a static entity schema and to in-process Java API usage rather than HTTP transport.

## Sources

- Oracle. (n.d.). [*Chapter 34: The Java Persistence Query Language*](https://docs.oracle.com/javaee/6/tutorial/doc/bnbtg.html).
- Wikipedia. (2025, October 30). [*Jakarta Persistence*](https://en.wikipedia.org/wiki/Jakarta_Persistence).
