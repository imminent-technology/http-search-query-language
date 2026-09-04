# JSON Query Language

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [JSON Query](https://jsonquerylang.org/)
- Media type: None known — no registered or documented media type found for this specification (jsonquerylang.org).
- Evaluated: 2026-09-04

> Note: No independent secondary source (e.g. Wikipedia) exists for this niche, relatively young project, so this evaluation is single-sourced from the project's own site/documentation.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | Provides a functional pipe/chain model with property getters, operators, functions (filter, sort, map, pick, aggregate functions), objects for parallel transforms, and arrays, covering most common query and transform needs, though its own docs acknowledge its scope is intentionally smaller than full-featured JSON query languages. |
| Simplicity | 4 | Explicitly designed as a reaction against JSONPath/JMESPath-style syntaxes that rely on dense special characters (@, $, \|, ?, :, *, &); its Text Format instead resembles familiar JavaScript/Lodash method chaining, which the project states makes it easy to learn. |
| Flexibility | 5 | Operates directly over arbitrary JSON documents and arrays with no schema requirement whatsoever, reflecting JSON's own inherently schema-free structure. |
| Community and Ecosystem | 1 | A small, single-maintainer open-source project with a modest set of listed implementations; it has nowhere near the adoption of established JSON query languages like JSONPath or JMESPath, let alone mainstream database query languages. |
| Extensibility | 4 | Explicitly marketed as "expandable", with a documented, easy-to-parse intermediate JSON Format (arrays of function calls) specifically designed to make it straightforward to build new integrations, GUIs, or ports to other languages/environments. |
| Transport Compatibility | 2 | Used as an embedded library function (`jsonquery(data, query)`) invoked programmatically within an application, rather than being designed for direct HTTP/URL query-string embedding. |
| Standardization | 1 | A single open-source project's own bespoke specification with no independent standards body behind it, unlike JSONPath which has an IETF RFC (RFC 9535). |
| Security | 4 | Explicitly designed with security as a stated goal: property access is restricted to plain JSON objects/arrays and disallows accessing object methods or class properties specifically "because accessing arbitrary properties may introduce security risks" — a direct contrast to the JavaScript+Lodash approach it calls out as an injection risk. |
| Performance | 3 | Built to be extremely lightweight (small bundle size, suitable for browser use) by leveraging native JSON parsing and built-in language functions, though no independent large-scale performance benchmarks are documented. |
| Orthogonality | 4 | The entire language reduces to a small set of uniform, composable constructs — functions, operators, pipes, objects, arrays, and property getters — all of which convert cleanly and losslessly between the Text Format and an equivalent JSON Format. |

**Overall score (avg, informational only): 3.1**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

JSON Query Language is a small, deliberately minimal, and explicitly security-conscious functional query language for arbitrary JSON data, designed to avoid the dense special-character syntax of JSONPath/JMESPath in favor of readable pipe/chain composition, but as a young single-maintainer project it has a tiny community, no independent standardization, and is used as an embedded library call rather than a URL-native transport mechanism.

## Sources

- JSON Query project (Jos de Jong). (n.d.). [*JSON Query*](https://jsonquerylang.org/).
