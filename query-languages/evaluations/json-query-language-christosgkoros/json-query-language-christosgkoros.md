# JSON Query Language (christosgkoros)

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [json-query-language](https://github.com/christosgkoros/json-query-language)
- Media type: None known — filter objects are embedded as a JSON Schema-validated field within a generic `application/json` request body (per the project's OpenAPI 3.1/3.2 integration examples); no dedicated media type is registered or documented for the predicate language itself.
- Evaluated: 2026-09-04

> Note: this is a distinct, unrelated project that happens to share the exact title "JSON Query Language" with the [jsonquerylang.org project](../json-query-language/json-query-language.md) already cataloged in this repository — see this file's disambiguated slug/label. No independent secondary source exists for this pre-1.0, single-maintainer project, so this evaluation is single-sourced from the project's own README.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Defines a broad operator set across nine profiles — logical ($and/$or/$nor/$not), comparison, ranges, string pattern-matching ($like/$ilike/$startsWith/$endsWith/$contains), regex, types, collections ($hasAny/$hasAll/$hasNone/$size/$elemMatch), cross-field references ($field), and free text ($search) — plus nested paths and array wildcards, covering most relational-style filtering needs. |
| Simplicity | 3 | Uses a deliberately SQL-flavored, readable JSON structure (sibling keys AND together, bare scalars mean equality) but documents several non-obvious gotchas up front — three-valued NOT/null semantics, $in comparing whole values rather than array membership, and a `$$`-escaping rule for literal `$`-prefixed field names — that add a real learning curve beyond the basic shape. |
| Flexibility | 4 | Operates over arbitrary JSON documents with no fixed field list by default, and ships a generator that derives a narrower, per-resource filter schema (with per-field operators/domains) from any existing JSON Schema, trading a bit of schema-agnosticism for stronger correctness guarantees when a resource schema exists. |
| Community and Ecosystem | 1 | A pre-1.0, single-maintainer project (2 GitHub stars, one human contributor plus an AI coding assistant) that is explicitly "not yet packaged for consumption" — unpublished to npm/GitHub Packages and still a working title even for its own name. |
| Extensibility | 4 | Explicitly designed around conformance profiles (core/strings/regex/ranges/types/collections/refs/text) that implementations can adopt piecemeal, plus a documented `x-jql` per-field override mechanism and a schema-generator tool for building resource-specific extensions. |
| Transport Compatibility | 3 | Purpose-built for HTTP APIs as a JSON request-body field — documented integration patterns cover both a conventional `POST /resource/search` (OpenAPI 3.1) and the new `QUERY` HTTP method (OpenAPI 3.2, RFC 10008) — but it is JSON-body-native rather than URL-query-string-native, with no dedicated GET/URL-encoding story. |
| Standardization | 1 | A single individual's working-title specification with an explicitly unsettled name and provisional identifiers (its own `$id` URL does not currently resolve); it references external standards (JSON Schema, RFC 9457, RFC 10008) but is not itself standardized by any independent body. |
| Security | 4 | Ships a dedicated safety section recommending bounds on nesting depth, clause count, set length and body size with rejection (not truncation) on overflow, plus explicit ReDoS guidance to use linear-time regex engines or drop the `regex` profile entirely — structural, schema-validated construction rather than string concatenation. |
| Performance | 3 | No independent benchmarks are published; the design defers actual query execution to whatever backend a server compiles the filter into (the repo's own `experiments/filter-to-sql` explores compiling to SQL), so performance depends entirely on the implementation rather than the language itself. |
| Orthogonality | 3 | The core model is fairly uniform — one `Constraint` shared across every field, AND-by-default sibling composition at every nesting level — but several operators carry special-cased exceptions (three-valued `$not`/`$ne`, `$in` needing a distinct `$hasAny` for array membership, `$elemMatch` vs. wildcard-path semantics) that require explicit documentation to use correctly. |

**Overall score (avg, informational only): 3.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

JSON Query Language (christosgkoros) is a pre-1.0, single-maintainer JSON Schema-described predicate/filter language purpose-built for OpenAPI search endpoints and MCP tool inputSchemas, offering a broad, profile-organized operator set and a generator that derives per-resource filter schemas with real operand domains. Its explicit safety guidance and schema-validated construction give it a solid security posture, but as an unstandardized, pre-naming working title with a tiny community it remains an early-stage design rather than a production-ready specification — and it shares its common name with the unrelated jsonquerylang.org project.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```json
{
  "category": "electronics",
  "price": { "$gt": 100 }
}
```

This project's grammar is a pure filter/predicate language (like SCIM Filter) — sorting and pagination are documented as separate companion parameters of the consuming API endpoint (e.g. a `sortBy`/`page` query parameter), not part of the JSON filter object itself.

## Sources

- Gkoros, C. (n.d.). [*json-query-language*](https://github.com/christosgkoros/json-query-language). GitHub.
