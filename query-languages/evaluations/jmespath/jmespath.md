# JMESPath

[↑ Full comparison table](../summary.md)

- **Category**: Path/document navigation
- **Official docs**: [JMESPath Specification](https://jmespath.org/specification.html)
- **Media type**: None known — no IANA-registered or vendor-documented media type; JMESPath expressions are passed as plain-text CLI arguments (AWS CLI/Azure CLI `--query`) or embedded as string fields in application code, not transmitted as a request body with a dedicated content type.
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Beyond JSONPath-style selection and filtering (`[?a==\`1\`]`), JMESPath's built-in function library adds real sorting (sort, sort_by) and aggregation (avg, sum, max, min, max_by, min_by) directly in the language, plus multi-select list/hash for reshaping nested structures — though it has no concept of joining separate arrays/documents by key. |
| Simplicity | 4 | Basic queries read like plain dotted paths (`foo.bar[0]`), but the full grammar layers in several distinct concepts — literal vs. raw-string syntax, the current-node `@` token, the `&expression` reference type used by higher-order functions like sort_by/map, and subtle projection-stopping rules for pipe- vs. sub-expressions — that go beyond a first glance. |
| Flexibility | 5 | Purpose-built for arbitrary JSON: an identifier that doesn't exist simply evaluates to null rather than raising an error (per the spec's Identifiers section), and wildcard/projection semantics work uniformly across any nested object/array shape. |
| Community and Ecosystem | 4 | JMESPath is the official query syntax behind both the AWS CLI's and Azure CLI's `--query` option, and the JMESPath org maintains seven fully-compliant reference implementations (Python, Go, Lua, JavaScript, PHP, Ruby, Rust) plus community ports (C++, Java, .NET, TypeScript, Elixir), each validated against a shared compliance test suite. |
| Extensibility | 3 | The specification defines a fixed, well-typed set of built-in functions (including a distinct `expression` type for higher-order functions like sort_by/map), but unlike JSONPath's IANA-registered Function Extensions mechanism, the JMESPath spec itself has no standardized way for users to register new functions — extension is only possible ad hoc, at the level of an individual library's own API. |
| Transport Compatibility | 3 | JMESPath expressions are plain strings that fit reasonably in a URL query parameter or JSON request-body field, but in practice they are consumed almost entirely as CLI arguments (AWS CLI's/Azure CLI's `--query`) or in-process library calls rather than transmitted over HTTP, and no IANA media type is registered for it. |
| Standardization | 2 | JMESPath has a complete ABNF grammar and a cross-language compliance test suite that around a dozen independent implementations are validated against, but it remains a single-author specification (James Saryerwinnie) hosted on GitHub/jmespath.org with no formal standards-body (IETF/W3C/ISO/OASIS) governance. |
| Security | 3 | JMESPath queries are typically built as raw strings (e.g. AWS CLI `--query`, Ansible's json_query filter) with no built-in parameterization mechanism, though because it only performs read-only selection over an already-retrieved, in-memory JSON document rather than querying a live backend, injection has a narrower blast radius than in database-facing query languages. |
| Performance | 2 | The specification defines no indexing, query-planning, or lazy-evaluation concept; because JMESPath is designed to post-process a JSON document that's already fully loaded in memory (e.g. filtering an AWS CLI response), the language provides essentially no optimization surface — every evaluation is a full in-memory tree walk. |
| Orthogonality | 4 | The spec's explicit token-precedence table (pipe < or < and < not < rbracket) and composable projection/pipe semantics let sub-expressions, filters, wildcards, and functions combine predictably, though pipe-expressions vs. sub-expressions have a subtle, easy-to-miss distinction in how they stop projections from propagating. |

**Overall score (avg, informational only): 3.4**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

JMESPath is a JSON query language authored by James Saryerwinnie, defined by a complete ABNF grammar and a cross-implementation compliance test suite, and best known as the engine behind the AWS CLI's and Azure CLI's `--query` option. Its filter expressions, pipe/sub-expression composition, and rich built-in function library (including sort_by, max_by, avg, and merge) give it genuine sorting/aggregation capability beyond simple selection, though it remains a single-author specification without formal standards-body governance or a registered media type.

## Sources

- JMESPath (James Saryerwinnie). (n.d.). [*JMESPath Specification*](https://jmespath.org/specification.html).
- JMESPath (James Saryerwinnie). (n.d.). [*JMESPath Libraries*](https://jmespath.org/libraries.html).
- Amazon Web Services (AWS). (n.d.). [*Filtering output in the AWS CLI*](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-filter.html).
