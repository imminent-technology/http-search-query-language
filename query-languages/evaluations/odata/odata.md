# OData

[↑ Full comparison table](../summary.md)

- **Category**: API/data-fetching
- **Official docs**: [odata.org](https://www.odata.org/)
- **Media type**: `application/json` with OData-specific parameters (e.g. `odata.metadata=minimal|full|none`, `odata.streaming=true`, `odata.ieee754compatible=true`) per the OData JSON Format v4.01 spec; older services also supported `application/atom+xml` (Atom), now a deprecated committee-specification-stage format as of OData 4.0. No dedicated `application/odata+json` (or similar) media type is registered in the IANA Media Types registry as of this writing.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | The URL-Conventions spec defines a rich $filter/$orderby expression grammar (logical, arithmetic, string, date/time, geo, and lambda `any`/`all` operators), $expand for related-entity graphs, $compute for derived properties, and $crossjoin for Cartesian products across unrelated entity sets — but $expand only follows navigation properties predefined in the service's CSDL metadata, and aggregation (GROUP BY-style) is a separate, non-core Data Aggregation extension rather than part of the base spec. |
| Simplicity | 3 | Basic queries read like plain URL parameters (`$filter=Name eq 'Milk'&$orderby=Price`), but the full grammar — parameter aliases, `$it`/`$this`/`$root` literals, nested `$expand($select=...;$filter=...)` sub-query options, and lambda operators — adds real complexity once queries go beyond simple filtering. |
| Flexibility | 2 | Every OData service publishes a CSDL metadata document describing its entity types, and query options are validated against that schema; open/dynamic properties are supported but are the exception rather than the default, unlike a schema-less document store. |
| Community and Ecosystem | 4 | Backed by an OASIS technical committee with members including Microsoft, SAP, IBM, and Citrix, and adopted by SAP NetWeaver Gateway, Microsoft Graph/Office 365, Salesforce Connect, and the DMTF Redfish hardware-management API, with independent libraries like Apache Olingo (Java) and RESTier (.NET). |
| Extensibility | 4 | Services can define bound/unbound custom functions and actions, and the spec explicitly reserves non-`$`/`@`-prefixed custom query options for service-specific extensions; vocabularies (Core, Capabilities, Measures) let services annotate schemas with additional semantics without changing the base protocol. |
| Transport Compatibility | 5 | OData is purpose-built around URL query-string conventions for GET requests, and also defines a `/$query` POST convention (with a `text/plain` body) specifically so long filter expressions that would exceed URL length limits can still be sent — giving it both a native URL form and a documented request-body fallback. |
| Standardization | 5 | OData 4.0/4.01 is an OASIS Standard produced by a dedicated technical committee and was subsequently approved as ISO/IEC 20802-1:2016 and 20802-2:2016, with multiple independent implementations (Microsoft, SAP, Apache Olingo) — a formal, vendor-neutral standardization path matching SQL's own. |
| Security | 3 | Query options are validated against a typed Entity Data Model rather than executed as raw strings, which reduces some injection surface, but `$filter`/`$orderby` still accept a string expression grammar, and the spec itself does not mandate parameterized backend execution, leaving injection risk dependent on how a given service implementation translates OData expressions into its own storage queries. |
| Performance | 3 | The spec lets services reject unsupported query options and computes `$count` after filtering, giving implementations room to use indexes on typed properties, but — like SQL — the protocol itself mandates no specific optimization strategy and leaves query-planning quality entirely to the backing service. |
| Orthogonality | 4 | System query options ($filter, $select, $expand, $orderby, $top/$skip, $count, $search, $compute) are designed to compose predictably — $expand can carry its own nested $filter/$select/$orderby, and $it/$this/$root literals give consistent, well-defined scoping rules across nested expressions. |

**Overall score (avg, informational only): 3.7**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.5**

## Summary

OData is a formally standardized (OASIS/ISO) protocol for URL-native REST query conventions, pairing strong transport compatibility and a rich filter/expand grammar with a schema-bound data model that trades away the flexibility of schema-less alternatives.

## Sources

- OData.org (OASIS OData Technical Committee). (n.d.). [*OData - the best way to REST*](https://www.odata.org/).
- OASIS. (2020, April 23). [*OData Version 4.01. Part 2: URL Conventions*](https://docs.oasis-open.org/odata/odata/v4.01/odata-v4.01-part2-url-conventions.html).
- Wikipedia. (2026, February 12). [*Open Data Protocol*](https://en.wikipedia.org/wiki/Open_Data_Protocol).
