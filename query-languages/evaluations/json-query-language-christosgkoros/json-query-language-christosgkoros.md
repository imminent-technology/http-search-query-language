# JSON Query Language (christosgkoros)

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [json-query-language](https://github.com/christosgkoros/json-query-language)
- Media type: None known — filter objects are embedded as a JSON Schema-validated field within a generic `application/json` request body (per the project's OpenAPI 3.1/3.2 integration examples); no dedicated media type is registered or documented for the predicate language itself.
- Evaluated: 2026-09-09
- Client Libraries: Python: none · JavaScript: partial · Java: none · Go: none · Rust: none · .NET: none
- Support Model: single-vendor-small-team

> Note: this is a distinct, unrelated project that happens to share the exact title "JSON Query Language" with the [jsonquerylang.org project](../json-query-language/json-query-language.md) already cataloged in this repository — see this file's disambiguated slug/label. No independent secondary source exists for this pre-1.0, single-maintainer project, so this evaluation is sourced from the project's own README, SPEC.md, CHANGELOG.md, and its `decisions/` ADR log (re-verified 2026-09-09 against the current `main` branch, tag v0.4.0 — a breaking release that unifies two array-traversal mechanisms into one $some/$every quantifier family and adds the $unknownAs modifier; unreleased commits on top of the tag additionally relax the error-envelope requirement from mandatory RFC 9457 to merely recommended and add a runnable MCP server example).

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Defines a broad, still-34-operator set (unchanged count per CHANGELOG.md) across eight `x-profiles` groups — `core` (logical $and/$or/$nor/$not plus comparison $eq/$ne/$gt/$gte/$lt/$lte/$in/$nin/$exists/$isNull/$unknownAs), `strings`, `regex`, `ranges`, `types`, `collections` ($some/$every/$hasAll/$size), `refs` (cross-field $field/$literal), and `text` ($search) — plus a field path grammar (SPEC.md §3.2) with dot-nesting and array indices. v0.4.0's new `$every` gives it universal quantification over array elements, a predicate the language's own CHANGELOG says was "not previously expressible" (only existential `$elemMatch`/`$some` existed), a genuine capability gain even though sorting/pagination/joins remain deliberately out of scope. |
| Simplicity | 3 | Uses a deliberately SQL-flavored, readable JSON structure (sibling keys AND together per SPEC.md §4.4, bare scalars mean equality), and v0.4.0 collapses what were two array mechanisms ($elemMatch plus a `[*]` wildcard path segment) into one quantifier family — a net simplification. But the formal apparatus keeps deepening: a three-valued TRUE/FALSE/UNKNOWN truth table (§4.1) now with an explicit `$nor` row, a type-mismatch table (§4.3, FALSE for equality operators vs. UNKNOWN for ordering/string/array ones), and a new `$unknownAs` modifier whose order-of-application and non-distribution-over-negation rules (§4.6) are easy to get subtly wrong. |
| Flexibility | 4 | Operates over arbitrary JSON documents with no fixed field list by default, and ships a generator (`tools/generate-filter-schema.mjs`) that derives a narrower, per-resource filter schema (with per-field operators/domains) from any existing JSON Schema; its own test suite (`tests/generator.test.mjs`) asserts the generated schema is strictly narrowing — everything it accepts the published grammar also accepts. The generator now also emits `$every` and `$unknownAs` on generated schemas, omitting each precisely where it would be a constant (a required, non-nullable field), the same rule it already applied to `$exists`/`$isNull`. |
| Community and Ecosystem | 1 | A pre-1.0, single-maintainer project (2 GitHub stars, 0 forks, two contributors — one human plus an AI coding assistant, both under christosgkoros/claude) now on its third tagged release (v0.4.0, 2026-09-07) with a runnable MCP server example added on top, but still explicitly not packaged for consumption: the release workflow still uploads nothing to npm/GitHub Packages, and RELEASING.md frames restoring that as future work contingent on the project's name being settled. |
| Extensibility | 4 | Explicitly designed around conformance profiles (`core`/`strings`/`regex`/`ranges`/`types`/`collections`/`refs`/`text`) that implementations can adopt piecemeal (SPEC.md §2.1), a documented `x-jql` per-field override mechanism, a schema-generator tool for resource-specific extensions, and a formal vendor-extension rule (SPEC.md §6: custom operators MUST use a distinct prefix like `$x_` and MUST NOT be advertised under the unmodified `$id`). A new `decisions/` ADR folder (added in v0.4.0) now documents the reasoning behind grammar changes, reinforcing the extension model's own governance discipline. |
| Transport Compatibility | 3 | Purpose-built for HTTP APIs as a JSON request-body field — documented integration patterns cover both a conventional `POST /resource/search` (OpenAPI 3.1) and the `QUERY` HTTP method (OpenAPI 3.2), citing RFC 10008 which the README confirms reached Proposed Standard in June 2026 — but it remains JSON-body-native rather than URL-query-string-native, with no dedicated GET/URL-encoding story. A new runnable `examples/mcp-server/` strengthens the agent-facing (tool-argument) transport case specifically, without changing the URL-transport gap. |
| Standardization | 1 | A single individual's working-title specification — now split across README.md, a normative SPEC.md (using RFC 2119/8174 keywords and a semver-based versioning policy in §9), CHANGELOG.md, COMPARISON.md, and a new `decisions/` ADR log — but still self-published with an explicitly unsettled name and provisional identifiers (its own `$id` URL, now naming v0.4.0, does not currently resolve). The unreleased changes since v0.4.0 even relax one prior normative requirement (the error envelope is no longer mandated as RFC 9457), moving further from, not toward, a fixed external standard. |
| Security | 4 | SPEC.md §7 formally sets RECOMMENDED safety limits (nesting depth 10, total clauses 100, set length 1000, request body 64 KiB, `$regex` execution 100ms/non-backtracking engine) with mandatory rejection rather than truncation on overflow, and §8 still mandates a `400` response naming which of five conditions applies plus an RFC 6901 pointer at the offending clause — structural, schema-validated construction rather than string concatenation. One post-v0.4.0 unreleased change loosens §8: RFC 9457 `application/problem+json` is now only the RECOMMENDED default envelope rather than a MUST, though the substantive protection (naming the condition, locating the clause) is unchanged. |
| Performance | 3 | No independent benchmarks are published; the design defers actual query execution to whatever backend a server compiles the filter into (the repo's own `experiments/filter-to-sql` explores compiling to SQL), so performance depends entirely on the implementation rather than the language itself. SPEC.md §7 now explicitly flags `$some`/`$every` as the most expensive operators on most backends and lets a server decline the whole `collections` profile rather than accept them. |
| Orthogonality | 4 | v0.4.0 directly resolves the inconsistency flagged in the prior evaluation: the two previously separate array-traversal mechanisms — `$elemMatch` and the `[*]` wildcard path segment, which differed on existential scope — are unified into one `$some`/`$every` quantifier family, and the schema now gives a decidable disambiguation rule (SPEC.md §5.8) for their operand-shape ambiguity with `$not`. A formal type-mismatch table (§4.3) also now states, uniformly, which operator families resolve to FALSE vs. UNKNOWN. The one remaining deliberate divergence — `$in` compares the whole value rather than array membership, unlike MongoDB — is unchanged, but is explicitly documented as an intentional, load-bearing design choice rather than an unexplained exception. |

**Overall score (avg, informational only): 3.1**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

JSON Query Language (christosgkoros) is a pre-1.0, single-maintainer JSON Schema-described predicate/filter language purpose-built for OpenAPI search endpoints and MCP tool inputSchemas, offering a broad, profile-organized operator set and a generator that derives per-resource filter schemas with real operand domains. Its v0.4.0 release unifies two previously separate array-traversal mechanisms into one `$some`/`$every` quantifier family (adding genuine universal-quantification expressiveness via `$every`), adds an `$unknownAs` escape hatch for its three-valued logic, and ships a runnable MCP server example — improving internal consistency and its agent-facing story — while a subsequent unreleased change relaxes its error-envelope requirement from mandatory RFC 9457 to merely recommended. It remains an unstandardized, pre-naming working title with a tiny community (still no published npm/GitHub Packages artifact) and shares its common name with the unrelated jsonquerylang.org project.

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

- Gkoros, C. (n.d.). [*json-query-language*](https://github.com/christosgkoros/json-query-language) (README, v0.4.0). GitHub.
- Gkoros, C. (n.d.). [*SPEC.md — JSON Query Language Specification*](https://github.com/christosgkoros/json-query-language/blob/main/SPEC.md) (v0.4.0 grammar). GitHub.
- Gkoros, C. (n.d.). [*CHANGELOG.md*](https://github.com/christosgkoros/json-query-language/blob/main/CHANGELOG.md). GitHub.
- Gkoros, C. (n.d.). [*decisions/0001-array-quantifiers-and-unknown-handling.md*](https://github.com/christosgkoros/json-query-language/blob/main/decisions/0001-array-quantifiers-and-unknown-handling.md). GitHub.
