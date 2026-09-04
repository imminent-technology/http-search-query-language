# GraphQL

- **Category**: API/data-fetching
- **Official docs**: [graphql.org](https://graphql.org/)
- **Media type**: `application/graphql-response+json` (responses) and `application/json` (requests) per the GraphQL-over-HTTP specification (graphql.github.io/graphql-over-http). Not registered with IANA. (A legacy, non-standard `application/graphql` convention for raw request bodies exists in some older server implementations but is not part of any official spec.)
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports precise nested field selection, mutations, and subscriptions across a typed schema, but per Wikipedia's own comparison section it is not a full graph query language — it cannot, for example, return an unbounded set of ancestors in a single query the way SPARQL or recursive SQL can. |
| Simplicity | 4 | Declarative queries mirror the shape of the UI/response, and the schema is self-documenting via introspection, though fragments, directives, and variable handling add complexity beyond trivial queries. |
| Flexibility | 4 | Storage-agnostic and designed for continuous schema evolution without versioning (fields can be deprecated and added without breaking clients), though every query is still bound to a predefined schema rather than being truly schema-less. |
| Community and Ecosystem | 5 | Governed by the GraphQL Foundation under the Linux Foundation since 2018, with adoption by Meta, GitHub, Shopify, AWS, and a large tooling ecosystem (GraphiQL, Apollo, GraphQL Hive). |
| Extensibility | 4 | Custom scalars, directives, and resolvers give strong extension points, and the schema-first model lets teams add domain-specific types and operations. |
| Transport Compatibility | 4 | Purpose-built for HTTP APIs — queries are usually POSTed as a JSON body to a single endpoint, and simple queries can also be passed as URL query-string parameters, though large queries are not comfortably URL-embeddable. |
| Standardization | 4 | Defined by a formal, versioned open specification (spec.graphql.org) governed by a vendor-neutral foundation with many independent server/client implementations, though it is not an ISO/W3C-level standard. |
| Security | 4 | The strongly-typed schema validates queries before execution, reducing injection-style risks, but introduces its own attack surface (query depth/complexity abuse, introspection exposure) that requires separate mitigation. |
| Performance | 3 | Performance depends heavily on resolver implementation; the well-known N+1 query problem typically requires patterns like DataLoader batching rather than being solved by the language/runtime itself. |
| Orthogonality | 4 | Queries, mutations, and subscriptions are cleanly separated operation types, and fragments/directives compose predictably against a single consistent type system. |

**Overall score (avg, informational only): 4.0**

## Summary

GraphQL is the strongest of the pilot languages for HTTP-native API design and client-driven flexibility, trading full graph-traversal expressiveness and built-in query optimization for precision, schema evolution, and a very active vendor-neutral ecosystem.

## Sources

- The GraphQL Foundation. (n.d.). [*The query language for modern APIs*](https://graphql.org/).
- Wikipedia. (2026, September 1). [*GraphQL*](https://en.wikipedia.org/wiki/GraphQL).
- The GraphQL Foundation. (2025, September 3). [*GraphQL Specification — September 2025 Release*](https://spec.graphql.org/).
