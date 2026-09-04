# PromQL

[↑ Full comparison table](../summary.md)

- **Category**: Analytics/Observability
- **Official docs**: [Querying basics — Prometheus](https://prometheus.io/docs/prometheus/latest/querying/basics/)
- **Media type**: None known — Prometheus's HTTP API accepts PromQL as a URL query parameter or `application/x-www-form-urlencoded` field, not a dedicated media type.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Rich set of aggregation operators, functions (rate, histogram_quantile), and instant/range vector selectors purpose-built for time-series analysis, but it is narrowly scoped — no joins or filtering across non-metric data models. |
| Simplicity | 3 | Basic metric selection is simple, but vector-matching modifiers (on/ignoring/group_left/group_right), duration expressions, and staleness semantics are documented by Prometheus itself as sources of confusion (its docs include a dedicated "Gotchas" section). |
| Flexibility | 2 | Tightly coupled to Prometheus's multi-dimensional label/value time-series model; not usable for other data shapes or schemas. |
| Community and Ecosystem | 5 | A graduated CNCF project since 2018 with a massive cloud-native adoption footprint, extensive exporters, client libraries for most languages, and the de facto pairing with Grafana. |
| Extensibility | 2 | PromQL itself has no user-defined function mechanism; extensibility happens at the exporter or recording-rule level, outside the query language. |
| Transport Compatibility | 4 | Designed from the start to be sent as a parameter to Prometheus's HTTP API (instant/range query endpoints), fitting naturally into URL query strings or POST bodies. |
| Standardization | 2 | A single-project, CNCF-governed language rather than a formally standardized one; OpenMetrics standardizes the metrics exposition format consumed by Prometheus, but not PromQL's query syntax itself. |
| Security | 3 | Structured selector/function syntax avoids raw string concatenation, but there is no built-in parameterization primitive comparable to SQL prepared statements, and expensive queries can be used to overload a server (explicitly called out in Prometheus's own docs). |
| Performance | 4 | Backed by an inverted index and time-series-optimized on-disk storage, but Prometheus's own documentation warns that broad selectors (e.g. a bare metric name) can expand to thousands of series and recommends recording rules to pre-aggregate expensive queries. |
| Orthogonality | 3 | Instant vs. range vector semantics are consistent, but binary-operator vector-matching modifiers interact with aggregation in ways that require special-cased knowledge, and duration-expression syntax was layered on over time. |

**Overall score (avg, informational only): 3.2**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.1**

## Summary

PromQL is a highly specialized, HTTP-native query language optimized for one job — querying multi-dimensional time-series metrics — with an enormous ecosystem behind it, but it trades away flexibility, extensibility, and formal standardization for that specialization.

## Sources

- Prometheus Authors. (n.d.). [*Querying basics — Prometheus Documentation*](https://prometheus.io/docs/prometheus/latest/querying/basics/).
- Wikipedia. (2026, August 25). [*Prometheus (software)*](https://en.wikipedia.org/wiki/Prometheus_(software)).
