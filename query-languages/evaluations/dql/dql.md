# DQL

- Category: Analytics/Observability
- Official docs: [Dynatrace Query Language](https://docs.dynatrace.com/docs/platform/grail/dynatrace-query-language) (list.csv links the equivalent `dynatrace.com/support/help` URL, which redirects here)
- Media type: None known — Dynatrace's Grail Query REST API accepts DQL as a JSON field within a generic `application/json` body.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Covers logs, metrics, security data, business events, and Davis AI problems/events through a rich set of documented commands, functions, and operators purpose-built for exploring data and building statistical models. |
| Simplicity | 3 | Dynatrace maintains a dedicated "DQL compared to SQL and more" comparison guide, implying the pipe-based syntax requires real reorientation for users coming from SQL or other query languages. |
| Flexibility | 5 | Explicitly designed to require "no up-front description of the input data's schema, contrary to relational databases like SQL tables", running against the schema-on-read Grail data lakehouse for arbitrary event data. |
| Community and Ecosystem | 3 | Dynatrace is a large, publicly traded observability vendor (~US$2.0 billion revenue, S&P 400 component in 2026), but DQL itself is a newer language introduced alongside the Grail lakehouse (2022) with a comparatively small dedicated user community relative to older, more established query languages. |
| Extensibility | 3 | Ships with a documented, evolving library of commands, functions, and operators that Dynatrace continues to expand, though the language itself is closed and versioned entirely by Dynatrace. |
| Transport Compatibility | 3 | Executed primarily through Dynatrace's own platform UI apps and Grail query API rather than embedded directly in a URL, though it is reachable over HTTP-based API calls. |
| Standardization | 1 | A proprietary, single-vendor query language specific to the Dynatrace Grail platform, with no independent standards body. |
| Security | 2 | No distinctive built-in anti-injection mechanism is documented (unlike KQL's dot-prefixed management-command separation); queries are typically built and submitted as strings, carrying conventional injection risk if built from unsanitized input. |
| Performance | 4 | Purpose-built for Dynatrace's Grail data lakehouse, engineered specifically for high-scale, schema-on-read analytics over telemetry, security, and business event data. |
| Orthogonality | 4 | Follows the same pipe-based command-chaining model as other modern observability query languages (e.g. KQL, Splunk SPL), giving it a small, consistent set of composable building blocks. |

**Overall score (avg, informational only): 3.2**

## Summary

DQL is Dynatrace's purpose-built query language for its schema-on-read Grail data lakehouse, offering strong flexibility across logs, metrics, security, and business event data with a consistent pipe-based composition model, but as a newer, single-vendor language it lacks external standardization, has a smaller dedicated community than more established observability languages, and has no documented built-in injection-prevention design.

## Sources

- Dynatrace LLC. (2026, January 28). [*Dynatrace Query Language*](https://docs.dynatrace.com/docs/platform/grail/dynatrace-query-language).
- Wikipedia. (2026, September 1). [*Dynatrace*](https://en.wikipedia.org/wiki/Dynatrace).
