# EQL

[↑ Full comparison table](../summary.md)

- **Category**: Log/security search
- **Official docs**: [EQL (Event Query Language) overview](https://www.elastic.co/guide/en/elasticsearch/reference/current/eql.html)
- **Media type**: application/json (EQL queries are submitted as a JSON request body's `query` string field to Elasticsearch's `_eql/search` REST endpoint; there is no dedicated media type for EQL syntax itself).
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: mature · JavaScript: partial · Java: mature · Go: partial · Rust: partial · .NET: partial
- **Support Model**: single-vendor-commercial

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Goes well beyond single-event filtering with `sequence`/`sample` constructs (ordered/unordered multi-event correlation with `by` join keys, `with maxspan`, `until` expiration, missing-event `!` clauses) plus comparison/lookup/pattern operators and functions — purpose-built for describing multi-step attacker behavior, though Elasticsearch's own docs explicitly document that it omits several pipes and functions present in the original Endgame EQL (count, filter, sort, unique, unique_count, array functions, joins). |
| Simplicity | 3 | The base `category where condition` syntax is intuitive and SQL-like, but case-sensitivity-by-default (`==` vs `:` vs `like`/`like~`/`regex`/`regex~`), the required `~` suffix for case-insensitive functions, and sequence/sample state-machine semantics add real depth beyond simple filters. |
| Flexibility | 4 | Requires indexed fields to exist in the searched data stream (arbitrary fields must be marked optional with `?` to avoid errors) and depends on a timestamp and event-category field (defaulting to ECS `@timestamp`/`event.category`), so while it works over any JSON-like indexed document it is schema-aware rather than fully schema-free. |
| Community and Ecosystem | 3 | Backed by Elastic and used specifically within the Elastic Security/threat-hunting product line with dedicated documentation, but it is a narrower, security-domain-specific language compared to the broader adoption of Elasticsearch's own Query DSL or general-purpose query languages. |
| Extensibility | 3 | Supports a documented set of built-in functions for string/math/type manipulation and runtime fields (computed at query time via `runtime_mappings`), but there is no user-defined function or plugin mechanism for extending the EQL language itself beyond what Elasticsearch's function reference exposes. |
| Transport Compatibility | 3 | Runs over Elasticsearch's HTTP REST API (`GET/POST _eql/search`) with the query passed as a JSON body field and results returned as JSON, including async search variants (`wait_for_completion_timeout`, get/delete async search) — genuinely HTTP-native, though the EQL string itself still travels inside a JSON envelope rather than a URL query string. |
| Standardization | 1 | A single-vendor language with a documented but self-maintained syntax reference; Elasticsearch's own docs explicitly enumerate its differences from the original Endgame EQL implementation, underscoring that there is no independent standards body unifying the two dialects. |
| Security | 3 | As with most search DSLs embedded in a JSON request body, injection risk is mitigated by using EQL through the structured API (query text is a data field, not concatenated into a larger command), but no dedicated EQL security/sandboxing documentation was found beyond the general Elasticsearch access-control model, and text fields are explicitly unsupported (must query via Query DSL filter instead). |
| Performance | 4 | Runs as a native Elasticsearch search type with function/field-computation caveats explicitly documented (e.g., functions like `endsWith` can slow searches versus pre-extracting fields at index time), and supports async execution with configurable retention for long-running searches across large or frozen data tiers. |
| Orthogonality | 4 | Basic `where` conditions, sequence/sample multi-event correlation, and pipes are cleanly layered (`category where condition \| pipe`), and the same comparison/lookup/pattern operators apply consistently whether used in a simple filter or inside a sequence's per-event conditions. |

**Overall score (avg, informational only): 3.2**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

EQL is Elasticsearch's security-focused event query language, purpose-built for multi-event sequence and sample correlation (attacker behavior chains) layered over familiar `where`-clause filtering, but it deliberately omits several pipes/functions from the original Endgame EQL and has no native arbitrary-field sort or offset-based pagination, leaving those concerns to the surrounding Elasticsearch API.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```eql
any where category == "electronics" and price > 100
| tail 10
```

EQL has no native ORDER BY-style sort by an arbitrary field (results are always returned in timestamp order) and no OFFSET/LIMIT-style pagination — the `tail` pipe shown only returns the N most recent matching events by timestamp, and true "page 2" pagination over an arbitrary sort key is not expressible in EQL itself.

## Sources

- Elastic. (n.d.). [*EQL (Event Query Language) overview*](https://www.elastic.co/guide/en/elasticsearch/reference/current/eql.html).
- Elastic. (n.d.). [*EQL syntax reference*](https://www.elastic.co/guide/en/elasticsearch/reference/current/eql-syntax.html).
