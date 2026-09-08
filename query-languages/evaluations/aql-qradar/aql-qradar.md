# AQL (QRadar)

[↑ Full comparison table](../summary.md)

- **Category**: Log/security search
- **Official docs**: [Ariel Query Language (AQL)](https://www.ibm.com/docs/en/qsip/7.5.0?topic=aql-ariel-query-language)
- **Media type**: None known — AQL statements are submitted as plain text through the QRadar Console's Log Activity/Network Activity search UI or the QRadar REST API's `ariel/searches` resource (a JSON-wrapped query string), not as an independently registered media type.
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: none · JavaScript: none · Java: none · Go: none · Rust: none · .NET: none
- **Support Model**: single-vendor-commercial

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A SQL-style query language over the Ariel event/flow database supporting SELECT/WHERE/ORDER BY/LIMIT/GROUP BY, arithmetic and comparison operators, BETWEEN, IN, LIKE/ILIKE, regex MATCHES/IMATCHES, a documented full-text TEXT SEARCH keyword, bitwise operators, subqueries, and time-criteria (START/STOP) clauses tailored specifically to security event/flow analysis. |
| Simplicity | 4 | Deliberately modeled on SQL syntax (`SELECT ... FROM ... WHERE ... ORDER BY ... LIMIT`), which is quickly approachable for anyone with SQL experience, with a small, well-documented operator table. |
| Flexibility | 2 | Purpose-built to query QRadar's own fixed Ariel database schema (events, flows, simarc) with a documented, largely fixed set of event/flow/simarc fields plus custom properties — it is not a general-purpose or schema-free query language for arbitrary data. |
| Community and Ecosystem | 2 | A single-vendor (IBM) query language scoped entirely to the QRadar SIEM product, with documentation and support channels tied to IBM's own product ecosystem rather than an independent community or multi-vendor adoption. |
| Extensibility | 2 | Supports custom properties (regex- or calculation-based fields defined within QRadar) and a documented library of data calculation/formatting/aggregation/retrieval functions, but there is no user-defined-function or plugin mechanism for extending the AQL language grammar itself. |
| Transport Compatibility | 2 | Executed via the QRadar Console UI or the documented `ariel/searches` REST API resource (query text wrapped in a JSON request), so it is HTTP-reachable through IBM's own API, but it has no independent URL-embeddable query-string form or IANA-registered content type of its own. |
| Standardization | 1 | A single-vendor, product-specific query language documented only in IBM's own QRadar manuals, with no external specification or standards-body involvement. |
| Security | 2 | No dedicated AQL injection-prevention or sandboxing documentation was found in the operators/reference pages reviewed; queries are typically issued by authenticated QRadar users/analysts through the product's own access-controlled UI or REST API rather than being built from untrusted end-user input, so the language's own security posture is largely inherited from QRadar's platform-level authentication and RBAC rather than anything AQL-specific. |
| Performance | 4 | Runs against Ariel, QRadar's purpose-built time-series event/flow database, and the documentation explicitly recommends the LIMIT clause together with mandatory START/STOP time-window bounds precisely to keep large-scale security log searches performant. |
| Orthogonality | 3 | WHERE-clause operators, ORDER BY/COLLATE, and LIMIT are documented as independent, composable clauses following familiar SQL clause ordering, though the required START/STOP time-window clause is a security-analytics-specific addition layered on top of the SQL-like core rather than a fully orthogonal, general-purpose construct. |

**Overall score (avg, informational only): 2.6**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.9**

## Summary

IBM QRadar's Ariel Query Language (AQL) is a SQL-styled, single-vendor query language purpose-built to search QRadar's Ariel events/flows database, combining familiar SELECT/WHERE/ORDER BY/LIMIT syntax with security-analytics-specific additions (mandatory time-window START/STOP clauses, full-text TEXT SEARCH) — at the cost of being scoped entirely to QRadar's fixed schema and product ecosystem, with no native offset-based pagination.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```aql
SELECT * FROM events
WHERE category = 'electronics' AND price > 100
ORDER BY price DESC
LIMIT 10
START '2024-01-01 00:00' STOP '2024-01-02 00:00'
```

AQL has no OFFSET-style pagination clause — LIMIT only caps the number of returned results (like a page size), and the mandatory START/STOP clause bounds the search by a time window rather than skipping to a later page. "Page 2 of 10 per page" is therefore not natively expressible in AQL; only the first N results within a given time range can be retrieved directly.

## Sources

- IBM. (2026, March 6). [*AQL logical and comparison operators*](https://www.ibm.com/docs/en/qsip/7.5.0?topic=language-aql-logical-comparison-operators). IBM QRadar SIEM 7.5.0 Documentation.
- IBM. (n.d.). [*Ariel Query Language (AQL)*](https://www.ibm.com/docs/en/qsip/7.5.0?topic=aql-ariel-query-language). IBM QRadar SIEM 7.5.0 Documentation.
