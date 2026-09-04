# Criteria API

- **Category**: Relational/SQL-family
- **Official docs**: [Chapter 32: Introduction to the Java Persistence API](https://docs.oracle.com/javaee/6/tutorial/doc/bnbpz.html)
- **Media type**: Not applicable — the Criteria API is a Java object-graph API for building queries programmatically; it has no serialized wire format.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Builds SQL-like queries programmatically with joins, subqueries, aggregate and group-by expressions, and dynamic predicate composition, though more verbose to write than an equivalent JPQL string. |
| Simplicity | 2 | The type-safe, fluent-builder style requires generated metamodel classes and verbose Java code for even simple queries, a steeper learning curve than writing a JPQL/SQL string directly. |
| Flexibility | 2 | Like JPQL, it operates over a fixed, annotated object-relational entity schema and is not designed for dynamic or schema-less data. |
| Community and Ecosystem | 4 | Part of the same widely-adopted Jakarta Persistence specification as JPQL, implemented by Hibernate, EclipseLink and OpenJPA, with mature documentation and IDE tooling for the generated metamodel. |
| Extensibility | 3 | Supports custom expressions and generic function calls similar to JPQL, but the API surface itself is fixed by the specification. |
| Transport Compatibility | 1 | Exists only as an in-process Java API for building queries; has no notion of URL or HTTP transport. |
| Standardization | 5 | Formally part of the Jakarta Persistence specification (JSR 317/338), implemented independently by multiple ORM vendors. |
| Security | 5 | Queries are built entirely from typed Java objects and bound parameters rather than string concatenation, making it structurally resistant to injection by construction. |
| Performance | 3 | Translated to native SQL by the JPA provider with the same caching/optimization characteristics as JPQL; the type-safe API adds no runtime cost beyond query construction. |
| Orthogonality | 3 | Predicates and expressions compose fluently as Java objects, but the API's verbosity and reliance on generated metamodel classes add indirection compared to a plain query string. |

**Overall score (avg, informational only): 3.2**

## Summary

The JPA Criteria API is a type-safe, programmatic alternative to JPQL that is structurally immune to injection by construction and formally standardized alongside it, but its fluent, metamodel-driven style trades away the simplicity of writing plain query strings and, like JPQL, is confined to in-process Java use over a fixed entity schema.

## Sources

- Oracle. (n.d.). [*Chapter 32: Introduction to the Java Persistence API*](https://docs.oracle.com/javaee/6/tutorial/doc/bnbpz.html).
- Wikipedia. (2025, October 30). [*Jakarta Persistence*](https://en.wikipedia.org/wiki/Jakarta_Persistence).
