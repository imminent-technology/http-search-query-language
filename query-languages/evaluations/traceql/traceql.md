# TraceQL

[↑ Full comparison table](../summary.md)

- **Category**: Analytics/Observability
- **Official docs**: [TraceQL](https://grafana.com/docs/tempo/latest/traceql/)
- **Media type**: None known — Tempo's HTTP Search API accepts a TraceQL query as a URL query parameter (`q=`) on `GET /api/search`, not a dedicated media type.
- **Evaluated**: 2026-09-07
- **Client Libraries**: Python: partial · JavaScript: partial · Java: partial · Go: mature · Rust: partial · .NET: partial
- **Support Model**: single-vendor-commercial

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | Beyond simple span-attribute filtering (`span.`/`resource.`/`event.`/`link.`/`instrumentation.` scopes plus built-in intrinsics like `span:duration`, `trace:rootService`), TraceQL has structural spanset operators (`>>`, `<<`, `>`, `<`, `~` and their `&`-prefixed "union" variants) that express ancestor/descendant/child/parent/sibling relationships between spans in a trace — effectively a join across a single trace's span tree — plus aggregates (count, avg, min, max, sum), grouping (`by()`), arithmetic, and field selection (`select()`). |
| Simplicity | 3 | Basic span selection (`{ span.http.method = "GET" }`) is simple, but the full structural-operator surface (plain vs. `&`-prefixed union variants, plus a separate "experimental" set of negated structural operators documented as prone to false positives) is a large, subtle feature set to learn. |
| Flexibility | 3 | Attribute scopes (`span.`/`resource.`/`event.`/`link.`/`instrumentation.`) are open-ended and schema-less — any custom OpenTelemetry attribute key is queryable without a fixed schema — but the language itself is rigidly modeled around the trace/span tree structure and isn't usable for non-tracing data. |
| Community and Ecosystem | 3 | Grafana Tempo has 5.5k GitHub stars and 321 contributors — a real but noticeably smaller footprint than sibling Grafana projects like Loki (28.8k stars) or Prometheus, reflecting the generally narrower adoption of dedicated tracing backends industry-wide. |
| Extensibility | 2 | TraceQL has no user-defined function or custom-operator mechanism; its adaptability comes from OpenTelemetry's open-ended attribute model, not from an extensible query grammar. |
| Transport Compatibility | 4 | Queries are passed as a URL-encoded `q` parameter to Tempo's `GET /api/search` HTTP endpoint, fitting naturally into a URL query string, the same pattern used by its sibling languages PromQL and LogQL. |
| Standardization | 2 | A single-vendor (Grafana Labs) query language with no formal, vendor-neutral specification of its own; it leans on OpenTelemetry's standardized attribute/semantic-convention model for the data it queries, but the TraceQL grammar itself isn't independently ratified. |
| Security | 4 | Structured, scope-qualified selector syntax with typed literals (integers, durations, floats, strings, nil) avoids raw string concatenation, and its regular-expression operators (`=~`, `!~`) are documented as using Go's RE2-based regexp engine, which guarantees linear-time matching and avoids the catastrophic-backtracking risk of backtracking regex engines. |
| Performance | 4 | Backed by Tempo's columnar Apache Parquet storage; scope-qualified attributes (`span.`/`resource.`/etc.) let Tempo "only scan the data you are interested in," and the docs explicitly recommend trace-level intrinsics (`trace:duration`, `trace:rootService`) over span-level ones because they require inspecting far less data. |
| Orthogonality | 3 | The `{selection} \| pipeline` model (spanset selection, structural combinators, aggregators, grouping, arithmetic, selection) composes fairly cleanly, but several structural operators are explicitly marked "experimental" due to known false positives, and the plain-vs-`&`-prefixed union distinction requires special-cased understanding to combine correctly. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

TraceQL is Grafana Tempo's PromQL/LogQL-inspired query language for distributed traces, distinguished by structural spanset operators that express ancestor/descendant/sibling relationships between spans within a trace — a join-like capability none of its sibling observability languages have. It trades formal standardization and a smaller community than Loki/Prometheus for strong expressiveness and a Parquet-backed performance model, while its structural-operator surface and lack of arbitrary-field sorting or offset pagination keep it firmly scoped to trace analysis.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page (adapted to TraceQL's span/trace model: spans carrying `category`/`price` attributes, e.g. from a product-catalog service).

```traceql
{ span.category = "electronics" && span.price > 100 }
```

TraceQL has no ORDER BY over an arbitrary attribute — results are returned in scan order by default, with only an experimental `most_recent=true` query hint to order by trace start time — and there is no offset/page pagination; the `/api/search` endpoint's `limit` parameter caps the result count with no `offset`, so further results require narrowing the `start`/`end` time window instead.

## Sources

- Grafana Labs. (n.d.). [*TraceQL*](https://grafana.com/docs/tempo/latest/traceql/).
- Grafana Labs. (n.d.). [*Construct a TraceQL query*](https://grafana.com/docs/tempo/latest/traceql/construct-traceql-queries/).
- Grafana Labs. (n.d.). [*Tempo HTTP API*](https://grafana.com/docs/tempo/latest/api_docs/).
- GitHub (Grafana Labs). (n.d.). [*grafana/tempo: Grafana Tempo is a high volume, minimal dependency distributed tracing backend.*](https://github.com/grafana/tempo).
