# Crul Queries

[↑ Full comparison table](../summary.md)

- Category: Niche/misc
- Official docs: [Queries](https://www.crul.com/docs/features/queries/)
- Media type: None known — no verifiable, actively documented standard or registered media type could be found for this query language.
- Evaluated: 2026-09-04

> Note: No independent secondary source exists for this small, niche commercial product, so this evaluation is single-sourced from the vendor's own documentation.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | A small set of pipe-chained stage commands (api, find, sort, min, max, timestamp, freeze) for orchestrating and curating API responses, with token substitution ($url$) for expanding stages, but a narrow scope focused on API-response manipulation rather than general-purpose data querying. |
| Simplicity | 4 | A readable stage-based grammar (command name, ordered arguments, --flag value flags) chained with a double-pipe `\|\|` separator, with each stage's purpose clearly documented and easy to follow. |
| Flexibility | 3 | Operates over arbitrary JSON-like API response data and supports "expanding stages" that run per-item token substitution and merge results, giving reasonable flexibility within its API-orchestration niche. |
| Community and Ecosystem | 1 | A small startup product (Crul, Inc.) with a modest Discord/Slack community and no evidence of significant broader adoption or independent ecosystem. |
| Extensibility | 2 | New commands are added by the vendor (documented in a growing commands reference), but there is no documented mechanism for users to define their own commands or extend the language themselves. |
| Transport Compatibility | 2 | Used to orchestrate and curate HTTP API calls within the Crul platform itself, rather than being a query mechanism that is embedded in or submitted over a URL. |
| Standardization | 1 | A proprietary, single-vendor query language with no independent standards body. |
| Security | 2 | No documented security-specific design; its token-substitution mechanism ($url$ replaced with piped-in values across expanding stages) resembles templating and could carry injection-style risk if untrusted data flows into subsequent stage arguments, with no built-in protections described. |
| Performance | 2 | No independent performance data is documented; the language is designed for orchestrating API calls and curating their results rather than large-scale analytical workloads. |
| Orthogonality | 4 | Every stage follows the same uniform structure (command, ordered arguments, flags) chained via a single pipe operator, giving the language a small, consistent set of composable building blocks. |

**Overall score (avg, informational only): 2.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.6**

## Summary

Crul Queries is a small, pipe-based DSL for orchestrating and curating HTTP API calls within the Crul platform, with a clean and uniform stage-based syntax, but it is a niche, single-vendor product with a tiny community, no independent standardization, and no documented security-specific design beyond its basic token-substitution mechanism.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
api get https://api.example.com/products || find "category:electronics" || sort price
```

Crul's public command reference documents `find` (keyword search) and `sort` commands but doesn't clearly specify field-based comparison filtering (e.g. price > 100), sort direction, or any pagination/limit stage — this example only approximates the scenario using the two most relevant documented commands; a genuine descending-sort/page-2 construct isn't confirmable from the available docs.

## Sources

- Crul, Inc. (n.d.). [*Queries*](https://www.crul.com/docs/features/queries/).
