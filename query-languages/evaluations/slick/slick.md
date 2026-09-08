# Slick

[↑ Full comparison table](../summary.md)

- **Category**: Language-integrated
- **Official docs**: [Functional Relational Mapping for Scala](https://scala-slick.org/)
- **Media type**: Not applicable — Slick is an in-process Scala library that compiles queries to SQL executed over JDBC; it is not itself transmitted over HTTP and has no wire format of its own.
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: none · JavaScript: none · Java: partial · Go: none · Rust: none · .NET: none
- **Support Model**: open-source-community

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports filtering, mapping, sorting, applicative and monadic joins (including cross/inner/outer/zip joins), grouping, and aggregation (min/max/sum/avg/count/exists) via a Scala-collections-like query API, with an escape hatch to Plain SQL for anything the typed API can't express. |
| Simplicity | 3 | Deliberately modeled on Scala's own collections API (`filter`/`map`/`sortBy`/`take`/`drop`), which lowers the barrier for Scala developers, but its "lifted embedding" (`Rep[T]` types, implicit conversions, `===`/`=!=` instead of `==`/`!=`) is a real conceptual departure from plain Scala that takes time to internalize. |
| Flexibility | 2 | Queries are built against an explicit `Table` class representation mapped to relational tables/columns (optionally code-generated from an existing schema), so it is not schema-less, though the same query API works across many supported relational engines via pluggable profiles. |
| Community and Ecosystem | 3 | A long-running, community-maintained project (since 2011) backed historically by Lightbend, with real adoption in the Scala ecosystem and active support channels (GitHub Discussions, Discord), but it is narrower in reach than mainstream Java ORMs/query builders and has had periods of slower release cadence. |
| Extensibility | 4 | Supports custom column types and converters, custom SQL profiles for additional database engines, user-defined SQL functions (`SimpleFunction`), and Plain SQL string interpolation for constructs the typed query compiler can't express. |
| Transport Compatibility | 1 | Pure in-process Scala library operating over a JDBC connection (or async wrapper); it has no network transport, URL-embedding convention, or request-body format of its own. |
| Standardization | 1 | A proprietary, single-project Scala DSL with no standards-body specification or independent implementations. |
| Security | 4 | The primary typed query API is built entirely from Scala expressions and column references with no string concatenation, and its documented Plain SQL string-interpolation API (`sql"..."`) binds interpolated values as JDBC parameters rather than inlining raw text — though nothing prevents a caller from constructing an unsafe raw string themselves outside that interpolator. |
| Performance | 3 | Built on an async, non-blocking runtime (Cats Effect/FS2-based in current releases) with connection-pooling and a documented query compiler that generates SQL per-backend, but as with any query builder its real-world performance ultimately depends on the underlying database and JDBC driver rather than anything Slick optimizes itself. |
| Orthogonality | 4 | Query composition (`filter`, `sortBy`, `take`/`drop`, joins, `groupBy`), action composition (via for-comprehensions on `DBIOAction`), and row-expression composition are explicitly documented as three separate, independently composable layers, each mirroring Scala's own collection/for-comprehension semantics consistently. |

**Overall score (avg, informational only): 2.9**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.1**

## Summary

Slick brings LINQ-like, Scala-collections-style query composition to relational databases through a typed, async-first Scala DSL, trading true schema flexibility and any HTTP-facing transport of its own for compile-time-checked queries that read almost exactly like ordinary Scala collection operations.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```scala
val page2 = products
  .filter(p => p.category === "electronics" && p.price > 100.0)
  .sortBy(_.price.desc)
  .drop(10)
  .take(10)
  .result
```

## Sources

- Slick / Lightbend community. (n.d.). [*Functional Relational Mapping for Scala*](https://scala-slick.org/).
- Slick / Lightbend community. (n.d.). [*Queries*](https://scala-slick.org/doc/stable/queries.html). Slick 3.6.1 Documentation.
