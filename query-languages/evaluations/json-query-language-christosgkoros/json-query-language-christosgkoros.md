# JSON Query Language (christosgkoros)

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [json-query-language](https://github.com/christosgkoros/json-query-language)
- Media type: None known — filter objects are embedded as a JSON Schema-validated field within a generic `application/json` request body (per the project's OpenAPI 3.1/3.2 integration examples); no dedicated media type is registered or documented for the predicate language itself.
- Evaluated: 2026-09-07

> Note: this is a distinct, unrelated project that happens to share the exact title "JSON Query Language" with the [jsonquerylang.org project](../json-query-language/json-query-language.md) already cataloged in this repository — see this file's disambiguated slug/label. No independent secondary source exists for this pre-1.0, single-maintainer project, so this evaluation is sourced from the project's own README, SPEC.md, and CHANGELOG.md (re-verified 2026-09-07 against the current `main` branch, tag v0.3.1 — the schema/grammar itself is unchanged from v0.3.0; v0.3.1 only removed an npm/GitHub Packages publish attempt and fixed a broken install instruction).

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Defines a broad operator set across eight `x-profiles` groups — `core` (logical $and/$or/$nor/$not plus comparison $eq/$ne/$gt/$gte/$lt/$lte/$in/$nin/$exists/$isNull), `strings`, `regex`, `ranges`, `types`, `collections` ($hasAny/$hasAll/$hasNone/$size/$elemMatch), `refs` (cross-field $field/$literal), and `text` ($search) — plus a field path grammar (SPEC.md §3.2) with dot-nesting, array indices, and `[*]` wildcards, covering most relational-style filtering needs. |
| Simplicity | 3 | Uses a deliberately SQL-flavored, readable JSON structure (sibling keys AND together per SPEC.md §4.4, bare scalars mean equality), but SPEC.md's own formal apparatus — a three-valued TRUE/FALSE/UNKNOWN truth table (§4.1), a missing-vs-null distinction table (§4.2), and an ABNF field-path grammar (§3.2) — confirms this is a genuinely deeper model than the basic JSON shape suggests. |
| Flexibility | 4 | Operates over arbitrary JSON documents with no fixed field list by default, and ships a generator (`tools/generate-filter-schema.mjs`) that derives a narrower, per-resource filter schema (with per-field operators/domains) from any existing JSON Schema; its own test suite (`tests/generator.test.mjs`) asserts the generated schema is strictly narrowing — everything it accepts the published grammar also accepts. |
| Community and Ecosystem | 1 | A pre-1.0, single-maintainer project (2 GitHub stars, 0 forks, one human contributor plus an AI coding assistant) that as of the v0.3.1 release (2026-09-04) has explicitly *stopped* even attempting to publish to npm/GitHub Packages — the release workflow now "uploads nothing" and the `NPM_TOKEN` secret was deleted — reinforcing rather than changing its "not yet packaged for consumption" status. |
| Extensibility | 4 | Explicitly designed around conformance profiles (`core`/`strings`/`regex`/`ranges`/`types`/`collections`/`refs`/`text`) that implementations can adopt piecemeal (SPEC.md §2.1), a documented `x-jql` per-field override mechanism, a schema-generator tool for resource-specific extensions, and a formal vendor-extension rule (SPEC.md §6: custom operators MUST use a distinct prefix like `$x_` and MUST NOT be advertised under the unmodified `$id`). |
| Transport Compatibility | 3 | Purpose-built for HTTP APIs as a JSON request-body field — documented integration patterns cover both a conventional `POST /resource/search` (OpenAPI 3.1) and the `QUERY` HTTP method (OpenAPI 3.2), citing RFC 10008 which SPEC.md §10 confirms reached Proposed Standard in June 2026 — but it remains JSON-body-native rather than URL-query-string-native, with no dedicated GET/URL-encoding story. |
| Standardization | 1 | A single individual's working-title specification — now split across README.md, a normative SPEC.md (using RFC 2119/8174 keywords and a semver-based versioning policy in §9), CHANGELOG.md, and COMPARISON.md — but still self-published with an explicitly unsettled name and provisional identifiers (its own `$id` URL does not currently resolve); it references external standards (JSON Schema, RFC 9457, RFC 10008) without being standardized by any independent body itself. |
| Security | 4 | SPEC.md §7 formally sets RECOMMENDED safety limits (nesting depth 10, total clauses 100, set length 1000, request body 64 KiB, `$regex` execution 100ms/non-backtracking engine) with mandatory rejection rather than truncation on overflow, and §8 defines an RFC 9457 `application/problem+json` error model — structural, schema-validated construction rather than string concatenation. |
| Performance | 3 | No independent benchmarks are published; the design defers actual query execution to whatever backend a server compiles the filter into (the repo's own `experiments/filter-to-sql` explores compiling to SQL), so performance depends entirely on the implementation rather than the language itself. |
| Orthogonality | 3 | The core model is fairly uniform — one `Constraint` shared across every field, AND-by-default sibling composition at every nesting level (SPEC.md §4.4) — but several operators carry special-cased exceptions that SPEC.md itself calls out as surprising: three-valued `$not`/`$ne` excluding nulls (§4.1), `$in` comparing the whole value rather than array membership (§5.4), and `$elemMatch` vs. wildcard-path existential semantics differing on which element(s) must match (§5.9). |

**Overall score (avg, informational only): 3.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

JSON Query Language (christosgkoros) is a pre-1.0, single-maintainer JSON Schema-described predicate/filter language purpose-built for OpenAPI search endpoints and MCP tool inputSchemas, offering a broad, profile-organized operator set and a generator that derives per-resource filter schemas with real operand domains. Its formal SPEC.md now documents rigorous safety limits, three-valued evaluation semantics, and an RFC 9457 error model, giving it a solid security posture and stronger internal consistency than a bare README would suggest — but as an unstandardized, pre-naming working title with a tiny community (which as of v0.3.1 has explicitly stopped even attempting to publish a package) it remains an early-stage design rather than a production-ready specification, and it shares its common name with the unrelated jsonquerylang.org project.

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

- Gkoros, C. (n.d.). [*json-query-language*](https://github.com/christosgkoros/json-query-language) (README, v0.3.1). GitHub.
- Gkoros, C. (n.d.). [*SPEC.md — JSON Query Language Specification*](https://github.com/christosgkoros/json-query-language/blob/main/SPEC.md) (v0.3.0 grammar). GitHub.
- Gkoros, C. (n.d.). [*CHANGELOG.md*](https://github.com/christosgkoros/json-query-language/blob/main/CHANGELOG.md). GitHub.
