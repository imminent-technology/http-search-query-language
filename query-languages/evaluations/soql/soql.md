# SOQL

- **Category**: Relational/SQL-family
- **Official docs**: [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm)
- **Media type**: None known — submitted as a URL-encoded `q` query-string parameter on Salesforce's REST API.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | SELECT-based syntax supports filtering, ordering, parent-to-child/child-to-parent relationship queries and aggregate functions, but explicitly disallows arbitrary joins, field-list wildcards, or calculation expressions that SQL allows. |
| Simplicity | 4 | Intentionally modeled on the familiar SQL SELECT statement, easy to learn for anyone with SQL experience. |
| Flexibility | 2 | Tightly bound to the Salesforce object schema (standard and custom objects/fields); not usable outside the platform or against schema-less data. |
| Community and Ecosystem | 3 | Large, active Salesforce developer ecosystem with extensive official documentation and tooling (Apex, VS Code extension, CLI), though entirely platform-specific. |
| Extensibility | 2 | No user-defined functions or operators; extension is limited to built-in functions and relationship queries exposed by Salesforce. |
| Transport Compatibility | 4 | Designed to be passed as a query string parameter in the REST API's query resource or as the queryString in the SOAP API, fitting naturally into an HTTP request. |
| Standardization | 1 | A single-vendor proprietary syntax defined solely by Salesforce, with no independent specification or alternate implementations. |
| Security | 3 | Apex requires bind variables (":variable") in embedded SOQL, mitigating injection, but dynamically string-built SOQL is also common and vulnerable if not escaped. |
| Performance | 3 | Relies on Salesforce's own query optimizer and selectivity/indexing guidance, but strict governor limits on rows and queries per transaction constrain optimization compared to a general-purpose database. |
| Orthogonality | 3 | Core SELECT/WHERE/ORDER BY compose in a SQL-like way, but the lack of arbitrary joins/subquery placement and relationship-query rules introduce Salesforce-specific special-casing. |

**Overall score (avg, informational only): 2.8**

## Summary

SOQL is a deliberately SQL-like, HTTP-transportable query language purpose-built for the Salesforce platform, easy to learn but structurally limited to Salesforce's object schema and query features (no arbitrary joins or wildcards), with a single vendor governing its evolution.

## Sources

- Salesforce, Inc. (n.d.). [*Salesforce Object Query Language (SOQL)*](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).
