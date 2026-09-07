# FQL (CrowdStrike)

[↑ Full comparison table](../summary.md)

- **Category**: Log/security search
- **Official docs**: [Falcon Query Language (FQL)](https://developer.crowdstrike.com/api-reference/falcon-query-language/)
- **Media type**: None known — FQL filter strings are passed as the value of a `filter` query-string parameter on CrowdStrike Falcon REST API requests (transported as ordinary URL-encoded text, not a registered media type of their own).
- **Evaluated**: 2026-09-15

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | A compact filter expression language with `<property>:[operator]<value>` comparisons (`!`, `>`, `>=`, `<`, `<=`, `~`, `!~`, wildcard `*`), combinators (`+` for AND, `,` for OR), parentheses for grouping complex expressions, and exact-match array syntax (`[...]`), covering the common filter needs of CrowdStrike's security APIs without a broader general-purpose expression grammar (no comprehensions, functions, or joins). |
| Simplicity | 4 | A small, consistent grammar built around one comparison pattern (`field:op'value'`) combined with just two combinator symbols (`+`/`,`), documented in a single reference page and quick to learn for basic filters. |
| Flexibility | 3 | Used strictly as the `filter` query parameter against CrowdStrike Falcon's own fixed, per-endpoint resource schemas (detections, hosts, incidents, etc.) — it is not a general-purpose or schema-free query language usable outside the Falcon API surface. |
| Community and Ecosystem | 2 | A single-vendor (CrowdStrike) filter syntax documented for and used exclusively within the Falcon platform's REST APIs, with community knowledge concentrated in CrowdStrike's own developer portal and partner integrations rather than an independent, multi-vendor ecosystem. |
| Extensibility | 1 | The documentation describes a fixed set of comparison operators and combinators per resource with no user-defined function, custom-operator, or plugin mechanism for extending the filter grammar itself. |
| Transport Compatibility | 4 | Purpose-built as a URL query-string filter parameter for CrowdStrike's REST APIs — genuinely HTTP-native by design, passed directly as `?filter=...` (URL-encoded) alongside separate `sort`/`limit`/`offset` parameters for ordering and pagination. |
| Standardization | 1 | A single-vendor, product-specific filter syntax documented only on CrowdStrike's own developer portal, with no external specification or standards-body governance. |
| Security | 2 | No dedicated FQL-specific injection-prevention or sandboxing documentation was found; as a query-string filter value it is exposed to standard URL-encoding/injection considerations that the calling application must handle (e.g., proper encoding of user-supplied filter values), and CrowdStrike's docs do not describe additional language-level safeguards beyond the fixed operator set. |
| Performance | 3 | Runs as a query-string filter against CrowdStrike's own indexed Falcon API resources; the documentation does not publish a formal performance/complexity model, so throughput depends on CrowdStrike's backend implementation rather than anything FQL itself guarantees or exposes. |
| Orthogonality | 3 | The single `field:op'value'` comparison pattern combines uniformly with `+`/`,` combinators and parentheses across every documented resource/endpoint, giving consistent, predictable filter composition, though sorting and pagination live entirely outside FQL as separate API parameters rather than being part of the same orthogonal grammar. |

**Overall score (avg, informational only): 2.6**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.9**

## Summary

CrowdStrike's Falcon Query Language (FQL) is a compact, single-vendor filter-expression syntax purpose-built for the `filter` parameter of Falcon REST API requests, offering a small consistent set of comparison operators and AND/OR combinators — but it covers filtering only, leaving sorting and pagination to separate API parameters, and has no extensibility or standards-body governance of its own.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```fql
category:'electronics'+price:>'100'
```

FQL itself only expresses the filter predicate — sorting and pagination are separate CrowdStrike Falcon API parameters, not FQL syntax. The equivalent request would combine this filter with `sort=price.desc&limit=10&offset=10` as distinct query-string parameters alongside `filter=category:'electronics'+price:>'100'`.

## Sources

- CrowdStrike. (n.d.). [*Falcon Query Language (FQL)*](https://developer.crowdstrike.com/api-reference/falcon-query-language/). CrowdStrike Developer Portal.
