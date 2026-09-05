# JSONPath

[↑ Full comparison table](../summary.md)

- **Category**: Path/document navigation
- **Official docs**: [RFC 9535 - JSONPath: Query Expressions for JSON](https://www.rfc-editor.org/rfc/rfc9535)
- **Media type**: `application/jsonpath` — IANA-registered per RFC 9535 §3.1 (intended usage: COMMON).
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports name/wildcard/index/slice/filter selectors, a recursive descendant segment (`..`), and five built-in function extensions (length, count, match, search, value) enabling regex-based filtering and existence tests (RFC 9535 §2.3-2.4), but has no native sorting, aggregation beyond count()/length(), or cross-document joins. |
| Simplicity | 4 | The core dot/bracket syntax (e.g. `$.store.book[0].title`) is compact and immediately readable, but the full RFC 9535 grammar adds real complexity — filter-expression well-typedness rules, dual single/double-quote string literals, and Unicode scalar-value escaping — that a conformant implementation must get right. |
| Flexibility | 5 | Purpose-built for JSON's schema-less object/array model: a segment simply produces an empty nodelist when a member or index doesn't exist rather than raising an error (RFC 9535 §2.1.2), making it naturally tolerant of missing fields and evolving document shapes. |
| Community and Ecosystem | 3 | Wikipedia cites over fifty independent implementations catalogued by the JSONPath Comparison Project and wide use in the Java ecosystem, but RFC 9535 itself exists precisely because pre-2024 implementations diverged in behavior (many delegating fragments to a host language's `eval()`); ecosystem-wide conformance to the 2024 standard is still catching up. |
| Extensibility | 4 | RFC 9535 §2.4 defines a formal "Function Extensions" mechanism with a typed parameter/result system (ValueType/LogicalType/NodesType) and a dedicated IANA "Function Extensions" subregistry (§3.2) for registering functions beyond the five predefined ones — a genuine, standardized extension point. |
| Transport Compatibility | 3 | Has an IANA-registered `application/jsonpath` media type (RFC 9535 §3.1, intended usage COMMON) for conveying queries in JSON data, but it is predominantly consumed by libraries embedded in application/CLI code (e.g. `kubectl -o jsonpath`, the Java JsonPath library) rather than as an established HTTP query-string or request-body convention. |
| Standardization | 5 | Defined by RFC 9535, an IETF Internet Standards Track (Proposed Standard) specification published in February 2024, formalizing Stefan Gössner's original 2007 proposal after 17 years of divergent implementations. |
| Security | 3 | RFC 9535 §4 explicitly warns that historical JSONPath implementations fed query fragments to a host language's `eval()`, enabling injection, and requires conformant implementations to parse the full grammar instead of relying on such engines; §4.2 further warns that queries formed from untrusted variables still need validation and delimiter escaping. |
| Performance | 3 | The grammar distinguishes cheap child-segment access (name/index/slice) from potentially expensive recursive descendant (`..`) and filter-selector traversal, but RFC 9535 defines no indexing or query-planning concept itself; academic work on SIMD-accelerated descendant-segment processing exists precisely because naive descendant search is costly. |
| Orthogonality | 4 | Selectors combine consistently within a bracketed child segment (name, index, slice, filter can all appear together), descendant and filter segments nest freely, and function extensions integrate through a single declared type system that keeps composition well-typed and predictable (RFC 9535 §2.4.1). |

**Overall score (avg, informational only): 3.8**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.8**

## Summary

JSONPath (RFC 9535) is a lightweight, XPath-inspired path syntax for selecting and extracting values from JSON documents, standardized by the IETF in 2024 after 17 years of divergent library implementations. Its dot/bracket segment syntax, filter selectors, and typed function-extension mechanism make it well suited to schema-less JSON navigation, though it has no native sorting, aggregation, or join support and is used mainly as an embedded library/CLI convention rather than a first-class HTTP query mechanism.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```jsonpath
$.products[?@.category=="electronics" && @.price>100]
```

JSONPath (RFC 9535) has no sort function — only the filter selector shown above is natively expressible. Pagination via the array slice selector (e.g. `[10:20]`) only works if the array is already sorted by price, since JSONPath itself provides no ordering capability.

## Sources

- IETF (RFC Editor). (2024, February). [*RFC 9535: JSONPath: Query Expressions for JSON*](https://www.rfc-editor.org/rfc/rfc9535).
- Wikipedia. (2026, August 7). [*JSONPath*](https://en.wikipedia.org/wiki/JSONPath).
- Gössner, S. (2007, February 21). [*JSONPath - XPath for JSON*](https://goessner.net/articles/JsonPath/).
