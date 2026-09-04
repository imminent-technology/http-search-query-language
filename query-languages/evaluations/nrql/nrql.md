# NRQL

[↑ Full comparison table](../summary.md)

- Category: Analytics/Observability
- Official docs: [Get started with NRQL: the language of data](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/)
- Media type: None known — NRQL strings are submitted as a field inside a GraphQL request (`application/json`) to New Relic's NerdGraph API.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | Provides SQL-style SELECT/FROM/WHERE/FACET/LIMIT clauses plus observability-specific extensions (SINCE/UNTIL/TIMESERIES/COMPARE WITH) for time-windowed aggregation and faceted breakdowns, but is narrower in scope than general-purpose piped analytics languages. |
| Simplicity | 4 | New Relic explicitly designed NRQL to be "similar to ANSI SQL", so developers already familiar with SQL find the clause structure immediately approachable. |
| Flexibility | 3 | Queries span multiple built-in and custom event, metric, span, and log data types with per-event attribute sets, but every query still targets one of New Relic's predefined telemetry data types rather than arbitrary schema-free data. |
| Community and Ecosystem | 3 | New Relic is an established application-performance-management vendor with a large enterprise customer base, though its 2023 take-private acquisition and ~2,663 employees (per its last public filing) put its scale below the largest observability/search ecosystems evaluated. |
| Extensibility | 2 | NRQL's clause and function set is fixed and versioned by New Relic; there is no documented mechanism for user-defined functions or custom operators. |
| Transport Compatibility | 4 | Beyond the UI query builder, NRQL queries can be issued programmatically over HTTP through New Relic's NerdGraph GraphQL API, making it accessible via a standard web API. |
| Standardization | 1 | A proprietary, single-vendor query language with no independent standards body, despite its SQL-inspired syntax. |
| Security | 2 | Query strings are capped at 4 KB (a basic DoS mitigation) and use single-quoted string literals, but there is no documented parameterized-query mechanism, leaving typical string-concatenation injection risk when queries are built from user input. |
| Performance | 3 | Runs against New Relic's proprietary telemetry data platform built to ingest and query large volumes of event/metric/log data, though as a closed SaaS the underlying performance characteristics are not independently documented. |
| Orthogonality | 3 | The SELECT/FROM/WHERE/FACET/LIMIT/SINCE/UNTIL clause ordering is fixed and consistent across queries, mirroring SQL's own moderately orthogonal clause-based structure. |

**Overall score (avg, informational only): 2.8**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

NRQL is a deliberately SQL-like query language for New Relic's telemetry platform, easy to pick up for anyone who knows SQL and accessible over HTTP via the NerdGraph API, but it is a fixed, single-vendor syntax with no extensibility mechanism, no documented parameterization/injection protections, and a narrower feature set than general-purpose observability query languages like KQL or DQL.

## Sources

- New Relic, Inc. (2026). [*Get started with NRQL: the language of data*](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/).
- Wikipedia. (2026, September 2). [*New Relic*](https://en.wikipedia.org/wiki/New_Relic).
