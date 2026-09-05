# FQL

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [Facebook Query Language](https://en.wikipedia.org/wiki/Facebook_Query_Language) (list.csv links directly to Wikipedia, since Facebook's own FQL documentation was removed after deprecation)
- Media type: None known — the (now-deprecated) Facebook Query Language was submitted as a `q` parameter of Facebook's Graph API using generic form/JSON encoding; the feature has been retired.
- Evaluated: 2026-09-04

> Note: FQL has been fully deprecated since 2016 (Facebook API 2.0 removal); this evaluation is single-sourced to Wikipedia since the language's own vendor documentation no longer exists.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | A basic SQL-style SELECT/FROM/WHERE syntax for querying a fixed set of Facebook data tables, with no ongoing development possible since the language is deprecated. |
| Simplicity | 4 | Deliberately modeled on SQL's SELECT/FROM/WHERE syntax, making it immediately approachable to anyone with basic SQL knowledge. |
| Flexibility | 1 | Limited to a fixed, vendor-defined set of Facebook data tables (e.g. status) that could not evolve after the language was frozen and then removed entirely. |
| Community and Ecosystem | 1 | FQL was fully retired when Facebook API 2.0 was deprecated on August 7, 2016, and is no longer available or supported in any capacity. |
| Extensibility | 1 | A fixed, vendor-controlled schema with no user extension mechanism, and now permanently frozen since the platform that hosted it has been shut down. |
| Transport Compatibility | 4 | Queries were submitted directly over HTTP as a query-string parameter to the Facebook Graph API's /fql endpoint (q=[FQL]), making it genuinely URL-native while it was operational. |
| Standardization | 1 | A proprietary, single-vendor query language with no independent standards body, now entirely defunct. |
| Security | 2 | No documented security-specific design; used ordinary string-based SQL-like queries submitted via URL parameters, carrying typical injection-style risk, though this is now moot given the language's deprecation. |
| Performance | 2 | No independent performance data is documented, and the language has been non-functional since 2016. |
| Orthogonality | 3 | A simple, SQL-like clause structure (SELECT/FROM/WHERE) that was reasonably consistent, though the language's scope was too narrow to test composition much further. |

**Overall score (avg, informational only): 2.1**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.4**

## Summary

FQL was a SQL-style query language for retrieving Facebook Platform data over HTTP, easy to pick up for anyone familiar with SQL, but it was a proprietary single-vendor language with a fixed schema that Facebook fully deprecated in 2016 alongside Graph API 2.0, making its Community/Ecosystem, Extensibility, and Flexibility permanently frozen at zero further development — a useful illustration of a query language dying alongside the platform that hosted it.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```sql
SELECT uid, name, category, price FROM product
WHERE category = 'electronics' AND price > 100
ORDER BY price DESC
LIMIT 10, 10
```

FQL was fully deprecated in 2016 and its official documentation no longer exists; this query illustrates FQL's historically documented SQL-style `ORDER BY`/`LIMIT offset, count` syntax based on now-removed Facebook developer documentation, and isn't independently re-verifiable today.

## Sources

- Wikipedia. (2026, June 30). [*Facebook Query Language*](https://en.wikipedia.org/wiki/Facebook_Query_Language).
