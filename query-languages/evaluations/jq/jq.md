# jq

[↑ Full comparison table](../summary.md)

- **Category**: Path/document navigation
- **Official docs**: [jq Manual](https://jqlang.org/manual/)
- **Media type**: None known — jq programs are plain text filter expressions, typically supplied as a command-line argument or a `.jq` script file; there is no registered media type for jq filter syntax itself (the data it operates on is ordinary `application/json`).
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: mature · JavaScript: mature · Java: partial · Go: mature · Rust: mature · .NET: partial
- **Support Model**: open-source-community

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | A full functional pipeline language over JSON: filters compose with `\|`, includes `select`, `map`, `sort_by`, `group_by`, reduce/foreach, array/object construction, string interpolation, regex, and user-defined functions, letting it express filter+sort+reshape+aggregate pipelines in one expression. |
| Simplicity | 3 | The Unix-pipe-inspired `.foo \| .bar[] \| select(...)` style is quick to pick up for simple field access, but its functional/generator semantics (every expression can produce zero, one, or many outputs) and operators like `\|=`, `?`, and `//` are a genuine learning curve beyond basic filters. |
| Flexibility | 5 | Operates purely on ad hoc, dynamically-shaped JSON values with no schema, type declarations, or fixed document model required — any valid JSON document can be queried immediately. |
| Community and Ecosystem | 4 | A long-established (since 2012), ubiquitous command-line tool packaged in virtually every OS/package manager, with an active community, a compatible high-performance fork (jaq) and a maintained C-based reimplementation of the manual, though it remains primarily a CLI/scripting tool rather than a library ecosystem with client SDKs in the style of GraphQL or SQL drivers. |
| Extensibility | 4 | Supports user-defined functions (`def`), importable modules (`import`/`include`), and a documented C-level plugin mechanism for adding new builtins, letting users and downstream tools extend the language beyond its built-in filters. |
| Transport Compatibility | 1 | A command-line/library filter language with no URL-embedding or HTTP-native transport convention of its own; it is invoked as a CLI filter or through language bindings, not passed as a request parameter. |
| Standardization | 1 | A single de-facto-standard implementation-defined language (plus a compatible high-performance fork, jaq) with no formal specification or standards-body governance. |
| Security | 3 | Its own manual documents `--seq`/streaming and sandboxing caveats, and because filters are plain data-transformation expressions with no file/network I/O in the base language, the attack surface for injection is small, but embedding untrusted, user-supplied jq filters (versus untrusted data) into an application still requires care since the language itself was not designed as a sandboxed policy DSL. |
| Performance | 3 | A lightweight, C-implemented streaming JSON processor designed for fast command-line use on typical JSON payloads, though it is not optimized for large-scale concurrent query workloads the way a database query engine is, and its own ecosystem has spawned a faster Rust reimplementation (jaq) partly to address performance-sensitive use cases. |
| Orthogonality | 4 | Every jq expression is a filter that maps inputs to (possibly multiple) outputs and composes uniformly via `\|`, so path navigation, filtering, sorting, and construction all share the same generator/composition model rather than being separate sub-languages. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

jq is a ubiquitous, functional command-line filter language for JSON that composes filter, sort, and slice operations into a single pipeline with no schema or setup required, at the cost of a real conceptual learning curve (its generator-based semantics) and no HTTP-native transport or governance of its own.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```jq
[.[] | select(.category == "electronics" and .price > 100)] | sort_by(.price) | reverse | .[10:20]
```

## Sources

- jqlang / jq project. (n.d.). [*jq Manual*](https://jqlang.org/manual/).
- Wikipedia contributors. (n.d.). [*jq (programming language)*](https://en.wikipedia.org/wiki/Jq_(programming_language)).
