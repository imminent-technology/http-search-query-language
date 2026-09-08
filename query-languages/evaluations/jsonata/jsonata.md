# JSONata

[↑ Full comparison table](../summary.md)

- **Category**: Path/document navigation
- **Official docs**: [JSONata Overview](https://docs.jsonata.org/overview)
- **Media type**: application/jsonata (an unregistered, community-proposed media type suggested in JSONata discussions; not an IANA-registered type). JSONata expressions themselves are typically embedded as plain strings within a host application's own JSON payload or configuration.
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: mature · JavaScript: mature · Java: partial · Go: partial · Rust: partial · .NET: partial
- **Support Model**: single-vendor-small-team

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Combines path navigation, bracket-predicate filtering, the `^(...)` sort operator (with `>`/`<` multi-key sort), array range slicing (`[i..j]`), grouping (`{...}`), joins across arrays, higher-order functions, and a large standard function library, letting a single expression filter, sort, group, and reshape JSON in one pass. |
| Simplicity | 3 | The core path/predicate syntax (`Account.Order[Quantity>5]`) is approachable and reads close to plain property access, but sequence-flattening semantics, context variables (`$`, `$$`), and the transform/reduce operators add real conceptual depth once queries go beyond simple filters. |
| Flexibility | 5 | Operates purely on ad hoc, dynamically-shaped JSON with no schema or type declarations required — any JSON document can be queried immediately, and the same expressions work equally over deeply nested or flat structures. |
| Community and Ecosystem | 3 | An open-source (JS Foundation-hosted) project with an official JS implementation, community ports to Java/Python/.NET/Rust, browser-based "try JSONata" tooling, and real adoption inside integration platforms (e.g., IBM App Connect, Digital.ai) as an embedded transformation language, though its overall developer mindshare is narrower than GraphQL, SQL, or jq. |
| Extensibility | 4 | Supports user-defined functions (`function($x){...}`), lambda expressions, and a documented mechanism for registering custom native functions from host environments (e.g., extending the JS binding with new built-ins). |
| Transport Compatibility | 2 | No IANA-registered media type or formal URL-query-parameter convention exists, but its own community has proposed an `application/jsonata` content type for transformation-as-a-service use cases, and it is commonly passed as a string parameter/body field to transformation APIs. |
| Standardization | 1 | A single-project, JS-Foundation-hosted specification with no ratification by a standards body (ISO/IETF/W3C); the JSON-native XPath/XQuery-inspired design is documented but governed by one open-source project rather than a multi-stakeholder committee. |
| Security | 3 | Expressions are declarative data-transformation programs evaluated in a sandboxed interpreter (no ambient file/network I/O in the base language), which limits the blast radius of a malicious expression, but embedding fully untrusted, user-authored JSONata (rather than just untrusted data) still requires the same care as any embedded expression language, and no formal security audit or threat model is published in the docs reviewed. |
| Performance | 3 | A lightweight, pure-JS (or ported) tree-walking evaluator suited to typical API-integration and transformation payload sizes, but it is not a database query engine with index-aware optimization, so performance on very large documents depends on the host's evaluation strategy rather than anything JSONata optimizes internally. |
| Orthogonality | 4 | Path steps, predicate filters, the sort operator, range operator, and object/array constructors are documented as independently composable pieces of one expression grammar, so filtering, sorting, and reshaping combine predictably in a single chained expression (as in the example query below). |

**Overall score (avg, informational only): 3.2**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

JSONata is a lightweight, JS-Foundation-hosted expression language purpose-built for querying and transforming ad hoc JSON, chaining path predicates, a dedicated sort operator, and array range slicing into single, schema-free expressions — at the cost of a single-project governance model and no IANA-registered transport convention.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```jsonata
products[category = "electronics" and price > 100]^(>price)[10..19]
```

## Sources

- JSONata.org. (n.d.). [*Path Operators*](https://docs.jsonata.org/path-operators).
- JSONata.org. (n.d.). [*Sorting, Grouping, and Reducing*](https://docs.jsonata.org/sorting-grouping).
- JSONata.org. (n.d.). [*Other Operators*](https://docs.jsonata.org/other-operators).
- JSONata.org. (n.d.). [*Numeric Operators*](https://docs.jsonata.org/numeric-operators).
