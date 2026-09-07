# LogQL

[↑ Full comparison table](../summary.md)

- **Category**: Analytics/Observability
- **Official docs**: [Query Loki (LogQL)](https://grafana.com/docs/loki/latest/query/)
- **Media type**: None known — Loki's HTTP API accepts LogQL as a URL query parameter (`query=`) on `GET` endpoints, or as an `application/x-www-form-urlencoded` field on the equivalent `POST` endpoints, not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Combines a label-based stream selector with an optional pipeline of line filters (`|=`, `!=`, `|~`, `!~`), parser expressions (json, logfmt, pattern, regexp, unpack), label filters with comparison/and/or chaining, format expressions, and PromQL-derived metric aggregations (rate, count_over_time) — but there are no joins across streams and no query-level sort by an arbitrary extracted field. |
| Simplicity | 3 | Basic stream selection (`{app="foo"}`) is simple, but chaining multiple pipeline stages (filter \| parser \| label filter \| format \| metrics) and LogQL's inherited PromQL vector-matching/duration semantics for metric queries add real complexity beyond the basic shape. |
| Flexibility | 4 | Explicitly designed for "schema at query" — Loki does not require a strict schema upfront, and LogQL's parser expressions (json/logfmt/regexp/pattern/unpack) infer structure only when a query runs, so it adapts to varied and evolving log formats, though it remains tied to Loki's own label/stream architecture. |
| Community and Ecosystem | 4 | Grafana Loki has 28.8k GitHub stars, 1,281 contributors, and native Grafana integration (Explore, LogCLI, Alloy/Promtail agents), though as a single-vendor (Grafana Labs) project it is not a CNCF project the way its sibling Prometheus is. |
| Extensibility | 2 | LogQL has no user-defined function or operator mechanism; its adaptability comes from a fixed set of built-in parsers (json/logfmt/regexp/pattern/unpack), not from user-extensible query syntax. |
| Transport Compatibility | 4 | Queries are passed as a `query` URL parameter to Loki's `GET /loki/api/v1/query_range` HTTP endpoint (or URL-encoded in a POST body for long queries), fitting naturally into both URL query strings and request bodies. |
| Standardization | 2 | A single-vendor (Grafana Labs) open-source query language with no formal, vendor-neutral specification or independent ratifying body — governed entirely by the Loki project itself. |
| Security | 3 | Structured selector/pipeline syntax avoids raw string concatenation, but line/label filters accept arbitrary regular expressions (`|~`, `!~`) with no documented complexity limit comparable to a prepared-statement mechanism, making expensive queries a real operational concern. |
| Performance | 3 | Loki indexes only labels and timestamps, not log line content, so label-only queries are fast but any line-content filter (`|=`, `|~`, parser expressions) requires scanning compressed chunks — a deliberate cost/performance trade-off documented in Loki's own architecture description ("like Prometheus, but for logs"). |
| Orthogonality | 4 | The `{selector} \| pipeline` model composes predictably — each stage (filter, parser, format, metric) transforms the result of the previous one in a consistent pipe-like fashion, without the special-casing seen in some other query languages. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.4**

## Summary

LogQL is Grafana Loki's PromQL-inspired query language for logs, pairing a label-based stream selector with a composable pipeline of filters, parsers, and metric aggregations that infer log structure at query time rather than at ingestion. It trades formal standardization and query-language extensibility for a large, Grafana-native community and a deliberately cheap indexing model that only indexes labels, not log content.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page (adapted to LogQL's log-stream model: a `products` app emitting JSON log lines with `category`/`price` fields).

```logql
{app="products"} | json | category="electronics" | price > 100
```

LogQL has no ORDER BY over an arbitrary extracted field — results are strictly time-ordered, controlled only by the API's `direction=forward|backward` parameter — and there is no offset/page pagination; the `limit` API parameter caps the result count per call, and further results are fetched by re-querying with a narrower `start`/`end` time window rather than a `page`/`OFFSET` construct.

## Sources

- Grafana Labs. (n.d.). [*Query Loki (LogQL)*](https://grafana.com/docs/loki/latest/query/).
- Grafana Labs. (n.d.). [*Loki HTTP API*](https://grafana.com/docs/loki/latest/reference/loki-http-api/).
- GitHub (Grafana Labs). (n.d.). [*grafana/loki: Like Prometheus, but for logs.*](https://github.com/grafana/loki).
